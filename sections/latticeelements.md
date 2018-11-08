{% include lib/mathjax.html %}

# Lattice elements

Using the main input file, one can define a single undulator to simulate in Puffin. However, the undulator line in a modern FEL is usually composed of several undulator modules, interspersed with beam optical elements such as focusing quadrupoles and delays or phase shifters. To simulate this, a lattice file can be supplied which describes the layout of the modules and other elements. If it is supplied, the single undulator described in the main input file is ignored.

All common lattice elements except from the undulators employed on the undulator line to focus or delay the beam are currently included as point transforms only. They are specified in the lattice file by their 2 letter identifier, followed by their required parameters.

Elements should be listed sequentially in the order they are placed in the beam line. An example layout is given below:

```
UN  'planepole'  29   1.0   0.0   30   1.0   1.0   0.0    0.0
DR 1.6455
CH  0.0  0.966  0.0 
QU 2.39 -2.39
UN  'planepole'  29   1.0   0.0   30   1.0   1.0   0.0    0.0
DR 1.6455
CH  0.0  0.966  0.0 
QU -2.39 2.39
UN  'planepole'  29   1.0   0.0   30   1.0   1.0   0.0    0.0
```

which will give an undulator (indicated by `UN`), followed by a free-space drift (`DR`), followed by a chicane (`CH`), then a quadrupole (`QU`), then an undulator, *etc.* The elements, their 2 letter ID's, and description of following parameters are given below.

## Undulator

Identifier: **UN**

Example line
```
UN  'planepole'  29   1.0   0.0   30   1.0   1.0   0.0    0.0
```

with parameters after the ID corresponding to, in order:

 - undulator type, with choice of `'planepole', 'helical', 'curved'`, and `''` (blank - indicating variable polarization)
 - The number of undulator periods $$N_u$$
 - The tuning of the undulator parameter $$\alpha = a_u / a_{u0}$$, where $$a_{u0}$$ is the 'reference' tuning in the main input file (the undulator period cannot be varied, so this is really the ratio of magnetic field strengths)
 - The undulator taper (linear) $$d\alpha / d \bar{z}$$
 - The number of integration steps to use per undulator period
 - The relative size of the undulator $$x$$-polarised field strength $$u_x$$ (between $$0$$ and $$1$$) (ignored/overwritten if not using the variably polarized undulator)
 - The relative size of the undulator $$y$$-polarised field strength $$u_y$$ (between $$0$$ and $$1$$) (ignored/overwritten if not using the variably polarized undulator)
 - The strong in-undulator focusing wavenumber $$\bar{k}_{\beta SF x}$$
 - The strong in-undulator focusing wavenumber $$\bar{k}_{\beta SF y}$$


## Quadrupole

Identifier: **QU**

Example line
```
QU 2.39 -2.39
```

For the quad, we must specify $$\bar{F}_x$$ and $$\bar{F}_y$$. These are scaled transverse components of the transform matrix for the quad. The quad is only a point transform, currently, and does not have a length, so the length must be included in a drift section. The transforms for the quad, in S.I. units, are defined as

$$
\frac{d x_j}{d z}  \bigg|_{new} = \frac{d x_j}{d z} \bigg|_{old} + \frac{1}{F_x} x_j \\
\frac{d y_j}{d z}  \bigg|_{new} = \frac{d y_j}{d z} \bigg|_{old} + \frac{1}{F_y} y_j
$$

which in the scaled notation becomes:

$$
\frac{d \bar{p}_{xj}}{d \bar{z}} \bigg|_{new} = \frac{d \bar{p}_{xj}}{d \bar{z}}  \bigg|_{old} +\frac{\sqrt{\eta}}{2\rho\kappa} \frac{\bar{x}_j}{\bar{F}_x} \\
\frac{d \bar{p}_{yj}}{d \bar{z}}  \bigg|_{new} = \frac{d \bar{p}_{yj}}{d \bar{z}}  \bigg|_{old} +\frac{\sqrt{\eta}}{2\rho\kappa} \frac{\bar{y}_j}{\bar{F}_y}
$$

where $$\bar{F}_{x,y} = \dfrac{F_{x,y}}{l_g}$$.

In $$x$$ (unscaled) focal length is taken as

$$
\frac{1}{F_x} = \frac{g L_Q}{B\rho},
$$

where $$g$$ is the quad magnetic field gradient in $$Tm^{-1}$$, $$L_Q$$ is the length of the quad, and $$B\rho = \beta E_0 / 0.2998$$ is the so-called magnetic rigidity in $$Tm$$, with the beam energy $$E_0$$ in $$GeV$$ (corresponding to the scaling energy defined in the input file).

## Chicane

Identifier: **CH**

For the chicane, one must specify physical length, slippage length, and dispersion enhancement (scaled $$R_{56}$$). The length is the physical length of the device in undulator periods, and is used to calculate the diffraction properly. The slippage length tells how many wavelengths to delay the beam by relative to the radiation field in resonant radiation wavelengths - be careful, this should not be $$\leq 0$$, or the beam will then be faster than light speed! Similarly, it is left up to the user to decide what is appropriate to delay the beam by with respect to the physical length of the device. The dispersive enhancement, $$D$$, is the scaled $$R_{56}$$ of the device - using $$\gamma_r$$ in the main input as the mean $$\gamma$$ for the chicane, so that

$$
\bar{z}_{2} = \bar{z}_{20} - 2D \left( \frac{\gamma - \gamma_r}{\gamma_r}  \right) + \bar{l}_{slip},
$$

and $$D = k_r \rho  R_{56}$$.

This approach of being able to vary the 3 parameters above is quite flexible, but at the expense of easy automatic checking of the physical relevance of the parameters. For example, one can disperse the beam 'in place', without shifting it w.r.t. the resonant wavelength, which is obviously unphysical. However, this may be useful for a quick setup of the beam for EEHG at the beginning of the undulator, for instance. If one is not sure of the physical length of the actual device, but knows the length between modules and the desired slippage (e.g. for mode locking the FEL), then one can specify the spatial drift between modules using a drift section, and then specify a chicane with zero physical length, but with the desired delay and $$R_{56}$$. In this way the radiation diffraction will still be modelled correctly.

## Drift

Identifier: **DR**

For the drift, one must specify length in units of the number of undulator periods.

## Modulation

Identifier: **MO**

For the modulation section, one may add an energy modulation to the beam specified by $$\bar{k}_M = \dfrac{2 \pi}{\bar{\lambda}_M}$$ and $$\dfrac{\Delta \gamma}{\gamma_r}$$.



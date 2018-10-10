{% include lib/mathjax.html %}

# System of Equations Solved by Puffin

The scaled equations are:

$$
\Bigl[\frac{1}{2}\Bigl(\frac{\partial^2}{\partial\bar{x}^2} + \frac{\partial^2}{\partial\bar{y}^2}\Bigr) -  \frac{\partial^2}{\partial\bar{z}\partial\bar{z}_2}\Bigr]A_{\bot}  & = -\frac{1}{\bar{n}_p}\frac{\partial}{\partial \bar{z}_2}\sum_{j=1}^{N} \frac{\bar{p}_{\bot j}}{\Gamma_j} (1+\eta p_{2j})     \delta^3(\bar{x}_j,\bar{y}_j,\bar{z}_{2j})  \\
\frac{d \bar{p}_{\bot j}}{d \bar{z}} = & \frac{1}{2\rho}\Bigl[ i \alpha b_{\bot} - \frac{\eta p_{2j}}{\kappa^2}A_{\bot} \Bigr] - i\kappa \frac{ \bar{p}_{\bot j}}{\Gamma_j} (1 + \eta p_{2j})  \alpha b_z \\
\frac{d \Gamma_{j}}{d \bar{z}} &= - \rho \frac{(1 + \eta p_{2j})}{\Gamma_j} (\bar{p}_{\bot j} A^*_{\bot j} + c.c.)  \\
\frac{d\bar{z}_{2j}}{d\bar{z}}& = p_{2j}  \label{z2eqgen2} \\
\frac{d\bar{x}_j}{d\bar{z}} &=  \frac{2 \rho \kappa}{\sqrt{\eta} \Gamma_j} (1 + \eta p_{2j}) \Re(\bar{p}_{\bot j}) \\
\frac{d\bar{y}_j}{d\bar{z}} &= - \frac{2 \rho \kappa}{\sqrt{\eta} \Gamma_j}  (1 + \eta p_{2j}) \Im(\bar{p}_{\bot j}).
$$


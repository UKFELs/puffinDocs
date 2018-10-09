{% include lib/mathjax.html %}

# Notation Conventions

The direction of travel of the electron beam and radiation field is along the $$ z $$ or $$ t $$ axis. Transverse dimensions are $$x$$ and $$y$$.

## To scale or not to scale?

Although the Puffin algorithm uses scaled variables, the beam and radiation field parameters may be input in either SI units or the scaled units. Use the variable **qscaled** in the main input file to specify whether scaled or SI units are being used. If **qscaled** $$=$$ **.true.**, then Puffin expects scaled variables are being used. If, instead, If **qscaled** $$=$$ **.false.**, SI units are used, and the input parameters will be scaled internally by Puffin to the scaling values specified in the main input file.

The main algorithm in Puffin utilizes the scaled variables above to make the numbers 'nicer' to work with. The system saturates with scaled intensity $$ \sim 1 $$, the scaled perpendicular momentum of the beam in the wiggler oscillates between $$-1$$ and $$1$$, and so forth. The distance through the wiggler is given in units of a (1D) gain length, and the beam coordinate in the radiation frame is in units of the cooperation length $$l_c$$, so that a reference electron slips one $$l_c$$ through the radiation field in one gain length. The scaling defines a frame of reference which normalises the quantities not only to numerically more manageable numbers, but to *characteristic* variables.

The two dominant variables for the scaling are $$\rho$$ and $$\eta$$. $$\eta$$ is a function of the wiggler parameters $$a_u$$ and $$\lambda_u$$, and **reference** beam energy $$\gamma_r$$, and is calculated in Puffin from the input values of these 3 variables. It defines the velocity of the *reference* electron in the scaled radiation frame. The $$ \bar{z}_2 $$ coordinate is in the scaled frame travelling with the field (at velocity $$c$$) - $$\eta$$ determines how quickly the electrons slip back through this frame, such that an electron with energy $$\gamma_r$$, travelling in a wiggler with parameters $$a_u$$ and $$\lambda_u$$, slips back with scaled velocity $$p_2 \equiv \dfrac{d \bar{z}_2}{d\bar{z}} = 1$$.

The $$\rho$$ parameter is dependent on the peak electron beam number density, amongst other things, and as far as the discussion of the scaling parameters in Puffin goes, defines a reference for the amplification characteristics. A beam, or indeed, sections of an electron beam with peak number density giving a smaller, *localised* $$\rho$$ will amplify the beam more slowly with respect to the reference beam specified by $$\rho$$.

That is to say, that they are only *scaling* parameters. The FEL parameter as input by the user does not have to correspond to the beam or wiggler being input for the results to be correct. The scaled parameters will behave nicely if it does, but it is not necessary for the result to be physically correct. When the result is unscaled, the result will still be correct. The user may input in SI units, and get output in SI units. If using scaled units as input, the user must scale the lengths appropriately, but still, no beam input needs to satisfy the conditions to actually give the $$\rho$$ input by the user.

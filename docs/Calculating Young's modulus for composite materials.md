```ad-hint
title:FEM modeling PCBs
collapse:open
This methodology is great for doing FEA for PCBs by modeling them as shell elements with predetermined thickness. You can use a [[Material IDs in Nastran|MAT8 ID]] for the material properties and assign the two moduli for longitudinal modulus and transverse modulus respectively.
```

```ad-note
collapse:open
These equations are valid for the [elastic region](https://www.quora.com/What-is-the-elastic-region-on-a-stress-strain-curve) of those materials.
```


## Laminates Young's modulus in the longitudinal direction
![[Young's modulus for laminate composites (longitudinal)|700]]
We define the strain of the materials as: $$STRAIN = \frac{delta L}{L}$$
The applied force is shared between the fiber and the matrix as defined by the force equilibrium equation: $$ F_c=F_f+F_m$$
With the help of the definition of stress ($σ=\frac{F}{A}$), we can change the above to $$σ_cA_c=σ_fA_f+σ_mA_m\tag{1}$$
In the equation above, $A_f$ corresponds to the total cross-sectional area of the fibers and $A_m$ to the total cross-sectional area of the matrix, respectively.
Since we consider this composite material to have great bonding, hence act as a single sheet, we can assume: $$ε_c=ε_f=ε_m\tag{2}$$
Since we are in the [elastic region](https://www.quora.com/What-is-the-elastic-region-on-a-stress-strain-curve) of the stress-strain diagram, we can say: $$σ_c=E_cε_c,\;\;\;σ_f=E_fε_f,\;\;\;σ_m=E_mε_m \tag{3}$$
From (1) & (2) we derive:
$$E_mε_mA_c=E_fε_fA_f+E_mε_mA_m\;\;\;$$
And using (3) the above yields:
```ad-important
title:Elastic modulus of composite materials in longitudinal direction
collapse:open
$$E_c=E_f(\frac{A_f}{A_c})+E_m(\frac{A_m}{A_c})\tag{to use 1}$$
```

```ad-info
title:Rule of mixtures
collapse:open
If the fibers span along the whole length of the matrix, then because of the relationship $\frac{A_f}{A_c}=\frac{A_f}{A_c}\frac{L}{L}=\frac{v_f}{v_c}=V_f$,

we have $$E_c=E_fV_f+E_mV_m$$

This is called the "rule of mixtures"!
```

In the same manner we can derive the strength, Poisson's ratio, thermal conductivity, etc. in the fiber direction.


## Laminates Young's modulus in the Transverse direction
![[Young's modulus for laminate composites (transverse)|700]]
The force equilibrium for this case is $$F_c=F_f=F_m$$
For laminates, since they have the same cross-sectional area, we can say that $$σ_c=σ_f=σ_m\tag{4}$$
Now, as we said above for the longitudinal direction, if the fibers extend to the whole length of the matrix, we can use the terms $V_f$ and $V_m$. So from the above we can say: $$ε_c=ε_fV_f+ε_mV_m\tag{5}$$
We can again use the stress-strain equations of the elastic regions and get: $$\frac{σ_c}{E_c}=\frac{σ_f}{E_f}V_f+\frac{σ_m}{E_m}V_m$$
and from equation (4) the above yields: $$\frac{1}{E_c}=\frac{V_f}{E_f}+\frac{V_m}{E_m}$$
or
```ad-important
title:Elastic modulus of composite materials in transverse direction
collapse:open
$$E_c=\frac{E_fE_m}{V_fE_m+V_mE_f}\tag{to use 2}$$
```


## Poisson ratio for laminates; force applied in longitudinal direction

To derive the equations for the poisson ratios, we need to do an analysis of the composite with regards to strains. This way we can derive equations that relate the poisson ratio of the composite  ($ν_c$) and the poisson ratios of the fiber ($ν_f$) and the matrix ($ν_m$). The poisson ratios mentioned are defined as:
$$ε_{cL}=ε_{mL}=ε_{fL}\;\;\;strain\;in\;longitudinal\;direction\tag{2}$$
$$ε_c=ε_fV_f+ε_mV_m\;\;\; strain\; in \; transverse\; direction\tag{5}$$
$$ν_{fL}=\frac{ε_{fT}}{ε_{fL}}\;\;\;poisson's\;ratio\;of\;fiber;force\;applied\;in\;longitudinal\;direction\tag{6}$$
$$ν_{mL}=\frac{ε_{mT}}{ε_{mL}}\;\;\;poisson's\;ratio\;of\;matrix;force\;applied\;in\;longitudinal\;direction\tag{7}$$
We will try to define the poisson ratio of the composite material in the case of a force applied in the longitudinal direciton. We have the equation:
$$ν_{cL}=\frac{ε_{cT}}{ε_{cL}}$$
Using equation (2) and (5) we have:
$$ν_{cL}=\frac{ε_{fT}V_f+ε_{mT}V_m}{ε_{cL}}=\frac{ε_{fT}}{ε_{fL}}V_f+\frac{ε_{mT}}{ε_{mL}}V_m$$
Finally, with the definitions (6) and (7) we yield:
```ad-important
title:Poisson ratio for laminates with force applied in longitudinal direction
collapse=open
$$ν_{cL}=ν_{fL}V_f+ν_{mL}V_m\tag{to use 3}$$
```


## Sources and additional info:
[Composite Analysis for Modulus and Strength in the Longitudinal Direction](https://www.youtube.com/watch?v=WhcBM568TlM)
[Composite Analysis in Transverse Orientation for Elastic Modulus and Strength](https://www.youtube.com/watch?v=HG-grOpfpkA)
Helpful video for poisson's ratio:
[# Meaning of Engineering Constants for a Orthotropic Materials: Their Interpretation](https://www.youtube.com/watch?v=GVWThYQpWOM)
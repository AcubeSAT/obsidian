## MAT 1
## MAT 8
[MAT 8](https://knowledge.autodesk.com/search-result/caas/CloudHelp/cloudhelp/2019/ENU/NSTRN-Reference/files/GUID-C9C1D3A3-8338-4E15-8B5E-B2498A6EEE45-htm.html) is an ID which defines the material property for an orthotropic material for isoparametric shell elements. The image below is how the format looks like
![[MAT 8 format.png]]
This is an ID that can only be applied for PSHELL or PCOMP elements.
```ad-note
title:Modeling PCBs
collapse:open
These characteristics make this material ID ideal for modeling PCBs. Cause one can derive the [[Calculating Young's modulus for composite materials|sum of the layers' properties]] and include a single material ID for a shell mesh instead of a mesh for every layer seperately.
```

#### Required properties for MAT8:
* MID : This is just the identification number of the material. Can be any integer > 0.
* E1 : Modulus of elasticity in longitudinal direction, also defined as the fiber direction or 1 direction. Can be any non-zero real number.
* E2 : Modlulus of elasticity in transverse direction, also defined as the matrix direction or 2-direction. Can be any non-zero real number.
* NU12 : Poisson's ratio ($\frac{ε_2}{ε_1}$ for uniaxial loading in 1-direction). Can be a real number (by the definition of poisson's ratio, it makes sense for this number to be between -1 and 0.5)
* (Not required, but important)
  RHO : Mass density. Can be real $\geq$ 0 or blank.
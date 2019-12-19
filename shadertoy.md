---
layout: page
title: Shadertoy
permalink: /shadertoy/
---


Spectral Cornell box
====================
[<img src="../images/shadertoy/WtlSWM.jpg" class="img-thumbnail rounded mx-auto d-block" alt="Cornell box">](https://www.shadertoy.com/view/WtlSWM)

This Shadertoy renders a Cornell box in spectral using the official specifications
for spectral reflectance. Those are resampled each 1nm to ease the computations.
It uses XYZ Colour Matching Functions (CMFs) to transform radiance for a wavelength
to a tristimulus.

It is not meant to be fast but simple and as close as possible with the Cornell's
specifications with a proper tonemapping. Some improvements can be made but are not
going to be done in this version to keep it as simple as possible.

<br>

Diffraction by a prism
======================
<div class="row">
    <div class="col-sm">
        <a href="https://www.shadertoy.com/view/wlSXz3"><img src="../images/shadertoy/wlSXz3.jpg" class="img-thumbnail rounded mx-auto d-block" alt="Prism 1"></a>
    </div>
    <div class="col-sm">
        <a href="https://www.shadertoy.com/view/wt2SRy"><img src="../images/shadertoy/wt2SRy.jpg" class="img-thumbnail rounded mx-auto d-block" alt="Prism 2"></a>
    </div>
</div>
<br>
Shows the dispersion by a prism made of Dense flint glass SF10.
You can tweak the index of refraction and the light dispersion in cauchy_ior
function from Common tab (from line 144).
 
You can also change the orientation of the prism by changing the PRISM_ROT define
in Common tab.

<br>

Colour matching functions
=========================
[<img src="../images/shadertoy/WtsXW4.jpg" class="img-thumbnail rounded mx-auto d-block" alt="CMFs">](https://www.shadertoy.com/view/WtsXW4)

This shadertoy shows the comparison between various Colour Matching Functions (CMFs).
- CIE 1931 2°
- Judd & Vos 2°
- CIE 1964 10°
- CIE 2006 2°

Shown in range 380 - 720 nm (left to right).  
Intensity from 0 to 1 (bottom to top).

<br>

Interferences
=============
[<img src="../images/shadertoy/wt2XR3.jpg" class="img-thumbnail rounded mx-auto d-block" alt="Interferences">](https://www.shadertoy.com/view/wt2XR3)

Interferences caused by two slits (Young experiment). Viewed from top. A vertical slice is what would be observable on a screen. I used Fresnel vectors to accumulate both amplitude and phase shift.

You can change the slits 
- aperture with hotizontal clic and drag.
- distance with vertical clic and drag.

You can change the wavelength by pressing on your keyboard:
- 4 -> 400nm
- 5 -> 500nm
- 6 -> 600nm
- 7 -> 700nm

<br>

Misc
====
[<img src="../images/shadertoy/3ljXDd.jpg" class="img-thumbnail rounded mx-auto d-block" alt="Sound visualiser">](https://www.shadertoy.com/view/3ljXDd)

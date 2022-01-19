---
layout: page
title: Shadertoys
permalink: /shadertoy/
---

Here is a partial list of some of my Shadertoys. You can find all my Shadertoys on my profile page: [https://www.shadertoy.com/user/stack_overflow](https://www.shadertoy.com/user/stack_overflow).

Spectral Cornell box
====================

<div class="w3-content" style="max-width:500px">
  <div class="w3-card">
    <a href="https://www.shadertoy.com/view/WtlSWM">
      <img src="/images/shadertoy/WtlSWM.jpg" alt="Cornell box" />
    </a>
  </div>
</div>
<br>

This Shadertoy renders a Cornell box in spectral using the official specifications
for spectral reflectance. Those are resampled each 1 nm to ease the computations.
It uses XYZ Colour Matching Functions (CMFs) to transform radiance for a wavelength
to a tristimulus.

It is not meant to be fast but simple and as close as possible with the Cornell's
specifications with a proper tone mapping. Some improvements can be made but are not
going to be done in this version to keep it as simple as possible.

<br>

Dispersion by a prism
======================
<div class="w3-row-padding">
  <div class="w3-col m6 l6">
    <div class="w3-card">
      <a href="https://www.shadertoy.com/view/wlSXz3">
        <img src="../images/shadertoy/wlSXz3.jpg" class="w3-image" alt="Prism 1">
      </a>
    </div>
  </div>
  <div class="w3-col m6 l6">
    <div class="w3-card">
      <a href="https://www.shadertoy.com/view/wt2SRy">
        <img src="/images/shadertoy/wt2SRy.jpg" class="w3-image" alt="Prism 2">
      </a>
    </div>
  </div>
</div>
<br>

Shows the dispersion by a prism made of Dense flint glass SF10.
You can tweak the index of refraction and the light dispersion in `cauchy_ior`
function from Common tab (from line 144).
 
You can also change the orientation of the prism by changing the `PRISM_ROT` define
in Common tab.

<br>

Demo
====

<div class="w3-content" style="max-width:500px">
  <div class="w3-card">
    <a href="https://www.shadertoy.com/view/ttfBz4">
      <img src="/images/shadertoy/ttfBz4.jpg" alt="AFIG contest" />
    </a>
  </div>
</div>
<br>

This shader was created for an AFIG (*Association Française d'Informatique Graphique*) Shadertoy contest in 2020. It won the second place.


Colour matching functions
=========================

<div class="w3-content" style="max-width:500px">
  <div class="w3-card">
    <a href="https://www.shadertoy.com/view/WtsXW4">
      <img src="/images/shadertoy/WtsXW4.jpg" alt="CMFs" />
    </a>
  </div>
</div>
<br>

This Shadertoy shows the comparison between various Colour Matching Functions (CMFs).
- CIE 1931 2°
- Judd & Vos 2°
- CIE 1964 10°
- CIE 2006 2°

Shown in range 380 - 720 nm (left to right).  
Intensity from 0 to 1 (bottom to top).

<br>

Interferences
=============

<div class="w3-content" style="max-width:500px">
  <div class="w3-card">
    <a href="https://www.shadertoy.com/view/wt2XR3">
      <img src="/images/shadertoy/wt2XR3.jpg" alt="Interferences" />
    </a>
  </div>
</div>
<br>

Interferences caused by two slits (Young experiment). Viewed from top. A vertical slice is what would be observable on a screen. I used Fresnel vectors to accumulate both amplitude and phase shift.

You can change the slits'
- Aperture with horizontal click and drag.
- Distance with vertical click and drag.

You can change the wavelength by pressing on your keyboard:
- 4 -> 400 nm
- 5 -> 500 nm
- 6 -> 600 nm
- 7 -> 700 nm

<br>

Misc
====

<div class="w3-content" style="max-width:500px">
  <div class="w3-card">
    <a href="https://www.shadertoy.com/view/3ljXDd">
      <img src="/images/shadertoy/3ljXDd.jpg" alt="Sound visualiser" />
    </a>
  </div>
</div>
<br>


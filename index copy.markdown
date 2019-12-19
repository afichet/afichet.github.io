---
layout: home
---
<h1 class="display-1">Welcome</h1>

<div class="row">
    <div class="col-md-7">
        <p>
        This is my academic website.
        </p>

        <p>
        I defended my PhD on December 2019. I was under the supervision of <a href="https://artis.inria.fr/Members/Nicolas.Holzschuch/">Nicolas Holzschuch</a>. The subject of my PhD is efficient representation for measured reflectance.
        </p>

        <p>
        I did a year exchange in Czech Republic at Charles University in <a href="http://cgg.mff.cuni.cz/">Computer Graphics Group</a> under the supervision of <a href="http://cgg.mff.cuni.cz/~wilkie">Alexander Wilkie</a> and <a href="http://cgg.mff.cuni.cz/~jaroslav">Jaroslav Křivánek</a>. 
        </p>
    </div>
    <div class="col-md-5">
        <div class="card">
        <h4 class="card-header">Contact</h4>
        <div class="card-body">
        <p class="card-text">
            MAVERICK<br>
            INRIA Grenoble Rhône-Alpes<br>
            655, avenue de l’Europe<br>
            38330 Montbonnot Saint-Martin<br>
            France<br>
            <a href="mailto:alban.fichet@inria.fr">alban.fichet@inria.fr</a>
        </p>
        </div>
        </div>
    </div>
</div>

Shadertoy
=========
<div class="row">
    <div class="col-sm">
        <a href="https://www.shadertoy.com/view/WtlSWM"><img src="../images/shadertoy/WtlSWM.jpg" class="img-thumbnail rounded mx-auto d-block" alt="Prism 1"></a>
    </div>
    <div class="col-sm">
        <a href="https://www.shadertoy.com/view/wlSXz3"><img src="../images/shadertoy/wlSXz3.jpg" class="img-thumbnail rounded mx-auto d-block" alt="Prism 2"></a>
    </div>
    <div class="col-sm">
        <a href="https://www.shadertoy.com/view/3ljXDd"><img src="../images/shadertoy/3ljXDd.jpg" class="img-thumbnail rounded mx-auto d-block" alt="Prism 2"></a>
    </div>
</div>
<br>
<div class="text-right">
<a href="shadertoy"><button class="btn btn-outline-primary">More...</button></a>
</div>
<br>

Publications
============
<div class="card">
    <h3 class="card-header">2018</h3>
    <div class="container h-100">
        <div class="row no-gutters align-items-center h-100">
            <div class="col-md-2 mx-auto">
                <img src="images/18_teaser_fluo.png" class="card-img img-thumbnail" alt="teaser">
            </div>
            <div class="col-md-10">
                <div class="card-body">
                    <h4 class="card-title"><a href="https://hal.inria.fr/hal-01818826">Handling Fluorescence in a Uni-directional Spectral Path Tracer</a></h4>
                    <p class="card-text">Michal Mojzík, Alban Fichet, Alexander Wilkie</p>
                    <p class="card-text"><small>We present two separate improvements to the handling of fluorescence effects in modern uni-directional spectral rendering systems. The first is the formulation of a new distance tracking scheme for fluorescent volume materials which exhibit a pronounced wavelength asymmetry. Such volumetric materials are an important and not uncommon corner case of wavelength-shifting media behaviour, and have not been addressed so far in rendering literature. The second one is that we introduce an extension of Hero wavelength sampling which can handle fluorescence events, both on surfaces, and in volumes. Both improvements are useful by themselves, and can be used separately: when used together, they enable the robust inclusion of arbitrary fluorescence effects in modern uni-directional spectral MIS path tracers. Our extension of Hero wavelength sampling is generally useful, while our proposed technique for distance tracking in strongly asymmetric media is admittedly not very efficient. However, it makes the most of a rather difficult situation, and at least allows the inclusion of such media in uni-directional path tracers, albeit at comparatively high cost. Which is still an improvement since up to now, their inclusion was not really possible at all, due to the inability of conventional tracking schemes to generate sampling points in such volume materials.</small></p>
                    <p class="card-text"><small class="text-muted">Computer Graphics Forum, Wiley, 2018, 37 (4), pp.77 - 94. ⟨10.1111/cgf.13477⟩</small></p>
                </div>
            </div>
        </div>
    </div>
</div>

<div class="card">
    <h3 class="card-header">2016</h3>
    <div class="container h-100">
        <div class="row no-gutters align-items-center h-100">
            <div class="col-md-2 mx-auto">
                <img src="images/16_teaser.jpg" class="card-img img-thumbnail" alt="teaser">
            </div>
            <div class="col-md-10">
                <div class="card-body">
                    <h4 class="card-title"><a href="https://hal.inria.fr/hal-01302120v2">Capturing Spatially Varying Anisotropic Reflectance Parameters using Fourier Analysis</a></h4>
                    <p class="card-text">Alban Fichet, Imari Sato, Nicolas Holzschuch</p>
                    <p class="card-text"><small>Reflectance parameters condition the appearance of objects in photorealistic rendering. Practical acquisition of reflectance parameters is still a difficult problem. Even more so for spatially varying or anisotropic materials, which increase the number of samples required. In this paper, we present an algorithm for acquisition of spatially varying anisotropic materials, sampling only a small number of directions. Our algorithm uses Fourier analysis to extract the material parameters from a sub-sampled signal. We are able to extract diffuse and specular reflectance, direction of anisotropy, surface normal and reflectance parameters from as little as 20 sample directions. Our system makes no assumption about the stationarity or regularity of the materials, and can recover anisotropic effects at the pixel level.</small></p>
                    <p class="card-text"><small class="text-muted">Graphics Interface Conference 2016, Jun 2016, Victoria, BC, Canada. pp.65-73, ⟨10.20380/GI2016.09⟩</small></p>
                </div>
            </div>
        </div>
    </div>
</div>



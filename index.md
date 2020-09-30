---
layout: home
---

<div class="w3-row">
  <div class="w3-col m7 l7 w3-padding-large">
    <p>
    This is my academic website.
    </p>
    <p>I am a postdoctoral researcher at Institut d'Optique Graduate School in Bordeaux working with <a href="http://manao.inria.fr/perso/~pac/research.php">Romain Pacanowski</a>.
	</p>
    <p>
    I defended my PhD on December 2019. I was under the supervision of <a href="https://artis.inria.fr/Members/Nicolas.Holzschuch/">Nicolas Holzschuch</a>. The subject of my PhD is efficient representation for measured reflectance. You can access my manuscript here: <a href="https://tel.archives-ouvertes.fr/tel-02893514">https://tel.archives-ouvertes.fr/tel-02893514</a>.
    </p>
    <p>
    I did a year exchange in Czech Republic at Charles University in <a href="http://cgg.mff.cuni.cz/">Computer Graphics Group</a> under the supervision of <a href="http://cgg.mff.cuni.cz/~wilkie">Alexander Wilkie</a> and <a href="http://cgg.mff.cuni.cz/~jaroslav">Jaroslav Křivánek</a>. 
    </p>
  </div>
  <div class="w3-col m5 l5">
    <div class="w3-card">
      <header class="w3-container w3-light-grey">
      <h2>Contact</h2>
      </header>
    <div class="w3-container">
      <p><a href="mailto:alban.fichet@inria.fr">alban.fichet@gmx.fr</a><br>
      <a href="/assets/Alban_Fichet_0x5FA927F9_pub.asc">PGP Key: 6836 06E7 73C3 AF5A D048 D5D0 7049 35AF 5FA9 27F9</a></p>
    </div>
    </div>
  </div>
</div>

# Shadertoy

<div class="w3-row-padding">
  <div class="w3-col m4 l4">
    <div class="w3-card">
      <a href="https://www.shadertoy.com/view/WtlSWM"><img src="../images/shadertoy/WtlSWM.jpg" class="w3-image" alt="Cornell box"></a>
    </div>
  </div>
  <div class="w3-col m4 l4">
    <div class="w3-card">
      <a href="https://www.shadertoy.com/view/wlSXz3"><img src="../images/shadertoy/wlSXz3.jpg" class="w3-image" alt="Prism"></a>
    </div>
  </div>
  <div class="w3-col m4 l4">
    <div class="w3-card">
      <a href="https://www.shadertoy.com/view/3ljXDd"><img src="../images/shadertoy/3ljXDd.jpg" class="w3-image" alt="Sound visualiser"></a>
    </div>
  </div>
</div>
<p></p>
<div class="w3-display-container">
<p class="w3-right">
<a href="shadertoy" class="w3-button w3-blue">More...</a>
</p>
</div>
<p><br></p>

# Publications

## 2018

<div class="w3-section">
  <div class="w3-card">
    <header class="w3-container w3-light-grey">
      <h4>
        <a href="https://hal.inria.fr/hal-01818826">
          Handling Fluorescence in a Uni-directional Spectral Path Tracer
        </a>
      </h4>
    </header>
    <div class="w3-row w3-display-container">
      <div class="w3-col m3 l3 w3-padding-small w3-display-right">
        <img src="images/18_teaser_fluo.png" class="w3-round" alt="teaser" />
      </div>
      <div class="w3-col m9 l9 w3-padding-small">
        <p>Michal Mojzík, Alban Fichet, Alexander Wilkie</p>
        <p>
          <small>
            We present two separate improvements to the handling of
            fluorescence effects in modern uni-directional spectral rendering
            systems. The first is the formulation of a new distance tracking
            scheme for fluorescent volume materials which exhibit a pronounced
            wavelength asymmetry. Such volumetric materials are an important and
            not uncommon corner case of wavelength-shifting media behaviour, and
            have not been addressed so far in rendering literature. The second
            one is that we introduce an extension of Hero wavelength sampling
            which can handle fluorescence events, both on surfaces, and in
            volumes. Both improvements are useful by themselves, and can be used
            separately: when used together, they enable the robust inclusion of
            arbitrary fluorescence effects in modern uni-directional spectral
            MIS path tracers. Our extension of Hero wavelength sampling is
            generally useful, while our proposed technique for distance tracking
            in strongly asymmetric media is admittedly not very efficient.
            However, it makes the most of a rather difficult situation, and at
            least allows the inclusion of such media in uni-directional path
            tracers, albeit at comparatively high cost. Which is still an
            improvement since up to now, their inclusion was not really possible
            at all, due to the inability of conventional tracking schemes to
            generate sampling points in such volume materials.
          </small>
        </p>
      </div>
    </div>
    <footer class="w3-container w3-white">
      <p class="card-text">
        <small>
          Computer Graphics Forum, Wiley, 2018, 37 (4), pp.77 - 94.
          ⟨10.1111/cgf.13477⟩
        </small>
      </p>
    </footer>
  </div>
</div>

## 2016

<div class="w3-section">
  <div class="w3-card">
    <header class="w3-container w3-light-grey">
      <h4>
        <a href="https://hal.inria.fr/hal-01302120v2">
          Capturing Spatially Varying Anisotropic Reflectance Parameters using Fourier Analysis
        </a>
      </h4>
    </header>
    <div class="w3-row w3-display-container">
      <div class="w3-col m3 l3 w3-padding-small w3-display-right">
        <img src="images/16_teaser.jpg" class="w3-round" alt="teaser" />
      </div>
      <div class="w3-col m9 l9 w3-padding-small">
        <p>Alban Fichet, Imari Sato, Nicolas Holzschuch</p>
        <p>
          <small>
            Reflectance parameters condition the appearance of objects in photorealistic rendering. Practical acquisition of reflectance parameters is still a difficult problem. Even more so for spatially varying or anisotropic materials, which increase the number of samples required. In this paper, we present an algorithm for acquisition of spatially varying anisotropic materials, sampling only a small number of directions. Our algorithm uses Fourier analysis to extract the material parameters from a sub-sampled signal. We are able to extract diffuse and specular reflectance, direction of anisotropy, surface normal and reflectance parameters from as little as 20 sample directions. Our system makes no assumption about the stationarity or regularity of the materials, and can recover anisotropic effects at the pixel level.
          </small>
        </p>
      </div>
    </div>
    <footer class="w3-container w3-white">
      <p class="card-text">
        <small>
          Graphics Interface Conference 2016, Jun 2016, Victoria, BC, Canada. pp.65-73, ⟨10.20380/GI2016.09⟩
        </small>
      </p>
    </footer>
  </div>
</div>
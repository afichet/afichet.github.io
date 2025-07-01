---
layout: home
---

<div class="w3-row">
  <div class="w3-col m8 l8 w3-padding-large">
    <p>I am a software research engineer at <a href="https://www.intel.com">Intel</a> in the <a href="https://ggx-research.github.io/">Grenoble GraphiX Research Team</a>. I worked previously at <a href="https://unity.com/">Unity Technologies</a>.</p>
    <p>From February 2021 to January 2022, I was a postdoctoral researcher at Charles University in Prague, Czech Republic working with <a href="https://cgg.mff.cuni.cz/~wilkie/Website/Home.html">Alexander Wilkie</a>. In 2020, I did a one year post-doc at Institut d'Optique Graduate School in Bordeaux, France working with <a href="http://manao.inria.fr/perso/~pac/research.php">Romain Pacanowski</a>.</p>
    <p>I defended my PhD on December 2019. I was under the supervision of <a href="https://artis.inria.fr/Members/Nicolas.Holzschuch/">Nicolas Holzschuch</a>. The subject of my PhD is efficient representation for measured reflectance. You can access my manuscript here: <a href="https://tel.archives-ouvertes.fr/tel-02893514">https://tel.archives-ouvertes.fr/tel-02893514</a>.</p>
    <p>I did a year exchange in Czech Republic at Charles University in <a href="http://cgg.mff.cuni.cz/">Computer Graphics Group</a> under the supervision of <a href="http://cgg.mff.cuni.cz/~wilkie">Alexander Wilkie</a> and <a href="http://cgg.mff.cuni.cz/~jaroslav">Jaroslav Křivánek</a>.</p>
  </div>
  <div class="w3-col m4 l4">
    <div class="rounded_background">
      <header class="w3-container">
        <h2>Contact</h2>
      </header>
      <div class="w3-container">
        <!-- <img src="images/profile.jpg" class="w3-round teaser_image" /> -->
        <p>email: <a href="mailto:alban.fichet@gmx.fr">alban.fichet@gmx.fr</a></p>
        <p><a href="https://keys.openpgp.org/vks/v1/by-fingerprint/683606E773C3AF5AD048D5D0704935AF5FA927F9">PGP Key: 6836 06E7 73C3 AF5A D048 D5D0 7049 35AF 5FA9 27F9</a></p>
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
    <a href="https://www.shadertoy.com/user/stack_overflow" class="w3-button w3-blue">More...</a>
  </p>
</div>

<p><br></p>

# Publications

## 2025

<!--  Non-Orthogonal Reduction for Rendering Fluorescent Materials in Non-Spectral Engines  -->
<div class="container_papers rounded_background">
  <div class="teaser_image_col">
    <a href="https://arxiv.org/pdf/2505.19672">
      <img src="images/25_teaser_fluo_edit.png" class="w3-round teaser_image" alt="teaser" />
    </a>
  </div>
  <div class="paper_text_col">
    <div class="post-list-heading">
      <p><a href="https://arxiv.org/pdf/2505.19672">
          A Fluorescent Material Model for Non-Spectral Editing & Rendering
      </a></p>
    </div>
    <div class="post-meta">
      <p>Laurent Belcour, Alban Fichet, Pascal Barla</p>
    </div>
    <div class="post-content">
      <p>
          In this work, we introduce an analytical approach to the editing and rendering of fluorescence in a non-spectral engine. It is based on a decomposition of the reduced reradiation matrix, and an analytically-integrable Gaussian-based model of the fluorescent component. The model reproduces the appearance of fluorescent materials accurately, especially with the addition of a UV basis. Most importantly, it grants variations of fluorescent material parameters in real-time, either for the editing of fluorescent materials, or for the dynamic spatial variation of fluorescence properties across object surfaces. A simplified one-Gaussian fluorescence model even allows for the artist-friendly creation of plausible fluorescent materials from scratch, requiring only a few reflectance colors as input.
      </p>
    </div>
    <div class="post-meta">
      <a href="https://arxiv.org/pdf/2505.19672">ACM SIGGRAPH 2025</a>
    </div>
  </div>
</div>

<!--  Non-Orthogonal Reduction for Rendering Fluorescent Materials in Non-Spectral Engines  -->
<div class="container_papers rounded_background">
  <div class="teaser_image_col">
    <a href="https://jcgt.org/published/0014/01/04/">
      <img src="images/25_teaser_spectral_jxl.png" class="w3-round teaser_image" alt="teaser" />
    </a>
  </div>
  <div class="paper_text_col">
    <div class="post-list-heading">
      <p><a href="https://jcgt.org/published/0014/01/04/">
        Compression of Spectral Images using Spectral JPEG XL
      </a></p>
    </div>
    <div class="post-meta">
      <p>Alban Fichet, Christoph Peters</p>
    </div>
    <div class="post-content">
      <p>
          We propose a method to accurately handle fluorescence in a non-spectral (e.g., tristimulus) rendering engine, showcasing color-shifting and increased luminance effects. Core to our method is a principled reduction technique that encodes the re-radiation into a low-dimensional matrix working in the space of the renderer’s Color Matching Functions (CMFs). Our process is independent of a specific CMF set and allows for the addition of a non-visible ultraviolet band during light transport. Our representation visually matches full spectral light transport for measured fluorescent materials even for challenging illuminants. The advantages of spectral rendering are increasingly well known, and corresponding rendering algorithms have matured. In this context, spectral images are used as input (e.g., reflectance and emission textures) and output of a renderer. Their large memory footprint is one of the big remaining issues with spectral rendering. Our method applies a cosine transform in the wavelength domain. We then reduce the dynamic range of higher-frequency Fourier coefficients by dividing them by the mean brightness, i.e., the Fourier coefficient for frequency zero. Then we store all coefficient images using JPEG XL. The mean brightness is perceptually most important and we store it with high quality. At higher frequencies, we use higher compression ratios and optionally lower resolutions. Our format supports the full feature set of spectral OpenEXR, but compared to this lossless compression, we achieve file sizes that are 10 to 60 times smaller than their ZIP compressed counterparts.
      </p>
    </div>
    <div class="post-meta">
      <a href="https://jcgt.org/published/0014/01/04/">Journal of Computer Graphics Techniques</a>
    </div>
  </div>
</div>

## 2024

<!--  Non-Orthogonal Reduction for Rendering Fluorescent Materials in Non-Spectral Engines  -->
<div class="container_papers rounded_background">
  <div class="teaser_image_col">
    <a href="https://arxiv.org/abs/2406.17360">
      <img src="images/24_teaser_fluo_rgb.png" class="w3-round teaser_image" alt="teaser" />
    </a>
  </div>
  <div class="paper_text_col">
    <div class="post-list-heading">
      <p><a href="https://arxiv.org/abs/2406.17360">
         Non-Orthogonal Reduction for Rendering Fluorescent Materials in Non-Spectral Engines
      </a></p>
    </div>
    <div class="post-meta">
      <p>Alban Fichet, Laurent Belcour, Pascal Barla</p>
    </div>
    <div class="post-content">
      <p>
      We propose a method to accurately handle fluorescence in a non-spectral (e.g., tristimulus) rendering engine, showcasing color-shifting and increased luminance effects. Core to our method is a principled reduction technique that encodes the re-radiation into a low-dimensional matrix working in the space of the renderer’s Color Matching Functions (CMFs). Our process is independent of a specific CMF set and allows for the addition of a non-visible ultraviolet band during light transport. Our representation visually matches full spectral light transport for measured fluorescent materials even for challenging illuminants.
      </p>
    </div>
    <div class="post-meta">
      <a href="https://arxiv.org/abs/2406.17360">Computer Graphics Forum &lt;10.1111/cgf.15150&gt; </a>
    </div>
  </div>
</div>


## 2022

<!-- Efficient Storage and Importance Sampling for Fluorescent Reflectance -->
<div class="container_papers rounded_background">
  <div class="teaser_image_col">
    <a href="https://doi.org/10.1111/cgf.14716">
      <img src="images/22_teaser_cgf.png" class="w3-round teaser_image" alt="teaser" />
    </a>
  </div>
  <div class="paper_text_col">
    <div class="post-list-heading">
      <p><a href="https://doi.org/10.1111/cgf.14716">
        Efficient Storage and Importance Sampling for Fluorescent Reflectance
      </a></p>
    </div>
    <div class="post-meta">
      <p>Qingqin Hua, Vojtěch Tázlar, Alban Fichet, Alexander Wilkie</p>
    </div>
    <div class="post-content">
      <p>
      We propose a technique for efficient storage and importance sampling of fluorescent spectral data. Fluorescence is fully described by a reradiation matrix, which for a given input wavelength indicates how much energy is reemitted at other wavelengths. However, such representation has a considerable memory footprint. To significantly reduce memory requirements, we propose the use of Gaussian mixture models for the representation of reradiation matrices. Instead of the full-resolution matrix, we work with a set of Gaussian parameters that also allow direct importance sampling. Furthermore, if accuracy is of concern, a reradiation matrix can be used jointly with efficient importance sampling provided by the Gaussian mixture. In this paper, we present our pipeline for efficient storage of bispectral data and provide its extensive evaluation on a large set of bispectral measurements. We show that our method is robust and colour accurate even with its comparably minor memory requirements and that it can be seamlessly integrated into a standard Monte Carlo path tracer.
      </p>
    </div>
    <div class="post-meta">
      <a href="https://doi.org/10.1111/cgf.14716">Computer Graphics Forum &lt;10.1111/cgf.14716&gt; </a>
    </div>
  </div>
</div>


## 2021


<!-- Efficient Spectral Rendering on the GPU for Predictive Rendering -->
<div class="container_papers rounded_background">
  <div class="teaser_image_col">
    <a href="https://hal.inria.fr/hal-03331619">
      <img src="images/21_teaser_rtg.png" class="w3-round teaser_image" alt="teaser" />
    </a>
  </div>
  <div class="paper_text_col">
    <div class="post-list-heading">
      <p><a href="https://hal.inria.fr/hal-03331619">
        Efficient Spectral Rendering on the GPU for Predictive Rendering
      </a></p>
    </div>
    <div class="post-meta">
      <p>David Murray, Alban Fichet, Romain Pacanowski</p>
    </div>
    <div class="post-content">
      <p>
      Current graphic processing units (GPU) in conjunction with specialized APIs
      open the possibility of interactive path tracing. Spectral rendering is
      necessary for accurate and predictive light transport simulation, especially to
      render specific phenomena such as light dispersion. However, it requires
      larger assets than traditional RGB rendering pipelines. Thanks to the
      increase of available onboard memory on newer graphic cards, it becomes
      possible to load larger assets onto the GPU, making spectral rendering
      feasible. In this chapter, we describe the strengths of spectral rendering and
      present our approach for implementing a spectral path tracer on the GPU. We
      also propose solutions to limit the impact on memory when handling finely
      sampled spectra or large scenes.
      </p>
    </div>
    <div class="post-meta">
      <a href="https://doi.org/10.1007/978-1-4842-7185-8">Ray Tracing Gems II, Apress, Berkeley, CA 2021 - Chapter 42 pp.673 - 698 &lt;10.1007/978-1-4842-7185-8&gt; </a>
    </div>
  </div>
</div>


<!-- A Compact Representation for Fluorescent Spectral Data -->
<div class="container_papers rounded_background">
  <div class="teaser_image_col">
      <a href="https://hal.archives-ouvertes.fr/hal-03274233">
        <img src="images/21_teaser_fluo_gmm.png" class="w3-round teaser_image" alt="teaser" />
      </a>
  </div>
  <div class="paper_text_col">
    <div class="post-list-heading">
      <p><a href="https://hal.archives-ouvertes.fr/hal-03274233">
        A Compact Representation for Fluorescent Spectral Data
      </a></p>
    </div>
    <div class="post-meta">
      <p>Qingqin Hua, Alban Fichet, Alexander Wilkie</p>
    </div>
    <div class="post-content">
      <p>
      We propose a technique to efficiently importance sample and
      store fluorescent spectral data. Fluorescence behaviour is
      properly represented as a re-radiation matrix: for a given
      input wavelength, this matrix indicates how much energy is
      re-emitted at all other wavelengths. However, such a 2D
      representation has a significant memory footprint,
      especially when a scene contains a high number of
      fluorescent objects or fluorescent textures. We propose to
      use Gaussian Mixture Domain to model re-radiation, which
      allows us to significantly reduce the memory
      footprint. Instead of storing the full matrix, we work with
      a set of Gaussian parameters that also allow direct
      importance sampling. When accuracy is a concern, one can
      still use the re-radiation matrix data, and just benefit
      from importance sampling provided by the Gaussian
      Mixture. Our method is useful when numerous fluorescent
      materials are present in a scene, and in particular for
      textures with fluorescent components.
      </p>
    </div>
    <div class="post-meta">
      <a href="https://doi.org/10.2312/sr.20211305">Eurographics Symposium on Rendering (EGSR) &lt;10.2312/sr.20211305&gt; </a>
    </div>
  </div>
</div>


<!-- An OpenEXR Layout for Spectral Images -->
<div class="container_papers rounded_background">
  <div class="teaser_image_col">
    <a href="https://hal.inria.fr/hal-03252797">
      <img src="images/21_teaser_spectral_exr.png" class="w3-round teaser_image" alt="teaser" />
    </a>
  </div>
  <div class="paper_text_col">
    <div class="post-list-heading">
      <p><a href="https://hal.inria.fr/hal-03252797">
        An OpenEXR Layout for Spectral Images
      </a></p>
    </div>
    <div class="post-meta">
      <p>Alban Fichet, Romain Pacanowski, Alexander Wilkie</p>
    </div>
    <div class="post-content">
      <p>
      We propose a standardised layout to organise spectral data
      stored in OpenEXR images. We motivate why we chose the
      OpenEXR format as basis for our work, and we explain our
      choices with regard to data selection and organisation:
      our goal is to define a standard for the exchange of
      measured or simulated spectral and bi-spectral data. We
      also provide sample code to store spectral images in
      OpenEXR format.
      </p>
    </div>
    <div class="post-meta">
      <a href="https://jcgt.org/published/0010/03/01/">Journal of Computer Graphics Techniques</a>
    </div>
  </div>
</div>


## 2018


<!-- Handling Fluorescence in a Uni-directional Spectral Path Tracer -->
<div class="container_papers rounded_background">
  <div class="teaser_image_col">
    <a href="https://hal.inria.fr/hal-01818826">
      <img src="images/18_teaser_fluo.png" class="w3-round teaser_image" alt="teaser" />
    </a>
  </div>
  <div class="paper_text_col">
    <div class="post-list-heading">
      <p><a href="https://hal.inria.fr/hal-01818826">
        Handling Fluorescence in a Uni-directional Spectral Path Tracer
      </a></p>
    </div>
    <div class="post-meta">
      <p>Michal Mojzík, Alban Fichet, Alexander Wilkie</p>
    </div>
    <div class="post-content">
      <p>
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
      </p>
    </div>
    <div class="post-meta">
      <a href="https://dx.doi.org/10.1111/cgf.13477">Computer Graphics Forum, Wiley, 2018, 37 (4), pp.77 - 94. &lt;10.1111/cgf.13477&gt;</a>
    </div>
  </div>
</div>

## 2016


<!-- Capturing Spatially Varying Anisotropic Reflectance Parameters using Fourier Analysis -->
<div class="container_papers rounded_background">
  <div class="teaser_image_col">
    <a href="https://hal.inria.fr/hal-01302120v2">
      <img src="images/16_teaser.jpg" class="w3-round teaser_image" alt="teaser" />
    </a>
  </div>
  <div class="paper_text_col">
    <div class="post-list-heading">
      <p><a href="https://hal.inria.fr/hal-01302120v2">
        Capturing Spatially Varying Anisotropic Reflectance Parameters using Fourier Analysis
      </a></p>
    </div>
    <div class="post-meta">
      <p>Alban Fichet, Imari Sato, Nicolas Holzschuch</p>
    </div>
    <div class="post-content">
      <p>
      Reflectance parameters condition the appearance of objects in photorealistic rendering. Practical acquisition of reflectance parameters is still a difficult problem. Even more so for spatially varying or anisotropic materials, which increase the number of samples required. In this paper, we present an algorithm for acquisition of spatially varying anisotropic materials, sampling only a small number of directions. Our algorithm uses Fourier analysis to extract the material parameters from a sub-sampled signal. We are able to extract diffuse and specular reflectance, direction of anisotropy, surface normal and reflectance parameters from as little as 20 sample directions. Our system makes no assumption about the stationarity or regularity of the materials, and can recover anisotropic effects at the pixel level.
      </p>
    </div>
    <div class="post-meta">
      <a href="https://dx.doi.org/10.20380/GI2016.09">Graphics Interface Conference 2016, Jun 2016, Victoria, BC, Canada. pp.65-73, &lt;10.20380/GI2016.09&gt;</a>
    </div>
  </div>
</div>

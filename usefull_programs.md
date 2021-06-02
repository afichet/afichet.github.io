---
layout: page
title: Programs
permalink: /programs/
---

On this page, a non-exhaustive list of the projects I have contributed in or developed.

Some are very small piece of software but can be usefull.

- Spectral renderers
  - [Malia Rendering Framework (MRF)](#mrf)
  - [The Advanced Rendering Toolkit (ART)](#art)
- [Spectral Viewer](#spectral-viewer)
- OpenEXR tools
  - [OpenEXR Viewer](#openexr-viewer)
  - [Linux OpenEXR thumbnailer](#openexr-thumbnailer-linux)
  - [gThumb extension for OpenEXR](#openexr-gthumb-extension)
  - [OpenEXR / TIFF conversion](https://github.com/yama-chan/openexr-converter)
  - [OpenEXR diff tool](https://github.com/afichet/exr-diff)
- Other
  - [MERL / UTIA BRDF support for Python](https://github.com/afichet/brdf-snippets)

You also can find me:
- [On GitHub](https://github.com/afichet)
- [On GitLab](https://gitlab.com/afichet)

Spectral Renderers
==================

MRF
----

I am contributing in the development of MRF, *Malia Rendering Framework*, a GPU accelerated spectral renderer.

<div class="w3-row-padding">
    <div class="w3-card">
      <img src="../images/materials.png" class="w3-image" alt="Cornell box">
    </div>
</div>

<br>

<div class="w3-display-container">
<p class="w3-right">
<a href="https://pacanows.gitlabpages.inria.fr/MRF/main.md.html" class="w3-button w3-blue">Website...</a>
</p>
</div>

<p><br></p>

ART
----

I joined the long time running development of ART, *The Advanced Rendering Toolkit*, initially developed by [Robert f. Tobler](http://cgg.mff.cuni.cz/ART/archivers/dedication.html), currently maintained by [Alexander Wilkie](http://cgg.mff.cuni.cz/~wilkie) during my year in Czech Republic. 

<div class="w3-row-padding">
  <div class="w3-col m4 l4">
    <div class="w3-card">
      <img src="../images/CornellBox.jpg" class="w3-image" alt="Cornell box">
    </div>
  </div>
  <div class="w3-col m4 l4">
    <div class="w3-card">
      <img src="../images/SphereStage_TS.jpg" class="w3-image" alt="BRDF showcase">
    </div>
  </div>
  <div class="w3-col m4 l4">
    <div class="w3-card">
      <img src="../images/SIGGRAPH_2012_fluo_scene.jpg" class="w3-image" alt="Fluorescence">
    </div>
  </div>
</div>

<br>

<div class="w3-display-container">
<p class="w3-right">
<a href="http://cgg.mff.cuni.cz/ART" class="w3-button w3-blue">Website...</a>
</p>
</div>

<p><br></p>

Spectral Viewer
===============
I am participating in the development of an open source spectral image viewer that supports several images formats: ENVI, ART Raw (spectral), OpenEXR, PNG, JPEG...

<div class="w3-row-padding">
    <div class="w3-card">
      <img src="../images/spectralviewer.png" class="w3-image" alt="Cornell box">
    </div>
</div>

<br>

<div class="w3-display-container">
<p class="w3-right">
<a href="https://adufay.gitlabpages.inria.fr/SpectralViewer/" class="w3-button w3-blue">Website...</a>
</p>
</div>

<p><br></p>

OpenEXR tools
=============

OpenEXR Viewer
--------------
A simple tool I wrote to show detailed information about OpenEXR files. It is yet in a preliminary state.

<div class="w3-row-padding">
    <div class="w3-card">
      <img src="https://user-images.githubusercontent.com/7930348/119243717-bbb39200-bb69-11eb-8ad2-b8937cb31508.png" class="w3-image" alt="Cornell box">
    </div>
</div>

<br>

<div class="w3-display-container">
<p class="w3-right">
<a href="https://github.com/afichet/openexr-viewer" class="w3-button w3-blue">GitHub...</a>
</p>
</div>

<p><br></p>

OpenEXR Thumbnailer (Linux)
---------------------------
Display thumbnails / preview of your OpenEXR files in your file manager:
- [GitHub](https://github.com/yama-chan/openexr-thumbnailer)
- [Arch Linux AUR](https://aur.archlinux.org/packages/openexr-thumbnailer/)
- [PPA Ubuntu](https://launchpad.net/~alban-f/+archive/ubuntu/openexr-thumbnailer)

### Install on Ubuntu:
```
sudo add-apt-repository ppa:alban-f/openexr-thumbnailer
sudo apt-get update
sudo apt install openexr-thumbnailer
```
<br>

OpenEXR gThumb extension
------------------------
gThumb extension to support display of OpenEXR format:
- [GitHub](https://github.com/yama-chan/gthumb-openexr-extension)
- [Arch Linux AUR](https://aur.archlinux.org/packages/gthumb-openexr-extension/)
- [PPA Ubuntu](https://launchpad.net/~alban-f/+archive/ubuntu/gthumb-openexr-extension)

### Install on Arch Linux:
```
yay -Sy
yay -S gthumb-openexr-extension
```
<br>


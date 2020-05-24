---
layout: page
title: 1 - Introduction
---

Using our visual system to scan a room, we can identify accessories and furniture. We can distinguish their colour, and categorise their texture without touching them:

*The surface of this bathtub looks smooth. This car paint is old and damaged, its shininess is uneven.*

All of these characteristics are given by materials’ reflectance: the way a material reflects the light conveys to our visual system a lot of information. We first rely on our visual system to name the material that compose an object.

We use computers to generate images of virtual scenes. It has many applications whether for entertainment (special effects, video games) or for more serious applications (virtual prototyping, cultural heritage...).

One key element for these applications is the photorealism of pictures: to improve realism, we need realistic materials. To get these, we rely on material acquisition. It comes at a cost. The procedure is tedious and requires special and expensive equipment. After acquisition, materials are difficult to edit. Finally, acquired materials use a significant amount of memory.

We want to represent real-world reflectance efficiently. Memory is a valuable resource and production scenes rely on many materials at the same time. Using directly measured materials is not an option. Edition is another important aspect for usability: artists need to get intuitive handles to tweak material appearance.

In this thesis, we propose techniques to reduce the memory footprint of measured materials while allowing edition. We also propose a method for fast acquisition of material in a non-critical context.

<figure>
    <div class="w3-row-padding">
        <figure class="w3-col m6 l6">
            <img src="/figures/intro/bathroom_diffuse.png" class="w3-card" />
            <figcaption>
                <strong>(a)</strong> A bathroom scene only with diffuse material coating every surfaces.
            </figcaption>
        </figure>
        <figure class="w3-col m6 l6">
            <img src="/figures/intro/bathroom.png" class="w3-card" />
            <figcaption>
                <strong>(b)</strong> The same scene with different materials.
            </figcaption>
        </figure>
    </div>
    <figcaption>
        <strong>Figure 1:</strong> Materials drastically change the appearance of a scene. This scene is modified from the PBRT renderer example scenes.
    </figcaption>
</figure>

Local and global effects
========================

#### Material and geometry

Light is scattered by surfaces. The material drives a part of the scattering. The surface geometry accounts for the other part. In this thesis, we use the “microfacet” model which models light scattering by micro mirrors at micro scale. We want to distinguish two scales of geometry:

- The observable geometry which is not part of the material model. It is the surface geometry and is independent of the material. We can observe this scale with bare eyes.

- The theoretical geometry. It is the root of the microfacet model later introduced. This is a mathematical construction to model light scattering by a material.

The hard limit we draw between those two geometries is arguable. Material models are already a simplification of light scattering. Is brushed aluminium an aluminium surface with valleys? The scratches being barely noticeable by naked eyes, we may consider it part of the material scattering. It will provide anisotropy property to the material reflectance. In fact, the limit between those two scales is blurry and a range of work is focusing on providing level of details depending on the distance of the observer to the surface.

When we are dealing with measured materials, we consider the sub-pixel effect to be material effects and effects occurring over the footprint of a pixel to be surface effects. The effects of geometry and material influence each other due to multiple scattering. When measuring reflectance, we measure the two effects combined. It is challenging to separate the two when analysing measured reflectance.

#### Influence of material on their surrounding

Materials affect not only the appearance of surfaces but also their surrounding: they reflect light on the neighbouring objects. Surfaces become secondary light sources when we compute global illumination. Figure [2](#fig:gi_example) features an example of global illumination. The indirect illumination takes a significant share in the overall appearance of a scene. It is determined by materials populating the scene.

<figure id="#fig:gi_example">
    <div class="w3-row-padding">
        <figure class="w3-col m4 l4">
            <img src="/figures/intro/PastedGraphic-2.jpg" class="w3-card" />
            <figcaption>
                <strong>(a)</strong> Direction illumination.
            </figcaption>
        </figure>
        <figure class="w3-col m4 l4">
            <img src="/figures/intro/PastedGraphic-1.jpg" class="w3-card" />
            <figcaption>
                <strong>(b)</strong> Indirect illumination.
            </figcaption>
        </figure>
        <figure class="w3-col m4 l4">
            <img src="/figures/intro/PastedGraphic-3.jpg" class="w3-card" />
            <figcaption>
                <strong>(c)</strong> Global illumination.
            </figcaption>
        </figure>
    </div>
    <figcaption>
        <strong>Figure 2:</strong> When materials reflect light, they become secondary light sources. Direct illumination (a) does not solely contributes to the overall appearance of the scene (c). The indirect illumination takes an important part to the overall appearance (b). With the same lighting and geometry, appearance of a scene can drastically change depending on materials coating the surfaces. Images courtesy of Cyril Soler.
    </figcaption>
</figure>


The importance of material in the overall appearance of a scene motivates our need for accurate reflectance.

Desirable material properties
=============================

#### Energy conservative

Accurate material reflectance is crucial for realism. One of the main properties a material representation shall verify is energy conservation: it shall not reflect more light than it received. We call the materials verifying this property *physically plausible*.

A more restrictive group base their representation on physical properties; we call them *physically based*. This does not mean they are perfectly modelling real-world; it means they are built upon a theoretical foundation following laws of physics.

*Physically based* materials are highly desirable in computer graphics when targeting photorealism.

#### Efficiency

Simulating light transport is a computationally intensive task. For both real time and offline rendering, materials efficient to evaluate are capital. Efficiency takes two necessary components:

- **Fast evaluation:** thousands of evaluations are required for a single pixel. When using stochastic methods, the property of guessing in which direction the light is most likely scattered is important as well. This is given by importance sampling. Fast evaluation and accurate importance sampling are both important.

- **Reduced memory footprint:** a scene uses multiple materials at once. We cannot afford very large materials. We need to fit the whole scene in fast memory for efficient light transport evaluation. Addressing large blocks of memory is also expensive and a potential bottleneck.

#### Edition

Computer graphics is used in a wide range of context. Artists are often involved. A material is at the heart of overall appearance. *Editability* is a valuable asset.

Not all materials offer the same ease for edition.

Material representations
========================

#### Homogeneous and spatially varying

A material in its most general form is spatially varying: wood shows varying grain (see Figure [3](#fig:wood_varying)), skin has a varying cellular and imperfection distribution. Some materials can be assumed to be homogeneous. A plastic, except potential manufacturing defects, keeps a constant reflectance across its surface.

<figure id="#fig:wood_varying">
    <div class="w3-row-padding">
        <figure class="w3-col m4 l4">
            <img src="/figures/intro/wood.JPG" class="w3-card" />
            <figcaption>
                <strong>(a)</strong> Wood is a spatially varying material.
            </figcaption>
        </figure>
        <figure class="w3-col m4 l4">
            <img src="/figures/intro/wall_detail.JPG" class="w3-card" />
            <figcaption>
                <strong>(b)</strong> Wall painting detail.
            </figcaption>
        </figure>
        <figure class="w3-col m4 l4">
            <img src="/figures/intro/microfiber_detail.JPG" class="w3-card" />
            <figcaption>
                <strong>(c)</strong> Microfiber towel detail.
            </figcaption>
        </figure>
    </div>
    <figcaption>
        <strong>Figure 3:</strong> Different types of materials and surfaces: wood (a) is spatially varying while the wall (b) has a uniform paint and the towel (c) is made of the same fibre but their geometry influences the surface appearance.
    </figcaption>
</figure>


#### Isotropic and anisotropic

An anisotropic material has a privileged reflection axis regardless illumination and observation. This is typically the case of brushed metals. It requires 4 dimensions to characterise its reflectance: both viewing and illumination elevations and azimuths.

An isotropic material has no such reflection pattern and can be characterised with 3 dimensions: the viewing and illumination elevations and the azimuths difference between the two.

#### Measured and analytic

To get realistic materials, acquisition is an appealing choice. The acquisition measure how light is reflected from multiple combination of illuminations and viewing directions. Editability and acquisition costs makes usage of measured data impractical and not always possible. For spatially varying materials, memory footprint is also a major issue.

Analytic models offer another approach to render materials. They are based on mathematical expressions with appearance driven by parameters. Those models are compact and efficient to evaluate. Although the parameters involved in analytic models are not always meaningful for a non-specialist relating to the physical underlying model used, they are accessible for edition.

While captured materials offer realism, physically based models express material appearance in a canonical fashion with a limited number of parameters. We want to represent a measured material by an analytic model to benefit from compactness, efficiency, and *editability*. This process is difficult: not all the reflectance properties are well modelled and approximations have to be made. These have to be convincing enough to be visually conclusive. In addition, acquisition errors have to be addressed when we want to fit to an analytic model.

Organisation of the manuscript
==============================

The manuscript is organised in two parts; the first part reviews the basic physical principles we use in the scope of this thesis for computer graphics.

Chapter [physics of light](physics_of_light):  
We introduce the physical nature of light and the quantities used to measure light radiation. We explain some of the properties of an electromagnetic wave which can have visual consequences when simulating light transport.

Chapter [human perception of colours](human_perception_of_colours):  
We introduce how our visual system interprets the light wavelengths as
colours. We motivate the utility of spectral rendering for accurate
simulation of light transport and colour accuracy.

Chapter <a href="#chapter:light_transport" data-reference-type="ref" data-reference="chapter:light_transport">[chapter:light_transport]</a>  
We explain how light is reflected on surfaces and give the basis of
material scattering models. We explain the basics of the microfacet
model.

Chapter <a href="#chapter:material_aquisition" data-reference-type="ref" data-reference="chapter:material_aquisition">[chapter:material_aquisition]</a>  
We overview and group material acquisition techniques proposed in the
literature.

We omit important points for the reader interested in implementing a
path tracer: we do not present rendering techniques, specific
acceleration structures for scene hierarchy, intersections or filtering
methods. We concentrate on the physical properties of materials and
their interaction with light.  
The second part aggregates my contributions in the direct scope of my
thesis.

Chapter <a href="#chapter:anisotropy" data-reference-type="ref" data-reference="chapter:anisotropy">[chapter:anisotropy]</a>  
We present a method for acquiring spatially varying anisotropic
materials. Our setup works with as few as twenty sample and is cheap and
simple to build. This work was presented at Graphics Interface 2016 in
Victoria, BC, Canada.

Chapter <a href="#chapter:btf_fit" data-reference-type="ref" data-reference="chapter:btf_fit">[chapter:btf_fit]</a>  
We describe a pipeline for fitting measured spatially varying materials
with editability in mind.

Chapter <a href="#chapter:eval_fit" data-reference-type="ref" data-reference="chapter:eval_fit">[chapter:eval_fit]</a>  
We evaluate the accuracy of our fitting method presented previously. We
explain the implication of acquisition sampling on material acquisition.

Chapter <a href="#chapter:combining_iso_aniso" data-reference-type="ref" data-reference="chapter:combining_iso_aniso">[chapter:combining_iso_aniso]</a>  
We introduce a technique for editing measured materials without
computing the underlying analytical model. We can mix material
properties from different datasets. For example, we can use the
shininess from one material and the anisotropy of another. Then, we can
edit each property independently.

Contributions and notions developed in the course of this thesis are
summarised at the end of the manuscript. We propose outlooks for
material acquisition and edition.

Collaboration
=============

I did a gap year in the Czech Republic at Charles University during my
PhD. I was under the supervision of Alexander Wilkie and Jaroslav
Křivánek. I have strengthened my knowledge on rendering during this
year. I have collaborated on an article for rendering fluorescence in a
path tracer, enabling the usage of Hero Wavelength Spectral Sampling
(HWSS) and participating media with fluorescence (Mojzík, Fichet, and
Wilkie 2018). We use parts of this article in this thesis to introduce
fluorescence in the context part. I chose not to include its core
contribution: I joined an ongoing project and was not at the initiative
of the idea. I have contributed to the project by writing rendering
code, debugging evaluating and writing part of the article.

During this year, I took part in the open source release of the long
time in house developed physically based rendered ART (The Advanced
Rendering Toolkit) which enables spectral path tracing with
polarisation, fluorescence, and HWSS support (“The Advanced Rendering
Toolkit” 2018).

Publications
============

Here is a list of the published work during my thesis.

-   Capturing Spatially Varying Anisotropic Reflectance Parameters using
    Fourier Analysis  
    **Alban Fichet**, Imari Sato, Nicolas Holzschuch (Fichet, Sato, and
    Holzschuch 2016)  
    *Graphics Interface Conference 2016, Jun 2016, Victoria, BC, Canada.
    pp.65 - 73, &lt;10.20380/GI2016.09&gt;*

-   Handling Fluorescence in a Uni-directional Spectral Path Tracer  
    Michal Mojzík, **Alban Fichet**, Alexander Wilkie (Mojzík, Fichet,
    and Wilkie 2018)  
    *Computer Graphics Forum, Wiley, 2018, 37 (4), pp.77 - 94.
    &lt;10.1111/cgf.13477&gt;*


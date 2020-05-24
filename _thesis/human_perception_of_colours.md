---
layout: page
title: 3. Human perception of colours
---

Human vision system is sensitive a certain range of frequencies. Radiations out of that range are not visible. In daylight, we perceive different colours depending on received spectral distribution: three types of cells in our retina are exited with different level.

Tristimulus is a mathematical basis for representing a mix of three primaries. It would seem a natural way of characterising reflectance and illumination: we use colour primaries in photography and cinema. We are familiar with red, green and blue, or cyan, magenta and yellow primaries.

But a colour or tristimulus value does not defines a unique spectrum: we can perceive multiple spectra as the same colour. This is called metamerism. This is not a concern for photography: we are interested by the image resulting of the physical transport of light. It reproduces what our eyes would see. It is however a concern for computer graphics where we simulate light transport.

In this chapter, we discuss the importance of spectral consideration for reflectance and illuminant in computer graphics.

The first section introduces photometric units and how spectra are perceived as colours. We show example of metamerism.

In the second section we compare tristimulus rendering with spectral rendering. We discuss the reasons for tristimulus wide adoption in computer graphics and motivate the need for a spectral rendering pipeline transition.

We need to characterise the energy distribution when simulating light transport. Using tristimulus values can lead to serious discrepancies. Light is reflected depending on its spectral distribution not depending on a set of primaries. Tristimulus values, and colour in particular, are perceptual concepts and mathematical framework resulting of physics and biology. They do not characterise a physical wavelength distribution.

Human vision and Tristimulus
============================

Photometry
----------

The retinas at the back of the human eye are composed by two different types of photosensitive cells, rods and cones. Both are used for vision, depending on lighting conditions.

-   **In bright environments, cone cells are active.** This is called
    *photopic vision*. The human eye have three types of cones sensitive
    to different frequencies; S for small-wavelength-sensitive, M for
    middle-wavelength-sensitive, L for long-wavelength-sensitive. This
    allows colour vision.

-   **In lower brightness conditions, rod cells are active**. This is
    called *scotopic vision*. Rod cells are more sensitive than cone
    cells. Rod cells share the same sensitivity range hence we are
    unable to distinguish colours in a darker environment.

Cone and rod cells having different sensitivity bandwidth, vision varies depending on lighting condition. This is described by the luminosity function (Figure [1](#fig:luminous_efficiency)) and varies depending on the lighting condition.


<figure id="fig:luminous_efficiency">
  <img src="/figures/human_perception_of_colours/plot/output/judd_vos_1978_photopic_CIE_1951_scotopic.svg"/>
  <figcaption>
    <strong>Figure 1:</strong> Depending on the lighting condition, the cones or the rods cells are active, resulting in our eyes having different sensitivity. Judd and Vos corrected photopic CIE 1924 \(V(\lambda)\) known as \(V_M(\lambda)\) \cite{judd1951,vos_colorimetric_1978} and CIE 1951 scotopic \(V(\lambda)\).
  </figcaption>
</figure>

We use photometric units quantities to describe how much of the light is perceived. It is an equivalent of radiometric units, characterising radiation, for perception (see Table bellow).

| Name               | Symbol     | Units                                                              | Radiometric equivalent |
| :----------------- | :--------: | :----------------------------------------------------------------- | :--------------------- |
| luminous flux      | $$\Phi_v$$ | lumen $$[\mathrm{lm}]$$                                            | radiant flux           |
| illuminance        | $$E_v$$    | lux $$[\mathrm{lx}]$$ i.e. $$[\mathrm{lm.m^{-2}}]$$                | irradiance             |
| luminous intensity | $$I_v$$    | candela $$[\mathrm{lm}]$$ i.e. $$[\mathrm{lm.sr^{-1}}]$$           | radiant intensity      |
| luninance          | $$L_v$$    | nits $$[\mathrm{cd.m^{-2}}]$$ i.e. $$[\mathrm{lm.m^{-2}.sr^{-1}}]$$| radiance               |

To convert from radiance $$L_e$$ to the luminance $$L_v$$, we use the following equation for photopic vision (daytime):

$$
\begin{equation}
    L_v = K_m \int_\Lambda L_e(\lambda) V_M(\lambda) \:\mathrm{d} \lambda \qquad [\mathrm{lm.m^{-2}.sr^{-1}}]
    \label{eqn:photopic}
\end{equation}
$$

With: $$K_m = 683 \mathrm{lm.W^{-1}}$$, the maximum luminous efficacy for photopic vision.

For scotopic vision (dim-light): 

$$
\begin{equation}
    L_v = K'_m \int_\Lambda L_e(\lambda) V(\lambda) \:\mathrm{d} \lambda \qquad [\mathrm{lm.m^{-2}.sr^{-1}}]
    \label{eqn:scotopic}
\end{equation}
$$
With: $$K_m = 1700 \mathrm{lm.W^{-1}}$$, the maximum luminous efficacy for scotopic vision.

We have to specify the luminous efficiency function corresponding to the
environment when we use a photometric unit.

Determining colour primaries
----------------------------

The theory of colour vision based on primaries started with Newton [[Newton 1704]](#ref-Newton1704). He stated that seven primaries (red, orange, yellow, green, blue, indigo and violet) can be mixed to reproduce any visible colours. He based his theory on the observation of the sun light dispersed by a prism. Later, mathematical and experimental foundation was refined by Young [[Young 1802b]](#ref-10.2307/107126), [[1802a]](#ref-10.2307/107113), Grassmann [[Grassmann 1853]](#ref-Grassmann1853) Helmholtz [[Helmholtz 1852]](#ref-Helmholtz1852) [[1855]](#ref-Helmholtz1855) and Maxwell [[Maxwell 1857]](#ref-maxwell_1857), [[1860]](#ref-10.2307/108759) with the theory of three primaries.

To determine the visual sensitivity to light, the <span lang="fr">*Commission Internationnale de l’Éclairage*</span> (CIE), conducted a series of experiments from 1920 to lead to the CIE 1931 XYZ colour space. The CIE 1931 $$2^{\circ}$$ colour matching functions (CMFs) are based on the CIE 1924 $$V(\lambda)$$ photopic luminosity function. This photopic luminosity function underestimate the importance of eye sensitivity below 460 nm. Stiles and Burch re-conduct the experiment to refine the CMFs among 10 observers for $$2^{\circ}$$ matching field [[Stiles and Burch 1955]](#ref-stiles_interim_1955) and for $$10^{\circ}$$ matching field [[Stiles and Burch 1959]](#ref-stiles_n.p.l._1959).

<figure id="fig:rgb_colour_matching">
  <img src="/figures/human_perception_of_colours/plot/output/rgb_2deg.svg"/>
  <figcaption>
    <strong>Figure 2:</strong> Stiles and Burch RGB colour matching functions for 2\(^{\circ}\) observer <a href="#ref-stiles_interim_1955">[Stiles and Burch 1955]</a>. These are not emission spectra. Those curves describe the knob's positions for the three monochromatic illuminants used in the experiment (represented by the arrows) to match a specific monochromatic stimulus.
  </figcaption>
</figure>

An observer was facing a screen with two patches of light and a series of three knobs. One patch, the reference, is made of a monochromatic light and the observer have to manipulate the knobs controlling the amount of three primaries of almost monochromatic lights to match the colour of the second patch with the reference ($$r = 648.6\:\mathrm{nm}$$, $$g = 526.4\:\mathrm{nm}$$, $$b = 445.3\:\mathrm{nm}$$ in the CIE 1931, $$r = 645.2\:\mathrm{nm}$$, $$g = 526.3\:\mathrm{nm}$$, $$b = 444.4\:\mathrm{nm}$$ in (Stiles and Burch 1955, 1959)). To match some colours, *negative* values have to be used for the knobs. A negative position on the knob is simulated by adding the corresponding opposite value to the reference patch. Figure [2](#fig:rgb_colour_matching) shows the resulting curves for the colour-matching function.

<figure id="fig:xyz_2006">
  <img src="/figures/human_perception_of_colours/plot/output/xyz_2006_2deg.svg"/>
  <figcaption>
    <strong>Figure 3:</strong> CIE 2006 XYZ 2\(^{\circ}\) observer colour space based from LMS fundamentals from <a href="#ref-Stockman2000">[Stockman2000]</a>. \(\bar{y}(\lambda)\) corresponds to \(V_M(\lambda)\) the luminous efficiency for photopic vision.
  </figcaption>
</figure>

To overcome the problem of having negative RGB coordinates, the CIE proposed the CIE 1931 $$2^{\circ}$$ XYZ colour space. Similar to Stiles and Burch RGB corrected visibility function for $$V(\lambda)$$ below 460nm, Judd [[Judd 1951]](#ref-judd1951) and later Vos [[Vos 1978]](#ref-vos_colorimetric_1978) proposed a correction for CIE 1931 $$2^{\circ}$$ XYZ. More recently, the CIE released CIE 2006 XYZ colour matching functions based on cone fundamentals from Stockman and Sharpe [[Stockman and Sharpe 2000]](#ref-Stockman2000) (see Figure [3](#fig:xyz_2006)).

Reflectance and colours
-----------------------

<figure id="fig:macbeth_colours">
<div markdown="1">

|         | D65                                                                        | FL4                                                                        | A                                                                       |
| :-----: | :------------------------------------------------------------------------: | :------------------------------------------------------------------------: | :---------------------------------------------------------------------: |
| SPD     | ![](/figures/human_perception_of_colours/plot/output/spd_d65.svg)          | ![](/figures/human_perception_of_colours/plot/output/spd_fl4.svg)          | ![](/figures/human_perception_of_colours/plot/output/spd_a.svg)         |
| Macbeth | ![](/figures/human_perception_of_colours/illus/perception/macbeth_D65.png) | ![](/figures/human_perception_of_colours/illus/perception/macbeth_FL4.png) |![](/figures/human_perception_of_colours/illus/perception/macbeth_A.png) |

</div>
    <figcaption>
        <strong>Figure 4:</strong> A Macbeth colour checker lit under different illuminants: CIE D65 (average midday in Western Europe), FL4 (fluorescent lighting), and A (typical, domestic, tungsten-filament lighting). The perceived colour varies drastically depending on the illuminant used.
    </figcaption>
</figure>

When characterising a reflectance by its colour, it is important to also specify under which illuminant it is observed. For example, Figure [4](#fig:macbeth_colours) shows a Macbeth colour checker lit by different illuminants. The illuminant used to lit the scene drastically influences the perceived colours of the patches. Under D65, some patches appear blue while they are looking violet under fluorescent illuminant FL4.

From spectra to tristimulus
---------------------------

To transform a spectra into a perceived colour, we use colour matching functions. Usually, we first transform spectra to XYZ coordinates. Then, we transform XYZ coordinates to a specific colour space depending on the targeted application.

In computer graphics, we typically display an image on a 8bit RGB monitor. We transform XYZ to RGB values, then gamma correct to sRGB.

### Radiance

To get XYZ coordinates of a radiance spectrum, we multiply and integrate the spectral radiance with the colour matching functions: 

$$
\begin{aligned}
    \begin{cases}
        \displaystyle X = \int_\Lambda L_e(\lambda) \bar{x}(\lambda) \:\mathrm{d} \lambda\\
        \displaystyle Y = \int_\Lambda L_e(\lambda) \bar{y}(\lambda) \:\mathrm{d} \lambda\\
        \displaystyle Z = \int_\Lambda L_e(\lambda) \bar{z}(\lambda) \:\mathrm{d} \lambda
    \end{cases}
\end{aligned}
$$

Notice from equation \eqref{eqn:photopic}, the luminance can be retrieved from the $$Y$$ component in photopic conditions by multiplying it with the corresponding $$K_m$$.

### Reflectance

We mentioned in section [1.3](#sec:reflectance_and_colours) the perceived colour of reflectance depends on the illumination under which it is observed. Then, we specify XYZ coordinates of a reflectance relative to an illuminant: 

$$
\begin{aligned}
    &\begin{cases}
        \displaystyle X = \frac{1}{N}\int_\Lambda s(\lambda) L_e(\lambda) \bar{x}(\lambda) \:\mathrm{d} \lambda \\
        \displaystyle Y = \frac{1}{N}\int_\Lambda s(\lambda) L_e(\lambda) \bar{y}(\lambda) \:\mathrm{d} \lambda \\
        \displaystyle Z = \frac{1}{N}\int_\Lambda s(\lambda) L_e(\lambda) \bar{z}(\lambda) \:\mathrm{d} \lambda
    \end{cases}
\end{aligned}
$$
    
With $$N = \int_\Lambda L_e(\lambda) \bar{y}(\lambda) \:\mathrm{d} \lambda$$.  

Where:
- $$L_e(\lambda)$$ is the spectral radiance of the illuminant.
- $$s(\lambda)$$ is the spectral reflectance.


Metamerism
----------

A spectrum defines a colour, but a colour does not define an unique spectra: multiple spectra can lead to the observation of the same colour due to the way humans perceive colours. In mathematical terms, there is a surjection between spectra and colours.

<figure id="fig:metamer_comparison">
  <figure>
    <img src="/figures/human_perception_of_colours/plot/output/metamerism.svg" />
    <figcaption>
      <strong>(a)</strong> Two metamer reflectances under HP1 illuminant
    </figcaption>
  </figure>
  <figure>
    <div>
      <table>
      <thead>
        <tr>
          <td></td>
          <td colspan="2" style="text-align:center"><strong>HP1</strong></td>
          <td colspan="2" style="text-align:center"><strong>D65</strong></td>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>SPD</td>
          <td colspan="2"><img src="/figures/human_perception_of_colours/plot/output/spd_hp1.svg" /></td>
          <td colspan="2"><img src="/figures/human_perception_of_colours/plot/output/spd_d65.svg" /></td>
        </tr>
        <tr>
          <td></td>
          <td style="text-align:center"><strong>Original</strong></td>
          <td style="text-align:center"><strong>Metamer</strong></td>
          <td style="text-align:center"><strong>Original</strong></td>
          <td style="text-align:center"><strong>Metamer</strong></td>
        </tr>
        <tr>
          <td>Colour patches</td>
          <td width="22%"><img src="/figures/human_perception_of_colours/illus/original_HP1_0.png" width="100%" /></td>
          <td width="22%"><img src="/figures/human_perception_of_colours/illus/metamer_HP1_0.png" width="100%" /></td>
          <td width="22%"><img src="/figures/human_perception_of_colours/illus/original_D65_0.png" width="100%" /></td>
          <td width="22%"><img src="/figures/human_perception_of_colours/illus/metamer_D65_0.png" width="100%" /></td>
        </tr>
      </tbody>
      </table>
    </div>
    <figcaption>
      <strong>(b)</strong> The metamer reflectances shown under HP1 and under D65 illuminants.
    </figcaption>
  </figure>
  <figcaption>
    <strong>Figure 5:</strong> We generate a metamer reflectance for HP1 illuminant. While the two spectra are very different, the perceived colour is exactly the same under this illuminant. When using CIE D65 illuminant, we can distinguish the colours.
  </figcaption>
</figure>

While some patches have a clear colours difference in Figure [4](#fig:macbeth_colours) under D65 (green and yellow), it is much harder to see the difference between the same patches under FL4 or A illuminants. The extreme cases is when two different reflectance spectra appears the same under a given illuminant. They are then called metamers under this illuminant. When changing illuminant, the difference between the reflectance may appear.

<figure id="fig:metamer_real">
  <div class="w3-row-padding">
    <figure class="w3-col m3 l3">
      <img src="/figures/human_perception_of_colours/illus/metamer/DSF0031.jpg" class="w3-card" />
      <figcaption>
          <strong>(a)</strong> Fluorescent light
      </figcaption>
    </figure>
    <figure class="w3-col m3 l3">
      <img src="/figures/human_perception_of_colours/illus/metamer/DSF0032.jpg" class="w3-card" />
      <figcaption>
          <strong>(b)</strong> Red (R) LED
      </figcaption>
    </figure>
    <figure class="w3-col m3 l3">
      <img src="/figures/human_perception_of_colours/illus/metamer/DSF0033.jpg" class="w3-card" />
      <figcaption>
          <strong>(c)</strong> Green (G) LED
      </figcaption>
    </figure>
    <figure class="w3-col m3 l3">
      <img src="/figures/human_perception_of_colours/illus/metamer/DSF0034.jpg" class="w3-card" />
      <figcaption>
          <strong>(d)</strong> Blue (B) LED
      </figcaption>
    </figure>
    <figure class="w3-col m3 l3">
      <img src="/figures/human_perception_of_colours/illus/metamer/DSF0038.jpg" class="w3-card" />
      <figcaption>
          <strong>(e)</strong> R+G+B LEDs
      </figcaption>
    </figure>
    <figure class="w3-col m3 l3">
      <img src="/figures/human_perception_of_colours/illus/metamer/DSF0035.jpg" class="w3-card" />
      <figcaption>
          <strong>(f)</strong> R+G LEDs
      </figcaption>
    </figure>
    <figure class="w3-col m3 l3">
      <img src="/figures/human_perception_of_colours/illus/metamer/DSF0036.jpg" class="w3-card" />
      <figcaption>
          <strong>(g)</strong> G+B LEDs
      </figcaption>
    </figure>
    <figure class="w3-col m3 l3">
      <img src="/figures/human_perception_of_colours/illus/metamer/DSF0037.jpg" class="w3-card" />
      <figcaption>
          <strong>(h)</strong> R+B LEDs
      </figcaption>
    </figure>
  </div>
  <figcaption>
    <strong>Figure 6:</strong> Painted artwork lit with different lightsources. It is impossible to distinguish colours when lit with almost monochromatic coloured LED (b) (c) (d), each reflectance reemitting shades of the same colour, the paint not being fluorescent. With the three LEDs combined (e), we can better make the difference. Althought white and yellow are hardly the same while easily separable with the fluorescent lighting (a). If only two LEDs are used,some colours are impossible to distinguish while being very different. For instance, with red and blue lighting (h), yellow and red (on the fish's tail) look very similar.
  </figcaption>
</figure>

In practice, metamers can easily appear when two surfaces are lit with purely monochromatic light. If the surface is not fluorescent, it only reflects the incoming wavelength (see Figure [6](#fig:metamer_real)). This is typically the case with street lighting using low pressure sodium-vapour lamps which are nearly monochromatic.

Figure [5](#fig:metamer_comparison) shows a example of two metamers for a given illuminant. One reflectance is taken from one of the Macbeth colour checker. The second reflectance is synthetically generated to produce the same perceived colour under HP1 illuminant.

Spectral and tristimulus pipelines
==================================

A colour does not properly define an illuminant or a reflectance due to metamerism. Still, many rendering pipelines rely on tristimulus values, whether renderers, or softwares used by artists to edit textures, for multiple reasons:

  - Efficiency  
    In the early days, with limited computational resources, the exclusive usage of tristimulus values enabled producing colour images with reasonable compromise on accuracy. A consequence of this long-term usage is the knowledge acquired on weaknesses and drawbacks of the tristimulus pipeline.

  - Transition  
    From a software point of view, moving from a tristimulus to a spectral workflow would imply an important codebase adaptation. Years of development resulted in software working correctly in tristimulus with known weaknesses. Transitioning to spectral would potentially break many features.

  - Intuitiveness  
    For artists, it is no easy task to switch from colours to spectra paradigm, the latter being far less intuitive to work with.

Tristimulus renderers are approximative. In some circumstances, they produce images very different from what a real scene would look like. This is especially problematic for prototyping applications. An architect or a car manufacturer could have misleading information about the appearance of paints depending on lighting conditions.

In the following sections we review some of the approximations caused by tristimulus rendering.


The core approximation of a tristimulus renderer
------------------------------------------------

In a spectral renderer, we treat each wavelength independently. We transform to tristimulus values only at the end of the evaluation. Each reflectance and illuminant have then to be specified as a spectrum.

In a tristimulus renderer, we treat each reflectance and illuminant as tristimulus values and multiply them. The integration transforming the spectra to tristimulus values is applied prior to the evaluation. In practice, the values are directly provided in XYZ or RGB and multiplied with each other.

Equation \eqref{eqn:approx_tristimulus} shows the core approximation made by a tristimulus renderer[^1]. In this equation, we apply a normalisation factor to the illuminant. This results in a correct result only in the case of single bounce if the illuminant we use to lit the scene match the one we use for reflectance tristimulus values. In practice, the need for this correction factor is arguable:

  - If the illuminant is seen directly, this leads to incorrect colour result.

  - While getting accurate results in single bounce and same illuminant scenario, when changing illuminant, it can cause more discrepancies.

  - In a multiple bounce scenario, each element reflecting in the scene would act as a secondary light source. The re-normalisation factor is unpredictable and can increase the error.

$$
\begin{align}
    \underbrace{
    \int_\Lambda r(\lambda) L_e(\lambda) \bar{c}(\lambda) \mathrm{d} \lambda}_{\text{Spectral rendering}} 
&\approx
\underbrace{
    \overbrace{\left(\frac{1}{N_m}
        \int_\Lambda r(\lambda) L^m_e(\lambda) \bar{c}(\lambda) \mathrm{d} \lambda
        \right)}^{\text{Tristimulus reflectance}} 
    \cdot 
    \overbrace{\left(N_m\frac
        {\int_\Lambda L_e(\lambda) \bar{c}(\lambda) \mathrm{d} \lambda}
        {\int_\Lambda L^m_e(\lambda) \bar{c}(\lambda) \mathrm{d} \lambda}
        \right)}^{\text{Tristimulus illuminant}}}_{\text{Tristimulus rendering}}
    \label{eqn:approx_tristimulus}\\
    &N_m = \int_\Lambda L^m_e(\lambda) \bar{y}(\lambda) \mathrm{d} \lambda
\end{align}
$$

Where:
- $$r(\lambda)$$ is the spectral reflectance.
- $$L_e(\lambda)$$ is the spectral power distribution of the illuminant for rendering.
- $$L^m_e(\lambda)$$ is the spectral power distribution of the illuminant for measuring reflectance.
- $$\bar{c}(\lambda)$$ is one of the colour matching functions $(\bar{x}, \bar{y}, \bar{z})$.



Comparing spectral and tristimulus rendering
--------------------------------------------

We evaluate the approximation made by a tristimulus rendering pipeline influences the final appearance. We compare both methods:

1.  In a single bounce context with variation of reflectance and illuminant. We use the Macbeth colour checker as the base collection of reflectance. Each patch is specified as a reflectance spectra. We show:
    
    1.  Colour discrepancies when using a different illuminant than the one used for measurement,
    
    2.  Limitations of tristimulus rendering threw reflectance and illuminant metamers.

2.  In a global illumination context we show:
    
    1.  Energy conservation problems rising with tristimulus rendering with generated spectra,
    
    2.  Error accumulation after multiple bounces in a Cornell box,
    
    3.  Discrepancies depending on the colour matching function used for representing illuminant and reflectance.

### Single bounce

#### Reflectance rendering under different illuminants

The illuminant influences the perceived colour of a reflectance. Figure [7](#fig:rendering_spectral_tristimulus) shows the impact of the pre-integration made in a tristimulus renderer on the colour accuracy using three different illuminants:

  - D65  
    is from the CIE series of daylight illuminants. This illuminant represent the average daylight illumination in Western Europe. Its spectral power distribution is well distributed and provides good ability for distinguishing colours.

  - FL4  
    is from the CIE series of fluorescent illuminants. Also called F4, this illuminant corresponds to a fluorescent lighting. The CIE used FL4 for colour rendering index calibration. It has two peaks around 410 nm and 435 nm and a larger emission band from 520 nm to 650 nm.

  - HP1  
    illuminant corresponds to a high-pressure vapour lamp. It has a narrow emission band roughly from 550 nm to 620 nm. It is difficult to differentiate colours under this illuminant.

For tristimulus rendering, we convert each patch of the colour checker to XYZ values as they would be measured under a given illuminant (here CIE D65). We convert the illuminant to XYZ values and correct it to match the measurement illuminant. We multiply the two XYZ sets together.

<figure id="fig:rendering_spectral_tristimulus">
  <div markdown="1">

|      | Spectral rendering | Tristimulus rendering | $$\Delta E^*_{2000}$$ |
| :--- | :----------------: | :-------------------: | :-------------------: |
| D65  | ![](/figures/human_perception_of_colours/illus/spectral/macbeth_spectral_D65.png) | ![](/figures/human_perception_of_colours/illus/spectral/macbeth_xyz_corrected_D65.png) | ![](/figures/human_perception_of_colours/illus/spectral/macbeth_deltaE_corrected_D65.png) |
|      | a | b | $$\Delta E^*_{2000}(a, b)$$ |
| FL4  | ![](/figures/human_perception_of_colours/illus/spectral/macbeth_spectral_FL4.png) | ![](/figures/human_perception_of_colours/illus/spectral/macbeth_xyz_corrected_FL4.png) | ![](/figures/human_perception_of_colours/illus/spectral/macbeth_deltaE_corrected_FL4.png) |
|      | a' | b' | $$\Delta E^*_{2000}(a', b')$$ |
| HP1  | ![](/figures/human_perception_of_colours/illus/spectral/macbeth_spectral_HP1.png) | ![](/figures/human_perception_of_colours/illus/spectral/macbeth_xyz_corrected_HP1.png) | ![](/figures/human_perception_of_colours/illus/spectral/macbeth_deltaE_corrected_HP1.png) |
|      | a'' | b'' | $$\Delta E^*_{2000}(a'', b'')$$ |

  </div>
  <figcaption>
    <strong>Figure 7:</strong> Comparison of spectral and tristimulus rendering. When using spectral rendering, we transform the colours from spectra to RGB at the end. With tristimulus rendering, we transform both reflectance and illuminants into their tristimulus counterparts prior to the evaluation. Then, we compute the final colour by multiplying illuminant and reflectance colour together. This approximation yields to observable differences as shown by the \(\Delta E^*_{2000}\) metric.
  </figcaption>
</figure>

  - With D65, the illuminant matches the one used for measuring the reflectance, the tristimulus rendering is exact. This is expected since the integration is made during the measurement and then a simple scaling is applied depending on the relative power of the illuminant used for rendering.

  - With FL4, the error increase for the coloured patches. When reflectance spectrum have its most reflectivity in values within the re-radiation band of the FL4 illuminant ($$520\sim 630\:\mathrm{nm}$$), it can be well represented with a tristimulus renderer. The fluorescent lamp also have an emission peak around $$400\:\mathrm{nm}$$ and around $$440\:\mathrm{nm}$$. Those two peaks are going to misrepresented: mostly X and Z values are affected. Those two functions have a much larger bandwidth than the emission peaks. This explains the poor rendering accuracy of the blue part of the spectrum.

  - This high frequency phenomena is even more pronounced with HP1 illuminant: the emission band is narrow and cannot be well represented by multiplications with XYZ values.

  - The grey reflectance, on the bottom line, have good rendering accuracy in a tristimulus renderer. Their reflectance spectrum is almost constant. This limited dependence to wavelength explains the good rendering results regardless the illuminant used.

In conclusion, the error caused by a tristimulus renderer is limited when we have low frequency illuminant or reflectance spectra.

#### Reflectance metamers

A tristimulus renderer will not handle reflectance metamers. When observed under another illuminant, the reflectance will appear identical while they should differ according to their reflectance spectra: the same XYZ values are used in both cases even if reflectance spectra differs.

<figure id="fig:metamer_reflectance_comparison">
  <table>
      <tr>
        <td></td>
        <td style="text-align:center"><strong>Original</strong></td>
        <td style="text-align:center"><strong>Metamers</strong></td>
        <td style="text-align:center">\(\Delta E^*_{2000}\)</td>
      </tr>
      <tr>
        <td>Spectral</td>
        <td width="30%"><img src="/figures/human_perception_of_colours/illus/reflectance/macbeth_refl_HP1_spectral.png" /></td>
        <td width="30%"><img src="/figures/human_perception_of_colours/illus/reflectance/macbeth_refl_metamer_HP1_spectral.png" /></td>
        <td width="30%"><img src="/figures/human_perception_of_colours/illus/reflectance/macbeth_deltaE_refl_HP1_spectral.png" /></td>
      </tr>
      <tr>
        <td></td>
        <td style="text-align:center">a</td>
        <td style="text-align:center">b</td>
        <td style="text-align:center">\(\Delta E^*_{2000}(a, b)\)</td>
      </tr>
      <tr>
        <td>Tristimulus</td>
        <td width="30%"><img src="/figures/human_perception_of_colours/illus/reflectance/macbeth_refl_HP1_xyz.png" /></td>
        <td width="30%"><img src="/figures/human_perception_of_colours/illus/reflectance/macbeth_refl_metamer_HP1_xyz.png" /></td>
        <td width="30%"><img src="/figures/human_perception_of_colours/illus/reflectance/macbeth_deltaE_refl_HP1_xyz.png" /></td>
      </tr>
      <tr>
        <td></td>
        <td style="text-align:center">a'</td>
        <td style="text-align:center">b'</td>
        <td style="text-align:center">\(\Delta E^*_{2000}(a', b')\)</td>
      </tr>
  </table>
  <figcaption>
    <strong>Figure 8:</strong> For each patch of the Macbeth colour checker, we generate a reflectance metamer for D65, then illuminate with HP1. When using a tristimulus renderer, the XYZ values are the same for both reflectance spectra of a given patch. Only a spectral renderer is able to show the colour difference with a suitable illuminant.
  </figcaption>
</figure>


Figure [8](#fig:metamer_reflectance_comparison) shows an example of two colour checkers. One is the original Macbeth colour checker. For the other, we replaced each of its patches by a metamer reflectance under an illuminant with a flat SPD. Only a spectral renderer accurately shows the difference between the two colour checkers depending on the illuminant.

#### Illuminant metamers

Similarly to metamer reflectance, we can generate metamer illuminant. If the illuminant is reflected by a perfectly grey surface (constant reflectance regardless the wavelength), the surface will appear the same to our eyes with both illuminants even though their emission spectra differ. Other reflectance are going to look different.


<figure id="fig:metamer_illuminant_comparison">
  <figure>
    <img src="/figures/human_perception_of_colours/plot/output/metamerism_illu.svg" />
    <figcaption>
      <strong>(a)</strong> Two illuminant metamers
    </figcaption>
  </figure>
  <figure>
    <div>
      <table>
        <thead>
          <tr>
            <td></td>
            <td style="text-align:center"><strong>D65</strong></td>
            <td style="text-align:center"><strong>D65 metamer</strong></td>
            <td style="text-align:center">\(\Delta E^*_{2000}\)</td>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td>Spectral</td>
            <td width="30%"><img src="/figures/human_perception_of_colours/illus/illumination/macbeth_illu_D65_spectral.png" /></td>
            <td width="30%"><img src="/figures/human_perception_of_colours/illus/illumination/macbeth_illu_D65_metamer_spectral.png" /></td>
            <td width="30%"><img src="/figures/human_perception_of_colours/illus/illumination/macbeth_deltaE_illu_D65_spectral.png" /></td>
          </tr>
          <tr>
            <td></td>
            <td style="text-align:center">a</td>
            <td style="text-align:center">b</td>
            <td style="text-align:center">\(\Delta E^*_{2000}(a, b)\)</td>
          </tr>
          <tr>
            <td>Tristimulus</td>
            <td width="30%"><img src="/figures/human_perception_of_colours/illus/illumination/macbeth_illu_D65_xyz.png" /></td>
            <td width="30%"><img src="/figures/human_perception_of_colours/illus/illumination/macbeth_illu_D65_metamer_xyz.png" /></td>
            <td width="30%"><img src="/figures/human_perception_of_colours/illus/illumination/macbeth_deltaE_illu_D65_xyz.png" /></td>
          </tr>
          <tr>
            <td></td>
            <td style="text-align:center">a'</td>
            <td style="text-align:center">b'</td>
            <td style="text-align:center">\(\Delta E^*_{2000}(a', b')\)</td>
          </tr>
        </tbody>
      </table>
    </div>
    <figcaption>
      <strong>(b)</strong> Macbeth colour checker lit by the two illuminants.
    </figcaption>
  </figure>
  <figcaption>
    <strong>Figure 9:</strong> We generate a metamer illuminant from D65. If illuminating a perfect grey albedo (reflecting equally all the wavelengths) with the two illuminants our eyes see the same reflected colour. Other reflectance spectra will look different. Contrary to a tristimulus renderer, a spectral renderer can show the colour difference.
  </figcaption>
</figure>

In Figure [9](#fig:metamer_illuminant_comparison) we show a such scenario. We generate a metamer illuminant for D65. We then compare the Macbeth colour checker lit by the original D65 illuminant and its metamer.

  - With a spectral rendering, the patches have a different colour from one illuminant to the other. This is expected: the illuminants have different spectral power distributions.

  - With a tristimulus rendering, there is no difference when changing illuminant. The two metamer illuminants are transformed to the same XYZ values prior to the rendering.

Only a spectral renderer with spectral reflectance can handle metamer illuminants.

### Global illumination

Global illumination increases the discrepancies exposed before. At each new reflection bounce event, a tristimulus renderer accumulates error.

Even if we specify all reflectance using the illuminant in the scene, each light bounce step is equivalent to a new illuminant radiating the next reflectance. This yields to incorrect results and breaks energy conservation, starting from the second light bounce.

#### Energy conservation

To illustrate the potential loss and creation of energy caused by a tristimulus renderer, we generate two synthetic cases:

  - In the first (see Figure [10.a](#fig:energy_loss)), we simulate scattering from D65 illuminant to a patch and a second bounce from this first patch to another one having the same reflectance. The reflectance is perfectly reflecting the light between 440 nm and 550 nm. Otherwise, the light is absorbed. We observe a loss of energy in the case of a tristimulus renderer: the XYZ components of the reflectance cannot reflect the nature of the spectra.

  - In the second (see Figure [10.b](#fig:energy_creation)), we use the first spectrum as the one used before. For the second bounce, we use a complementary spectrum: its reflectance is null at the value where the other spectrum reflects and perfectly reflective where the other absorbs light. We observe creation of energy in the case of a tristimulus renderer: not null XYZ values are multiplied together.

We do not attenuate the light depending on its angle nor considering the distance: we are only interested in showing the absence of energy conservation caused by the multiplication of XYZ values instead of spectra.

<figure>
  <div class="w3-row-padding">
    <figure class="w3-col m6 l6" id="fig:energy_loss">
      <table>
        <tr>
          <td width="50%" style="text-align:center"><strong>Reflectance A</strong></td>
          <td width="50%" style="text-align:center"><strong>Reflectance B</strong></td>
        </tr>
        <tr>
          <td><img src="/figures/human_perception_of_colours/plot/output/spectrum_create_a.svg" width="100%" /></td>
          <td><img src="/figures/human_perception_of_colours/plot/output/spectrum_create_a.svg" width="100%" /></td>
        </tr>
        <tr>
          <td><img src="/figures/human_perception_of_colours/illus/energy/loss_spectral_a.png" width="100%" /></td>
          <td><img src="/figures/human_perception_of_colours/illus/energy/loss_spectral_a.png" width="100%" /></td>
        </tr>
        <tr>
          <td colspan="2" style="text-align:center"><strong>Tristimulus renderer</strong></td>
        </tr>
        <tr>
          <td><img src="/figures/human_perception_of_colours/illus/energy/loss_xyz_a.png" width="100%" /></td>
          <td><img src="/figures/human_perception_of_colours/illus/energy/loss_xyz.png" width="100%" /></td>
        </tr>
        <tr>
          <td colspan="2" style="text-align:center"><strong>Spectral renderer</strong></td>
        </tr>
        <tr>
          <td><img src="/figures/human_perception_of_colours/illus/energy/loss_spectral_a.png" width="100%" /></td>
          <td><img src="/figures/human_perception_of_colours/illus/energy/loss_spectral.png" width="100%" /></td>
        </tr>
      </table>
      <figcaption>
        <strong>(a)</strong> Loss of energy caused by a tristimulus renderer. While the two spectra shall reflect 100% of the light between 440 nm and 550 nm, the conversion to XYZ makes the second bounce multiplied by numbers inferior to 1 causing a loss of energy.
      </figcaption>
    </figure>
    <figure class="w3-col m6 l6" id="fig:energy_creation">
      <table>
        <tr>
          <td width="50%" style="text-align:center"><strong>Reflectance A</strong></td>
          <td width="50%" style="text-align:center"><strong>Reflectance B</strong></td>
        </tr>
        <tr>
          <td><img src="/figures/human_perception_of_colours/plot/output/spectrum_create_a.svg" width="100%" /></td>
          <td><img src="/figures/human_perception_of_colours/plot/output/spectrum_create_b.svg" width="100%" /></td>
        </tr>
        <tr>
          <td><img src="/figures/human_perception_of_colours/illus/energy/create_spectral_a.png" width="100%" /></td>
          <td><img src="/figures/human_perception_of_colours/illus/energy/create_spectral_b.png" width="100%" /></td>
        </tr>
        <tr>
          <td colspan="2" style="text-align:center"><strong>Tristimulus renderer</strong></td>
        </tr>
        <tr>
          <td><img src="/figures/human_perception_of_colours/illus/energy/create_xyz_a.png" width="100%" /></td>
          <td><img src="/figures/human_perception_of_colours/illus/energy/create_xyz.png" width="100%" /></td>
        </tr>
        <tr>
          <td colspan="2" style="text-align:center"><strong>Spectral renderer</strong></td>
        </tr>
        <tr>
          <td><img src="/figures/human_perception_of_colours/illus/energy/create_spectral_a.png" width="100%" /></td>
          <td><img src="/figures/human_perception_of_colours/illus/energy/create_spectral.png" width="100%" /></td>
        </tr>
      </table>
      <figcaption>
        <strong>(b)</strong> Creation of energy caused by a tristimulus renderer. The two spectra are complementary to each other. What is reflected by reflectance A is absorbed by reflectance B. This shall lead to no energy scattered after the second bounce. This time, both XYZ reflectances are superior to zero causing energy creation.
      </figcaption>
    </figure>
  </div>
  <figcaption>
    <strong>Figure 10:</strong> Comparing scattered light colour after two bounces with a tristimulus and spectral renderers using a CIE D65 illuminant. The corresponding XYZ values are in the bottom left of each patch.
  </figcaption>
</figure>

#### Cornell box example

To show a practical example of discrepancies observable with a simple scene, we use the Cornell box rendered with Mitsuba [[Jakob 2010]](#ref-Jakob2010). The spectral variant is using 30 spectral samples while the tristimulus variant is converting all spectra to RGB prior to light transport.

<figure id="fig:gi_spectral">
  <table>
      <tr>
        <td></td>
        <td style="text-align:center"><strong>Spectral</strong></td>
        <td style="text-align:center"><strong>RGB</strong></td>
        <td style="text-align:center">\(\Delta E^*_{2000}\)</td>
      </tr>
      <tr>
        <td>Spectral</td>
        <td width="30%"><img src="/figures/human_perception_of_colours/illus/gi/cbox_cornell_30.png" /></td>
        <td width="30%"><img src="/figures/human_perception_of_colours/illus/gi/cbox_cornell_rgb.png" /></td>
        <td width="30%"><img src="/figures/human_perception_of_colours/illus/gi/cbox_cornell_deltaE.png" /></td>
      </tr>
      <tr>
        <td></td>
        <td style="text-align:center">a</td>
        <td style="text-align:center">b</td>
        <td style="text-align:center">\(\Delta E^*_{2000}(a, b)\)</td>
      </tr>
      <tr>
        <td>Tristimulus</td>
        <td width="30%"><img src="/figures/human_perception_of_colours/illus/gi/cbox_hp1_30.png" /></td>
        <td width="30%"><img src="/figures/human_perception_of_colours/illus/gi/cbox_hp1_rgb.png" /></td>
        <td width="30%"><img src="/figures/human_perception_of_colours/illus/gi/cbox_hp1_deltaE.png" /></td>
      </tr>
      <tr>
        <td></td>
        <td style="text-align:center">a'</td>
        <td style="text-align:center">b'</td>
        <td style="text-align:center">\(\Delta E^*_{2000}(a', b')\)</td>
      </tr>
  </table>
  <figcaption>
    <strong>Figure 11:</strong> Rendering of a Cornell box with Mitsuba using 30 spectral samples and RGB rendering modes. We observe significant differences between the two rendering methods.
  </figcaption>
</figure>


The appearance drastically change if using tristimulus values instead of the full spectrum for rendering (see Figure [11](#fig:gi_spectral)).

For the same input spectra, the colour matching functions used in a tristimulus renderer can also drastically change the appearance of the output image (see Figure [12](#fig:gi_cmfs))).

The error would significantly increase with multiple light sources having different spectra.

<figure id="fig:gi_cmfs">
  <div class="w3-row-padding">
    <figure class="w3-col m4 l4">
      <img src="/figures/human_perception_of_colours/illus/cornell/spectral_hp1.png" class="w3-card" />
      <figcaption>
          <strong>(a)</strong> Spectral rendering.
      </figcaption>
    </figure>
    <figure class="w3-col m4 l4">
      <img src="/figures/human_perception_of_colours/illus/cornell/xyz_hp1.png" class="w3-card" />
      <figcaption>
          <strong>(b)</strong> CIE XYZ 2006 colour matching functions.
      </figcaption>
    </figure>
    <figure class="w3-col m4 l4">
      <img src="/figures/human_perception_of_colours/illus/cornell/rgb_hp1.png" class="w3-card" />
      <figcaption>
          <strong>(c)</strong> RGB colour matching functions.
      </figcaption>
    </figure>
  </div>
  <figcaption>
    <strong>Figure 12:</strong> Comparison of Cornell box lit with HP1 illuminant using a spectral renderer (a) with tristimulus renderers using XYZ (b) and RGB (c) colour matching functions for light transport. Tristimulus renderers are strongly impacted by the colour matching function used to convert spectra. Those renders were done using Shadertoy.
  </figcaption>
</figure>

Discussion
----------

### Drawbacks of spectral rendering

The major drawback of a spectral renderer is the need to specify a spectrum for each illuminant and reflectance. Most tools provided to artists are designed with tristimulus in mind. Spectral uplifting overcomes this problem by creating plausible spectrum from tristimulus values. Jakob and Hanika [[Jakob and Hanika 2019]](#ref-Jakob2019Spectral) recently proposed a method to convert tristimulus textures to plausible spectral reflectance.

Another drawback of a spectral renderer is its inefficiency. While a tristimulus renderer evaluates directly a colour, a spectral renderer adds a dimension to the evaluation. In a path tracer, it means, in addition to the ray direction sampling, the wavelength of the ray also have to be sampled. Usually, in a spectral path tracer, a ray carries a single wavelength. This results in colour noise in low sampled images. However, Hero Wavelength Spectral Sampling (HWSS) technique drastically limit this phenomena carrying multiple wavelengths as the same time with almost the same computational time taking advantage of Single Instruction Multiple Data (SIMD) hardware capabilities [[Wilkie et al. 2014]](#ref-WNDWH14HWSS).

### Advantages of spectral rendering

Spectral rendering is more accurate compared to its tristimulus counterpart, avoiding energy leaks. It also simulates effects impossible to handle correctly in a tristimulus renderer: light dispersion, fluorescence, and polarisation. Those effects are wavelength dependent and thus require consideration for spectra.

Metamerism is another major issue a tristimulus renderer cannot deal with. While two reflectance spectra can be different, their tristimulus counterparts can be the same under a given illuminant. Only a spectral renderer is able to show the difference between those two spectra when changing the illuminant.

Finally, a spectral renderer is agnostic to colour matching functions. The final image can be saved as a spectrum and later converted to a tristimulus display for instance an RGB monitor. The monitor colour response and the observer one can be applied directly to the spectral image to get correct colourimetry. On the other hand, a tristimulus image has to rely on chromatic adaptation.

# Conclusion

We presented how light is perceived by the human vision system and experiments at the origin of the colour matching functions used for transforming spectra to tristimulus coordinates. We use XYZ coordinates to avoid negative values. Starting from these coordinates, we convert to different colour spaces depending on the application. In computer graphics, we mostly use RGB primaries.

For computer graphics applications, tristimulus representations have a major limitation: different spectra can be represented with the same tristimulus coordinates. This can result in important discrepancies using tristimulus rendering pipelines. Spectral rendering is immune to this problem.

However, moving a well-established tristimulus pipeline to spectral is challenging. It requires important code rewriting. We have to specify each reflectance and illuminant in their spectral form. Editing software used by artists are not yet suited for spectral application and using spectral paradigm instead of colour is less intuitive.

Finally, material acquisition is usually performed using tristimulus coordinates. Recently, efficient spectral acquisition techniques were proposed for non-spatially varying materials. For spatially varying material, is out of reach though at the time of writing this thesis. Storage and acquisition time issues, already problematic with tristimulus representations, would drastically increase.

Tristimulus rendering offers a decent approximation in most of the cases and provides efficient evaluation. For critical applications, it is important to be well aware of its limitations though. We cannot use it with line spectra (low pressure vapour lamps for instance) and it is incapable of handling metamers. Particular wavelength dependent effects such as fluorescence and polarisation are also out of reach for a tristimulus renderer.

Sources & references
====================

### Datasets

  - Colour matching functions: The Colour & Vision Research Laboratory  
    <https://www.rit.edu/science/munsell-color-lab>

  - Illuminants: The Rochester Institute of Technology  
    <http://www.rit-mcsl.org/UsefulData/D65_and_A.xls>

  - Macbeth colour checker spectral measurements  
    <http://www.babelcolor.com/colorchecker-2.htm>

### Further readings

  - *Real-Time Rendering fourth edition*, Chapter 8 [[Akenine-Möller et al. 2018]](#ref-moller2018real-time)

  - *The Ocean Optics Web Book* [[Mobley, Boss, and Roesler]](https://www.oceanopticsbook.info/)

  - *Microphysics of light emission (colors of the Universe - part 1)* [[Neyret 2019]](#ref-neyret_microphysics_2019)

  - *The Young-(Helmholtz)-Maxwell Theory of Color Vision* [[Heesen 2015]](#ref-pittphilsci11279)


References
==========

<div id="refs" class="references hanging-indent" markdown="1">

<div id="ref-moller2018real-time" markdown="1">

Akenine-Möller, Tomas, Eric Haines, Naty Hoffman, Angelo Pesce, Michal Iwanicki, and Sébastien Hillaire. 2018. *Real-time rendering Fourth Edition*. Boca Raton, FL: CRC Press, Taylor & Francis Group.

</div>

<div id="ref-Grassmann1853" markdown="1">

Grassmann, H. 1853. “Zur Theorie Der Farbenmischung.” *Annalen Der Physik Und Chemie* 165 (5): 69–84. <https://doi.org/10.1002/andp.18531650505>.

</div>

<div id="ref-pittphilsci11279" markdown="1">

Heesen, Remco. 2015. “The Young-(Helmholtz)-Maxwell Theory of Color Vision.” <http://philsci-archive.pitt.edu/11279/>.

</div>

<div id="ref-Helmholtz1852" markdown="1">

Helmholtz, H. 1852. “Ueber Die Theorie Der Zusammengesetzten Farben.” *Annalen Der Physik Und Chemie* 163 (9): 45–66. <https://doi.org/10.1002/andp.18521630904>.

</div>

<div id="ref-Helmholtz1855" markdown="1">

Helmholtz, H. 1855. “Ueber Die Zusammensetzung von Spectralfarben.” *Annalen Der Physik Und Chemie* 170 (1): 1–28. <https://doi.org/10.1002/andp.18551700102>.

</div>

<div id="ref-Mitsuba" markdown="1">

Jakob, Wenzel, and Johannes Hanika. 2019. “A Low-Dimensional Function Space for Efficient Spectral Upsampling.” *Computer Graphics Forum (Proceedings of Eurographics)* 38 (2).

</div>

<div id="ref-Jakob2010" markdown="1">

Jakob, Wenzel. 2010. “Mitsuba renderer” <http://www.mitsuba-renderer.org>

</div>

<div id="ref-judd1951" markdown="1">

Judd, D. B. 1951. “Report of U.s. Secretariat Committee on Colorimetry and Artificial Daylight.” *Proceedings of the Twelfth Session of the CIE, Stockholm* 1.

</div>

<div id="ref-maxwell_1857" markdown="1">

Maxwell, James Clerk. 1857. “XVIII.—Experiments on Colour, as Perceived by the Eye, with Remarks on Colour-Blindness.” *Transactions of the Royal Society of Edinburgh* 21 (2): 275–98. <https://doi.org/10.1017/S0080456800032117>.

</div>

<div id="ref-10.2307/108759" markdown="1">

Maxwell, J. Clerk. 1860. “On the Theory of Compound Colours, and the Relations of the Colours of the Spectrum.” *Philosophical Transactions of the Royal Society of London* 150: 57–84. <http://www.jstor.org/stable/108759>.

</div>

<div id="ref-ocean_optics" markdown="1">

Mobley, Curtis, Emmanuel Boss, and Collin Roesler. n.d. *Ocean Optics Web Book*. <http://www.oceanopticsbook.info/>.

</div>

<div id="ref-Newton1704" markdown="1">

Newton, Isaac. 1704. *Opticks or, a Treatise of the reflexions, refractions, inflexions and colours of light. Also two treatises of the species and magnitude of curvilinear figures*. London, printed for Sam. Smith. and Benj. Walford. <https://gallica.bnf.fr/ark:/12148/bpt6k3362k>.

</div>

<div id="ref-neyret_microphysics_2019" markdown="1">

Neyret, Fabrice. 2019. “Microphysics of Light Emission (Colors of the Universe - Part 1).” <http://evasion.imag.fr/~Fabrice.Neyret/publis/prez/Microphysics%20of%20light%20emission%20(colors%20of%20the%20Universe%201).pdf>.

</div>

<div id="ref-stiles_interim_1955" markdown="1">

Stiles, W. S., and J. M. Burch. 1955. “Interim Report to the Commission Internationale de L’Eclairage, Zurich, 1955, on the National Physical Laboratory’s Investigation of Colour-Matching (1955).” *Optica Acta: International Journal of Optics* 2 (4): 168–81. <https://doi.org/10.1080/713821039>.

</div>

<div id="ref-stiles_n.p.l._1959" markdown="1">

Stiles, W. S., and J. M. Burch. 1959. “N.P.L. Colour-Matching Investigation: Final Report (1958).” *Optica Acta: International Journal of Optics* 6 (1): 1–26. <https://doi.org/10.1080/713826267>.

</div>

<div id="ref-Stockman2000" markdown="1">

Stockman, Andrew, and Lindsay T. Sharpe. 2000. “The Spectral Sensitivities of the Middle- and Long-Wavelength-Sensitive Cones Derived from Measurements in Observers of Known Genotype.” *Vision Research* 40 (13): 1711–37. <https://doi.org/10.1016/s0042-6989(00)00021-3>.

</div>

<div id="ref-vos_colorimetric_1978" markdown="1">

Vos, J. J. 1978. “Colorimetric and Photometric Properties of a 2\(^{\circ}\) Fundamental Observer.” *Color Research & Application* 3 (3): 125–28. <https://doi.org/10.1002/col.5080030309>.

</div>

<div id="ref-WNDWH14HWSS" markdown="1">

Wilkie, Alexander, Sehara Nawaz, Marc Droske, Andrea Weidlich, and Johannes Hanika. 2014. “Hero Wavelength Spectral Sampling.” *Computer Graphics Forum 33(4) (Proceedings of Eurographics Symposium on Rendering 2014)* 33 (4).

</div>

<div id="ref-10.2307/107126" markdown="1">

Young, Thomas. 1802a. “An Account of Some Cases of the Production of Colours, Not Hitherto Described.” *Philosophical Transactions of the Royal Society of London* 92: 387–97. <http://www.jstor.org/stable/107126>.

</div>

<div id="ref-10.2307/107113" markdown="1">

Young, Thomas. 1802b. “The Bakerian Lecture: On the Theory of Light and Colours.” *Philosophical Transactions of the Royal Society of London* 92: 12–48. <http://www.jstor.org/stable/107113>.

</div>

</div>

------------------------------------------------------------------------------

[^1]: To simplify the notation. we are representing a single bounce. The reflectance spectra or tristimulus values have to be multiplied to each other for each further bounce.

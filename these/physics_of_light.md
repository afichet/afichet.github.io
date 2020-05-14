---
layout: page
title: Physics of light
permalink: /light_physics/
---

Light is both an electromagnetic wave and a particle (photon) displacement. For computer graphics, the latter model is more often used; it is based on geometrical optics.

In simple scenes, the effects due to the wave theory of light are barely noticeable. With more complex materials, they may have a significant impact on the appearance. Most surfaces cause polarisation and light interferences. Polarisation influences inter-reflection between specular surfaces. Interferences produce rainbow effects when light penetrate thin layers or hit small irregularities or scratches.

In this chapter, we first introduce the physics used in computer graphics for describing light radiation. We explain the relationships between wave, frequency and wavelength. We expose how electric field and magnetic induction are linked together and described by Maxwell equations. We introduce radiometric units used in computer graphics. We expose some effects the wave theory of light has on appearance.

Finally, we introduce what is a reflectance with its wavelength dependency. In Chapter [light transport](/light_transport), we further describe reflectance adding the angular dependency with Bidirectional Reflectance Distribution Function (BRDF).

Historical background
=====================

Historically, two interpretations of light have been competing. The first popular interpretation of light was the corpuscular theory proposed by René Descartes in 1637 [[Descartes 1637]](#ref-descartes1637), and further developed by Isaac Newton. The second interpretation was the wave front theory established by Christiaan Huygens presented in *Traité de la Lumière* [[Huygens 2015]](#ref-huygens2015traite).

Despite the comprehensive explanation of light transport provided by Huygens theory, corpuscular theory remained the consensual interpretation among scientists during the 17th century, mainly due to the fame of Descartes. It took a century before the wave theory appeared again thanks to Augustin Fresnel’s work [[Fresnel 1866]](#ref-fresnel_oeuvres_1866).

Still, the real nature of this wave was unknown. James Clerk Maxwell provided the answer in 1864 with his work on electromagnetic waves [[Maxwell 1865]](#ref-Maxwell1865).

The corpuscular theory was getting less attention until the beginning of 20th century with quantum theory. To explain black body radiations, Max Planck [[Planck 1901]](#ref-Planck1901) suggested light could gain or lose finite quanta of energy depending on wavelength. Albert Einstein used this idea in his first article on quantum physics in 1905 [[Einstein 1905a]](#ref-einstein1905), [[1905b]](#ref-doi:10.1002/andp.19053220607). In 1924, de Broglie [[De Broglie 1924]](#ref-debroglie:tel-00006807) proposed the matter-wave theory extending the light corpuscular-wave duality.

The dual interpretation of light is now consensual. Light is both a photon displacement with finite energy states (electron volt[^1]) and an electromagnetic wave propagation. It was experimentally shown by Tsuchiya  [[Tsuchiya et al. 1986]](#ref-Tsuchiya1986) with photon-counting imaging device using the Young’s dual slits experiment.

Frequency and wavelength
========================

<figure id="fig:electromagnetic_wave" class="w3-content" style="max-width:600px">
    <iframe src="/figures/light_physics/images/asy/wave.html" width="600" height="300" frameborder="0"></iframe>
    <figcaption>
        <strong>Figure 1:</strong> Illustration of a linearly polarised electromagnetic wave. The magnetic induction and the electric field are perpendicular and in phase with each other.
    </figcaption>
</figure>

Electromagnetic waves can take various frequencies $$\nu$$, or wavelengths $$\lambda$$. The wavelength $$\lambda$$ characterise the distance between two repetitive patterns of the wave (see Figure [1](#fig:electromagnetic_wave). Light is a subset of electromagnetic waves to which our eyes are sensitive (see Figure [2](#fig:em-spectrum). The wavelength of light characterises its colour. This will be discussed in Chapter [human perception of colours](/human_perception_of_colours).

<figure class="w3-content" id="fig:em-spectrum" style="max-width:700px">
    <img src="/figures/light_physics/images/EM_Spectrum.svg" />
    <figcaption>
        <strong>Figure 2:</strong> Visible light spectrum situated in the range of electromagnetic waves.
    </figcaption>
</figure>


Wavelengths and frequencies are linked by equation \eqref{eqn:wl_freq}.

$$
\begin{equation}
    \lambda = \frac{v}{\nu} \qquad [\mathrm{m}]
    \label{eqn:wl_freq}
\end{equation}
$$
    
Where:
- $$\lambda$$ is the wavelength in meters [$$\mathrm{m}$$].}
- $$v$$ is the speed of the wave in the considered medium in meters per seconds [$$\mathrm{m.s}^{-1}$$].
- $$\nu$$ is the wave frequency in Hertz [$$\mathrm{Hz}$$] i.e. [$$\mathrm{s}^{-1}$$].}

Notice from equation \eqref{eqn:wl_freq}, a wavelength is dependent of speed of propagation for the medium the wave is travelling in. Intuitively, if a wave travels slower in a medium, the repeating oscillation patterns will be closer to each other, and the wavelength will then be shorter. When designating wavelengths for light, we are referring to their wavelength in a vacuum, i.e. for travelling speed of about $$3.10^8\: \mathrm{m.s}^{-1}$$.

Mathematical description
------------------------

All waves, not only electromagnetic waves, are described by the following equation: 

$$
\begin{aligned}
        \mathbf{\Psi} (\mathbf{r}, t) &= \mathbf{A}_0 \cos(\mathbf{k}\cdot \mathbf{r} - \omega t + \varphi_0)\\
    \text{Or in its complex form: } 
        \mathbf{\Psi} (\mathbf{r}, t) &= \mathbf{A}_0 \mathrm{e}^{i \left(\mathbf{k}\cdot \mathbf{r} - \omega t + \varphi_0\right)}
\end{aligned}
$$

Where:
- $$\mathbf{r}$$ is the position in space of three components $$(x, y, z)$$, with $$\|\mathbf{r}\|$$ in [$$\mathrm{m}$$].
- $$t$$ is the time [$$\mathrm{s}$$].
- $$\mathbf{A}_0$$ is the amplitude. It describes the maximum value a waveform can take. For an electric field it is expressed in Volt per meter [$$\mathrm{V}\cdot\mathrm{m}^{-1}$$].}
- $$\mathbf{k}$$ is the wave-number of three components $$(k_x, k_y, k_z)$$ with $$\| \mathbf{r} \|$$ in [$$\mathrm{rad}\cdot\mathrm{m}^{-1}$$]. It describes the number of oscillations per distance unit.
- $$\omega$$ is the wave pulsation, or angular frequency [$$\mathrm{rad}\cdot\mathrm{s}^{-1}$$]. It describes the phase shift per time unit.
- $$\varphi_0$$ is the phase shift [$\mathrm{rad}$]. It describes the de-synchronisation of the wave from a reference wave without retardance.

To simplify calculus the complex form is often used. We deduce the physical solution from the real part.

The wave pulsation is proportional to the wave frequency:

$$
\begin{aligned}
    \omega = 2\pi\nu \qquad [\mathrm{rad}\cdot\mathrm{s}^{-1}]
\end{aligned}
$$

The wave-number vector is proportional to the wavelength, hence, to the frequency and the speed of the wave in the medium it is propagating in. In an isotropic medium, it is pointing to the same direction as the wave propagation direction. This is not the case for anisotropic media such as asymmetrical crystals. 

$$
\begin{aligned}
    \| \mathbf{k}\| = \frac{2\pi}{\lambda} \qquad [\mathrm{rad}\cdot\mathrm{m}^{-1}]
\end{aligned}
$$

Hence, for an isotropic medium with a wave travelling in the $$\mathbf{z}$$ direction: 

$$
\begin{aligned}
    \mathbf{k} &= \begin{bmatrix} 0 \\ 0 \\ k_z\end{bmatrix} = \begin{bmatrix} 0 \\ 0 \\ \frac{2\pi}{\lambda}\end{bmatrix} \qquad [\mathrm{rad}\cdot\mathrm{m}^{-1}]
\end{aligned}
$$

For an electromagnetic field travelling in the $$\mathbf{z}$$ direction, in an isotropic medium with no charge and no current, the electric field $$\mathbf{E}(\mathbf{r}, t)$$ (in volts per meter [$$\mathrm{V.m^{-1}}$$]) and magnetic induction[^2] $$\mathbf{B}(\mathbf{r}, t)$$ (in teslas [$$\mathrm{T}$$]) can be deduced from the Maxwell equations[^3]:

$$
\begin{aligned}
    \mathbf{\nabla} \cdot \mathbf{E} (\mathbf{r}, t) &= 0   & \mathbf{\nabla} \cdot \mathbf{B} (\mathbf{r}, t) &= 0\\
    \mathbf{\nabla} \times \mathbf{E} (\mathbf{r}, t) &= -\frac{\partial \mathbf{B} (\mathbf{r}, t)}{\partial t}    & \mathbf{\nabla} \times \mathbf{B} (\mathbf{r}, t) &= \mu_m \epsilon_m \frac{\partial \mathbf{E} (\mathbf{r}, t)}{\partial t}
\end{aligned}
$$

Where:
- $$\epsilon_m$$ is the permittivity of the medium in [$$\mathrm{F\cdot m^{-1}}$$].
- $$\mu_m$$ is the permeability of the medium in [$$\mathrm{H\cdot m^{-1}}$$].

$$
\begin{eqnarray}
    \label{eqn:electric_field}
    \mathbf{E}(\mathbf{r}, t) &=& \begin{bmatrix} E_{0_x} \cos(k_z - \omega t + \varphi_x) \\ E_{0_y} \cos(k_z - \omega t + \varphi_y) \\ 0\end{bmatrix} \qquad [\mathrm{V.m^{-1}}]\\
    \mathbf{B}(\mathbf{r}, t) &=& \sqrt{\mu_m\epsilon_m}\begin{bmatrix}-E_{0_y} \cos(k_z - \omega t + \varphi_y) \\ E_{0_x} \cos(k_z - \omega t + \varphi_x) \\ 0\end{bmatrix} \qquad [\mathrm{T}]
\end{eqnarray}
$$

Poynting vector
---------------

To describe the energy flux of an electromagnetic wave, the Poynting vector $$\mathbf{S}$$ is used. This is expressed in [$$\mathrm{W.m^{-2}}$$] and denoted $$\mathbf{S}$$. 

$$
\begin{aligned}
    \mathbf{S}(\mathbf{r}, t) &= \mathbf{E}(\mathbf{r}, t) \times \mathbf{H}(\mathbf{r}, t) \qquad [\mathrm{W.m^{-2}}]
\end{aligned}
$$

$$\mathbf{H}$$ is the magnetic field intensity:

$$
\begin{aligned}
    \mathbf{H}(\mathbf{r}, t) &= \frac{1}{\mu_0} \mathbf{B}(\mathbf{r}, t) - \mathbf{M}(\mathbf{r}, t) \qquad [\mathrm{A.m^{-1}}]
\end{aligned}
$$

Where:
- $$\mu_o$$ is the permeability of free space in [$$\mathrm{H\cdot m^{-1}}$$].
- $$\mathbf{M}$$ is the magnetisation vector in [$$\mathrm{A.m^{-1}}$$].

In the following of this manuscript, we are considering wave travelling in an isotropic medium with no charge and no current with $$\mathbf{M}$$ such as $$\mathbf{B} = \mu_m \mathbf{H}$$[^4].

Radiometry
==========

<div id="tbl:radiometric_quatities" markdown="1">

| Quantity              | Notation   | Units                           |
|:----------------------|:----------:|:--------------------------------|
| **radiant flux**      | $$\Phi_e$$ | [$$\mathrm{W}$$]                |
| **irradiance**        |   $$E_e$$  | [$$\mathrm{W.m^{-2}}$$]         |
| **radiant intensity** |   $$I_e$$  | [$$\mathrm{W.sr^{-1}}$$]        |
| **radiance**          |   $$L_e$$  | [$$\mathrm{W.m^{-2}.sr^{-1}}$$] |

</div>

To measure physical quantities transported by an electromagnetic wave, we use radiometric quantities (see table [above](#tbl:radiometric_quatities)). Those are time average values. They do not describe the waveform of the electromagnetic radiation. The unit described in this section are for a whole spectrum or for a specific bandwidth. They shall be given along with the considered bandwidth. Spectral variant of those quantities gives the value for a specific wavelength (per meters or more conveniently, for light, per manometer), or frequency (per hertz).

Radiant flux
------------

The radiant flux $$\Phi_e$$ is the flow of radiant energy $$Q_e$$ passing by unit of time. It is expressed in Joule per seconds [$$\mathrm{J.s}^{-1}$$] i.e. in Watts [$$\mathrm{W}$$]:

$$
\begin{aligned}
    \Phi_e = \frac{\partial Q_e}{\partial t} \qquad [\mathrm{W}]
\end{aligned}
$$

Irradiance
----------

The irradiance is the radiant flux per unit area. This is the density of power for a given surface area $$A$$ (in square meters $$\mathrm{m}^2$$). It is expressed in Watt per square meters [$$\mathrm{W.m^{-2}}$$]:

$$
\begin{aligned}
    E_e(\vec p) = \frac{\partial \Phi_e}{\partial A} \qquad [\mathrm{W.m^{-2}}]
\end{aligned}
$$

Irradiance is the time average of the Poynting vector:

$$
\begin{aligned}
    E_e(\vec p) = <\|\mathbf{S}\|> \cos \theta \qquad [\mathrm{W.m^{-2}}]
\end{aligned}
$$

Where: 
- $$\theta$$ is the angle between the Poynting vector (i.e. $$\mathbf{E} \times \mathbf{H}$$) and the surface element normal.  

Then, given the electric field amplitude, the irradiance in the plane of incidence of the wave is:

$$
\begin{equation}
    \label{eqn:irradiance_time_average}
    E_e(\vec p) = \frac{1}{2} \sqrt{\frac{\epsilon_m}{\mu_m}}  \|\mathbf{E}_0\|^2 \cos \theta \qquad [\mathrm{W.m^{-2}}]
\end{equation}
$$

Where:
- $$\epsilon_m$$ is the electrical permittivity of the medium in [$$\mathrm{F.m}^{-1}$$].}
- $$\mu_m$$ is the magnetic permeability of the medium in [$$\mathrm{H.m}^{-1}$$].}
- $$\mathbf{E}_0$$ is the amplitude $$\mathbf{E}_0 = (E_x, E_y, 0)$$ of the electric field, $$\|\mathbf{E}_o\|$$ in [$$\mathrm{V}\cdot\mathrm{m}^{-1}$$]}

Radiant intensity
-----------------

The radiant intensity $$I_e$$ is the radiant flux per unit of solid angle. A solid angle is a measurement determining the coverage of a spherical cap for a unit sphere ($$\omega$$ unit steradians $$\mathrm{sr}$$). It is expressed in watt per steradian [$$\mathrm{W.sr^{-1}}$$].

$$
\begin{aligned}
    I_e(\omega) = \frac{\partial \Phi_e}{\partial \omega} \qquad [\mathrm{W.sr^{-1}}]
\end{aligned}
$$

Radiance
--------

The radiance $$L_e$$ is the radiant flux per unit area per unit of solid angle. It is expressed in watt per square meter per steradian [$$\mathrm{W.m^{-2}.sr^{-1}}$$]. 

$$
\begin{aligned}
    L_e(\omega, \vec p) = \frac{\partial I_e(\omega)}{\partial A_\bot} = \frac{\partial^2 \Phi_e}{\partial A_\bot \partial \omega} = \frac{\partial^2 \Phi_e}{\cos \theta \partial A \partial \omega} \qquad [\mathrm{W.m^{-2}.sr^{-1}}]
\end{aligned}
$$

<figure id="fig:radiance_irradiance">
    <div class="w3-cell-row">
        <figure class="w3-cell">
            <img src="/figures/light_physics/images/asy/radiance.svg" />
            <figcaption>
                <strong>(a)</strong> Radiance is the radiant flux \(\Phi_e\) over a patch \(\mathrm{d} A\) projected on in the direction \(\omega_i\) per unit of solid angle \(\mathrm{d} \omega_i\).
            </figcaption>
        </figure>
        <figure class="w3-cell">
            <img src="/figures/light_physics/images/asy/irradiance.svg" />
            <figcaption>
                <strong>(b)</strong> Irradiance is the radiant flux \(\Phi_e\) over a patch \(\mathrm{d} A\). It can be seen as the integral of the radiance from all directions.
            </figcaption>
        </figure>
    </div>
    <figcaption>
        <strong>Figure 3:</strong> Radiance and irradiance definitions.
    </figcaption>
</figure>

Reciprocally, we can deduce irradiance from the radiance: it corresponds to the irradiance coming from all directions (see Figure [3](#fig:radiance_irradiance)):

$$
\begin{aligned}
    E_e(\vec p) = \int_\Omega L_e(\omega, \vec p) \cos \theta \,\mathrm{d} \omega \qquad [\mathrm{W.m}^{-2}]
\end{aligned}
$$

Similarly, for the radiant flux: 

$$
\begin{aligned}
    \Phi_e = \int_A \int_\Omega L_e(\omega, \vec p) \cos \theta \,\mathrm{d} \omega \,\mathrm{d} A \qquad [\mathrm{W}]
\end{aligned}
$$

Radiance and irradiance are important in computer graphics. Radiance is the quantity which is perceived by our eyes or by a camera sensor. In Chapter [light transport](/light_transport), we use the differential ratio between exiting radiance and incident irradiance on a surface to define the bidirection reflectance distribution function (BRDF).

Spectral power distribution
---------------------------

The previously presented photometric quantities are defined for the whole spectrum (a range of frequencies or wavelengths). For computer graphics, it is necessary to characterise the radiometric quantities for a given frequency or wavelength in order to translate those quantities into colours later on. The corresponding photometric units can be derived per unit of wavelength $$\lambda$$ or frequency $$\nu$$.

The spectral radiance: 

$$
\begin{aligned}
    L_e(\omega, \vec p, \lambda) = \frac{\partial^3 \Phi_e}{\partial A_\bot \partial \omega \partial \lambda} = \frac{\partial L_e(\omega, \vec p)}{\partial \lambda} \qquad [\mathrm{W.m^{-3}.sr^{-1}}]
\end{aligned}
$$

The spectral irradiance: 

$$
\begin{aligned}
    E_e(\vec p, \lambda) = \frac{\partial^2 \Phi_e}{\partial A \partial \lambda} = \frac{\partial E_e(\vec p)}{\partial \lambda} \qquad [\mathrm{W.m^{-3}}]
\end{aligned}
$$

A spectral power distribution (SPD) describes the value of spectral irradiance $$E_e(\vec p, \lambda)$$ for a range of frequencies. It is usually more convenient to express the wavelength of light in manometer [$$\mathrm{nm}$$] i.e. [$$10^{-9}\:\mathrm{m}$$] so the spectral irradiance in [$$\mathrm{W.m^{-2}.nm^{-1}}$$].

A relative SPD is a normalised SPD relative to the spectral irradiance at a given wavelength, often unity or $$100\%$$ at $$\lambda_0 = 560\:\mathrm{nm}$$.

$$
\begin{aligned}
    E_{e_{rel}}(\vec p, \lambda) = \frac{E_e(\vec p, \lambda)}{E_e(\vec p, \lambda_0)}
\end{aligned}
$$

<figure id="fig:spd_d65">
    <img src="/figures/light_physics/plot/output/spd_d65.svg" />
    <figcaption>
        <strong>Figure 4:</strong> CIE D65 illuminant relative spectral power distribution.\(E_e(560\:\mathrm{nm}) = 1\).
    </figcaption>
</figure>

Figure [4](#fig:spd_d65) shows an example of the relative SPD of CIE (<span lang="fr">*Commission Internationnale de l’Éclairage*</span>) D65 illuminant. An illuminant is a standardised light emission relative SPD.

Interferences
=============

In this section and the following, we describe several phenomena related to the wave nature of light. They are not always visible but it is useful to know they exist and keep them in mind.

#### Wave superposition

<figure id="fig:interferences_planar">
    <div class="w3-cell-row">
        <figure class="w3-cell">
            <img src="/figures/light_physics/images/same_freq.svg">
            <figcaption>
                <strong>(a)</strong> When summing two waves of the same frequency of phase difference \(\pi\), they cancel each other.
            </figcaption>
        </figure>
        <figure class="w3-cell">
            <img src="/figures/light_physics/images/shift_freq.svg">
            <figcaption>
                <strong>(b)</strong> In this case, the phase difference is \(\frac{5\pi}{6}\), the resulting wave have a lower intensity than each individual wave it is resulting from.
            </figcaption>
        </figure>
    </div>
    <figcaption>
        <strong>Figure 5:</strong> Interference between two waves of the same frequency. The phase and amplitude of the resulting wave depends on the amplitudes and phases of the two waves.
    </figcaption>
</figure>

The superposition of two waves of the same frequency is a wave of the same frequency: 

$$
\begin{eqnarray}
    \mathbf{\Psi} &=& A_1 \cos(\omega t + \varphi_1) + A_2 \cos(\omega t + \varphi_2)\\
    &=& \frac{A_1}{2}\left[\mathrm{e}^{i (\omega t + \varphi_1)} + \mathrm{e}^{-i (\omega t + \varphi_1)} \right] + \frac{A_2}{2} \left[ \mathrm{e}^{i (\omega t + \varphi_2)} + \mathrm{e}^{-i (\omega t + \varphi_2)} \right] \nonumber\\
    &=& \frac{1}{2}\left[ \mathrm{e}^{i \omega t} \left( A_1\mathrm{e}^{i \varphi_1} + A_2\mathrm{e}^{i \varphi_2} \right) +  \mathrm{e}^{-i \omega t} \left( A_1\mathrm{e}^{-i \varphi_1} + A_2\mathrm{e}^{-i \varphi_2} \right) \right]\nonumber\\
    \text{let } A_3\mathrm{e}^{i\varphi_3} &=&  A_1\mathrm{e}^{i \varphi_1} + A_2\mathrm{e}^{i \varphi_2}\label{eqn:fresnel_vector}\\
    &=& \frac{1}{2}\left[ \mathrm{e}^{i \omega t} A_3\mathrm{e}^{i\varphi_3} + \mathrm{e}^{-i \omega t} A_3\mathrm{e}^{-i\varphi_3} \right]\nonumber\\
    &=& \frac{A_3}{2}\left[ \mathrm{e}^{i (\omega t +\varphi_3)} + \mathrm{e}^{-i (\omega t + \varphi_3)} \right]\nonumber\\
    &=& A_3 \cos(\omega t + \varphi_3) \label{eqn:result_superpose}
\end{eqnarray}
$$

The resulting wave (equation above) have a different amplitude $$A_3$$ and phase $$\varphi_3$$. So, when two waves of the same frequency cross or superpose each other, this causes interferences. The superposition of two waves can yield in the extreme cases of a resulting wave of null amplitude (destructive interference) or a wave with a double amplitude (constructive interference).

The phase difference from one to the other defines how they are going to interfere (see Figure [5](#fig:interferences_planar)).

To compute the resulting amplitude $$A_3$$ and phase $$\varphi_3$$, we can
use Fresnel vectors.

<figure id="fig:fresnel_vectors">
    <img src="/figures/light_physics/images/asy/fresnel_vectors.svg" />
    <figcaption>
    <strong>Figure 6:</strong> Fresnel's vectors: red and purple vectors represent waves of the same frequency with different amplitudes and phase shifts. The sum of the two gives the amplitude and phase shift of the resulting wave.
    </figcaption>
</figure>

Equation \eqref{eqn:fresnel_vector} shows the resulting phase and amplitude can be deduced from the sum of two complex numbers. This is equivalent to addition of two vector in the complex plane, one of magnitude $$A_1$$ and phase $$\varphi_1$$, the other with magnitude $$A_2$$ and phase $$\varphi_2$$. Those are the Fresnel vectors corresponding to the two superposed waves. The module of resulting vector will be $$A_3$$ and its argument $$\varphi_3$$ (see Figure [6](#fig:fresnel_vectors)).

#### Optical path length

Given a wave $$\mathbf{\Psi}$$ of wavelength $$\lambda$$ and phase shift $$\varphi$$ at point $$\mathbf{O}$$, travelling at speed $$c$$ in the considered medium. Its phase shift $$\varphi'$$ at point $$\vec T$$ of distance $$l$$ from $$\mathbf{O}$$, will be: 

$$
\begin{aligned}
    \mathbf{\Psi}(\mathbf{O}) &= A \cos(2\pi \cdot \frac{c}{\lambda} \cdot t + \varphi)\nonumber\\
    \mathbf{\Psi}(\vec T) &= A \cos(2\pi \cdot \frac{c}{\lambda} \cdot t + \varphi')\nonumber\\
            &= A \cos(2\pi \cdot \frac{c}{\lambda} \cdot (t + \Delta t) + \varphi)\nonumber\\
    \Delta t &= \frac{l}{c} \nonumber\\
    \mathbf{\Psi}(\vec T) &= A \cos(2\pi \cdot \frac{c}{\lambda} \cdot t + \frac{2\pi}{\lambda} \cdot l + \varphi) \nonumber\\
    \varphi' &= \frac{2\pi}{\lambda} \cdot l + \varphi
\end{aligned}
$$

From the optical path length $$l$$ (OPL) we get the relative shift of a wave: $$\delta = \frac{2\pi}{\lambda} \cdot l$$.

#### Interference patterns

Figure [7](#fig:opl) shows two waves $$\mathbf{\Psi}_1, \mathbf{\Psi}_2$$ of same wavelength $$\lambda$$ with phase shifts $$\varphi_1, \varphi_2$$ at position $$\mathbf{P_1}, \mathbf{P_2}$$. They cross at $\mathbf{P_3}$ at distances $$l_1, l_2$$ respectively from $$\mathbf{P_1}, \mathbf{P_2}$$. The resulting wave $$\mathbf{\Psi}_3$$ at $$\mathbf{P_3}$$ will be the result of the interference between $$\mathbf{\Psi}_1$$ and $$\mathbf{\Psi}_2$$. To get the resulting wave $$\mathbf{\Psi}_3$$, we are interested in knowing respective phases $$\varphi'_1, \varphi'_2$$ of $$\mathbf{\Psi}_1, \mathbf{\Psi}_2$$ at $$\mathbf{P_3}$$.

<figure id="fig:opl">
    <img src="/figures/light_physics/images/asy/opd.svg" />
    <figcaption>
        <strong>Figure 7:</strong> Optical path length. The optical path length determines the amplitude and phase shift when two monochromatic waves cross point.
    </figcaption>
</figure>

Given the optical path lengths $$l_1, l_2$$, we can deduce the superposition of $$\mathbf{\Psi}_1$$ and $$\mathbf{\Psi}_2$$ at $$\mathbf{P_3}$$:

$$
\begin{aligned}
    \mathbf{\Psi}_3 &= A \left[ \cos(\omega t + \varphi'_1) + \cos(\omega t + \varphi'_2) \right]\\
           &= A \left[ \cos(\omega t + (\delta_1 + \varphi_1)) + \cos(\omega t + (\delta_2 + \varphi_2)) \right]\\
           &= 2A \cos\left( \frac{\delta_1 - \delta_2}{2} \frac{\varphi_1 - \varphi_2}{2} \right) \cos\left(\omega t + \frac{\delta_1 + \delta_2}{2} \frac{\varphi_1 + \varphi_2}{2} \right)
\end{aligned}
$$

Notice the amplitude variation in space is dependent of the wavelength. This means, the constructive and destructive interferences occurs at a different spatial frequency depending on the wavelength. The second cosine term is time dependant and not influencing the appearance of the interference pattern: the irradiance is the time-average of the resulting wave. So, the optical path difference $$l_1 - l_2$$ determines the wave amplitude and irradiance at $$\mathbf{P_3}$$.

In practice, this leads to the observation of rainbow patterns with interferences and polychromatic light. Fresnel’s vectors can be used if having to consider waves of different amplitude or for accumulating results from a path tracer (see Figure [8](#fig:interferences_d65)).

While the superposition of waves is linear, the resulting irradiance is proportional to the square of the wave amplitude (see equation \eqref{eqn:irradiance_time_average}).

Interferences are observable at macro-scale (see Figure [9](#fig:interferences_examples)). For instance, surfaces whose thickness is in the order of magnitude of wavelength of light (soap bubble, anti-glare coating, leather conditioners...) create visible rainbow effects due to interferences. Microstructure also cause interferences (small scratches on metals, tiny bumps on some plastics...). Those phenomena are due to light path interfering with itself causing coloured reflection even with incoherent light.

Interferences also occur when light hits a surface with irregularities at the scale of the wavelength. Holzschuch and Pacanowski [[Holzschuch and Pacanowski 2017]](#ref-Holzschuch:2017:TMR:3072959.3073621) proven the need for taking interferences into account and proposed a model to handle those phenomena (see Figure [10](#fig:diffraction_hp_allu)). Belcour and Barla [[Belcour and Barla 2017]](#ref-belcour_practical_2017) proposed a model to handle iridescent effects caused by thin-films.

<figure id="fig:interferences_d65" class="w3-content" style="max-width:800px">
    <img src="/figures/light_physics/images/render_41217.png" class="w3-card" />
    <figcaption>
    <strong>Figure 8:</strong> A simulation of interferences caused by two slits when lit with coherent D65 spectrum. We used Fresnel's vectors to accumulate contributions from a stochastic evaluation.
    </figcaption>
</figure>

<figure id="fig:interferences_examples" class="w3-row-padding">
    <figure class="w3-col m4 l4">
        <img src="/figures/light_physics/images/DSF0008.jpg" class="w3-card" />
        <figcaption>
        <strong>(a)</strong> Lens surface.
        </figcaption>
    </figure>
    <figure class="w3-col m4 l4">
        <img src="/figures/light_physics/images/DSF0012.jpg" class="w3-card" />
        <figcaption>
        <strong>(b)</strong> Shaving foam bubbles.
        </figcaption>
    </figure>
    <figure class="w3-col m4 l4">
        <img src="/figures/light_physics/images/DSF0013.jpg" class="w3-card" />
        <figcaption>
        <strong>(c)</strong> Leather.
        </figcaption>
    </figure>
    <figcaption>
    <strong>Figure 9:</strong> Interferences observable at macro scale. At the surface of a lens, the thin layer of anti-glare coating creates interferences causing coloured reflection at the surface of the glass <strong>(a)</strong>. The surface of soap bubbles is also showing rainbows effects <strong>(b)</strong>. Other surfaces such as leather show bright coloured highlight <strong>(c)</strong>.
    </figcaption>
</figure>

<figure id="fig:diffraction_hp_allu" class="w3-row-padding">
    <figure class="w3-col m4 l4">
        <img src="/figures/light_physics/diffraction/ct.png" class="w3-card" />
        <figcaption>
        <strong>(a)</strong> Specular only (Cook-Torrance).
        </figcaption>
    </figure>
    <figure class="w3-col m4 l4">
        <img src="/figures/light_physics/diffraction/diffraction.png" class="w3-card" />
        <figcaption>
        <strong>(b)</strong> Diffraction only.
        </figcaption>
    </figure>
    <figure class="w3-col m4 l4">
        <img src="/figures/light_physics/diffraction/hp.png" class="w3-card" />
        <figcaption>
        <strong>(c)</strong> Holzschuch-Pacanowski model ((a) + (b)).
        </figcaption>
    </figure>
    <figcaption>
        <strong>Figure 10:</strong> Interferences can cause visible hazy reflections. Here, an example for aluminium from <a href="#ref-Holzschuch:2017:TMR:3072959.3073621">[Holzschuch and Pacanowski 2017]</a>. Material have irregularities at the scale of the wavelength producing interferences.)
    </figcaption>
</figure>


Polarisation
============

We have considered the electric field oscillating in one plane in the previous examples. In equation \eqref{eqn:electric_field}, the electric field was presented in a more complete form. Its amplitude and shift may differ for $$\mathbf{x}$$ and $$\mathbf{y}$$ axis when propagating in $$\mathbf{z}$$ direction. The plane where the electric field propagates may rotate over time. This defines the polarisation of the wave.

Polarisation states
-------------------

<figure id="fig:polarisation_states">
    <div class="w3-row-padding">
        <figure class="w3-col m4 l4">
            <img src="/figures/light_physics/images/asy/polarized_linear.svg" width="80%"  />
            <figcaption>
            <strong>(a)</strong> Linear polarisation. The amplitude projection of the field on x is null.
            </figcaption>
        </figure>
        <figure class="w3-col m4 l4">
            <img src="/figures/light_physics/images/asy/polarized_elliptic.svg" id="subfig:elliptical_polarisation" width="80%" />
            <figcaption>
            <strong>(b)</strong> Elliptical polarisation. The projection of the field on x and y planes is 90<span class="math inline"><sup>∘</sup></span> out of phase with higher magnitude for the sinusoid on y axis.
            </figcaption>
        </figure>
        <figure class="w3-col m4 l4">
            <img src="/figures/light_physics/images/asy/polarized_circular.svg" id="subfig:circular_polarisation" width="80%" />
            <figcaption>
            <strong>(c)</strong> Circular polarisation. The projection of the field on x and y planes is 90<span class="math inline"><sup>∘</sup></span> out of phase with equal magnitude.
            </figcaption>
        </figure>
    </div>
    <figcaption >
        <strong>Figure 11:</strong> Polarisation states of the electric field of a monochromatic wave. The magnetic induction is perpendicular to the electric field (see Figure <a href="#fig:em-spectrum">2</a>) and is not represented for clarity. The projection on the x plane represents the rotation of the electric field over time. When the wave is projected onto the z plane, the different polarisation patterns are visible.
    </figcaption>
</figure>

When the plane where the electric field propagates remains fixed, the light is said linearly polarised. If the plane rotates over time at the same frequency as the wave frequency, the light is said to be circularly polarised. The intermediate states are said elliptically polarised. Finally, if this plane rotates randomly the light is said to be unpolarised.

Figure [11](#fig:polarisation_states) illustrates different states of polarisation. The electric field $$\mathbf{E}$$ propagates along the $$\mathbf{z}$$ axis and is projected on $$\mathbf{x}$$ and $$\mathbf{y}$$. It is defined as: 

$$
\begin{aligned}
    \mathbf{E} (t) &= E_x(t) \cdot \mathbf{x} + E_y(t) \cdot \mathbf{y} \qquad [\mathrm{V.m^{-1}}]
\end{aligned}
$$

Where $$E_x(t)$$ and $$E_y(t)$$ are the electric field components with respect to $$\mathbf{x}$$ and $$\mathbf{y}$$ directions.

We cannot measure the value of $$\mathbf{E} (t)$$ but only its time-averaged value, corresponding to the irradiance $$E_e$$ (see equation \eqref{eqn:irradiance_time_average}).

While our eyes are almost not sensitive to the polarisation of light[^5], light transport is: surfaces can reflect or transmit the light differently depending on the polarisation state of the incoming radiation. The resulting energy received by our eyes is then impacted. It is necessary to consider polarisation for light transport interactions in computer graphics.

Stokes formalism
----------------

To represent polarisation states, various mathematical formalisms exists. We use the Stokes vector formalism, adopted in computer graphics:

$$
\begin{aligned}
    \mathbf{S} 
    = \begin{pmatrix} S_0 \\ S_1 \\ S_2 \\ S_3 \end{pmatrix}
    = \begin{pmatrix} I   \\ Q   \\ U   \\ V   \end{pmatrix}
\end{aligned}
$$

The same wave can be represented as different combination of sinusoidal waves on an orthogonal basis depending on the frame orientation. So, this vector[^6] is defined within a specific frame.

### Linear polarisation

We can measure the irradiance but not directly the variation of electric field over time. With two linear polarisation filters, one aligned in $$\mathbf{x}$$ direction and the other with $$\mathbf{y}$$, we can measure $$E_{e_x}$$ and $$E_{e_y}$$, the irradiance components on $$\mathbf{x}$$ and $$\mathbf{y}$$.

The Stokes’ parameter $$Q$$ is defined as follows:

$$\begin{aligned}
    Q = E_{e_x} - E_{e_y}  \qquad  [\mathrm{W.m^{-2}}]
\end{aligned}$$

When the linearly polarised wave is rotated, the polarisation axis cannot be determined solely with $$Q$$: two solutions are possible.

To leverage this indetermination, we use the third Stokes’ parameter $$U$$. It consists in rotating the $$(\mathbf{O}, \mathbf{x}, \mathbf{y})$$ frame by $$45^{\circ}$$. We are calling this new frame $$(\mathbf{O}, \vec a, \mathbf{B})$$. Then, the irradiance components are measured in this new frame (see Figure [12](#fig:QU_filters)):

$$
\begin{equation}
    U = E_{e_a} - E_{e_b}  \qquad  [\mathrm{W.m^{-2}}]
\end{equation}
$$

<figure id="fig:QU_filters" class="w3-content" style="max-width:800px">
    <iframe src="/figures/light_physics/images/asy/polarized_stokes_linear_xy_U.html" width="800" height="540" frameborder="0"></iframe>
    <figcaption>
        <strong>Figure 12:</strong> When using both \(Q\) and \(U\), the indetermination is solved. Only one solution is valid, we can discard the second (represented by the dashed arrows).
    </figcaption>
</figure>

### Circular polarisation

Figures <a href="#subfig:elliptical_polarisation" data-reference-type="ref" data-reference="subfig:elliptical_polarisation">3</a> and <a href="#subfig:circular_polarisation" data-reference-type="ref" data-reference="subfig:circular_polarisation">4</a> illustrate the case where the electric field is rotating over time leading to circular or elliptical polarisation.

<figure id="fig:stokes_circular">
    <div class="w3-cell-row">
        <figure class="w3-cell">
            <img src="/figures/light_physics/images/asy/polarized_stokes_circular_left.svg" width="80%" />
            <figcaption>
                <strong>(a)</strong> Left circular polarised light.
            </figcaption>
        </figure>
        <figure class="w3-cell">
            <img src="/figures/light_physics/images/asy/polarized_stokes_circular_right.svg" width="80%" />
            <figcaption>
                <strong>(b)</strong> Right circular polarised light.
            </figcaption>
        </figure>
    </div>
    <figcaption>
        <strong>Figure 13:</strong> Using quarter-wave filter and linear linear polarisation filters, we can determine the polarisation rotation direction.
    </figcaption>
</figure>

We get $$E_{e_l}$$ and $$E_{e_r}$$, the irradiance of left and right polarisation with combination of a quarter-wave filter and a linear polarisation filter. A quarter-wave filter introduces a phase shift of $$\frac{\pi}{2}$$ on one axis of the electric field. Depending on the rotation direction of the polarisation plane, it transforms circular into linear polarised wave rotated by $$45^\circ$$ or $$-45^\circ$$ (see Figure [13](#fig:stokes_circular)).

The fourth Stokes’ parameter $$V$$ is defined as: 

$$
\begin{aligned}
    V = E_{e_r} - E_{e_l}  \qquad  [\mathrm{W.m^{-2}}]
\end{aligned}
$$

We have to use and specify a convention for the orientation of the circular polarisation. Here, we are in the frame facing the propagation direction of the wave.

### Irradiance and degree of polarisation

The first component $$I$$ of the Stokes’ vector is the irradiance. We can represent any polarisation state by Stoke’ vectors: a randomly polarised light will have its $$Q, U, V$$ components null. But irradiance information will remained characterised by its $$I$$ component.

The ratio between norm of vector defining polarisation $$(Q, U, V)$$, $$(Q, U)$$ or $$V$$ and irradiance $$I$$ is the degrees of polarisation (see Table below).

| Degree of polarisation | Degree of linear polarisation | Degree of circular polarisation |
| :--------------------- | :---------------------------- | :------------------------------ |
| $$DoP = 100 \cdot \frac{\sqrt{Q^2+U^2+V^2}}{I}$$ | $$DoLP = 100 \cdot \frac{\sqrt{Q^2+U^2}}{I}$$ | $$DoCP = 100 \cdot \frac{V}{I}$$ |

Reflectance
===========

When light interacts with matter, it is scattered. The energy is not scattered equally depending on the wavelength and the direction of the incoming wave. We will discuss in Chapter [light transport](/light_transport) the directional dependency.

Reflectance is the effectiveness of a surface to reflect radiant energy. It is a function of wavelength.

Spectral reflectance
--------------------

In the simpler scenario, when light illuminate a surface, the reflected radiation will be at the same frequency as the incoming one. The reflectance can be described similarly as a spectral power distribution. For a given wavelength, the effectiveness of its reflection is given by a value.

Figure [14](#fig:reflectance) shows an example of such reflectance spectrum from a measured material of the database of Dupuy and Jakob [[Dupuy and Jakob 2018]](#ref-Dupuy2018Adaptive).

<figure id="fig:reflectance">
    <img src="/figures/light_physics/plot/output/reflectance.svg" />
    <figcaption>
        <strong>Figure 14:</strong> A measured reflectance, TeckWrap vinyl wrapping film (Ibiza Sunset RD02), from Dupuy and Jakob <a href="#ref-Dupuy2018Adaptive">[Dupuy and Jakob 2018]</a>. This shows the efficiency of the material to reflect incoming radiance for a given set of illumination and observation.
    </figcaption>
</figure>

Bi-spectral reflectance
-----------------------

In addition to straight re-emission with the same wavelength, a material can, for certain exiting wavelengths re-emit at a longer wavelength. This phenomena is called fluorescence.

<figure class="w3-row-padding">
    <figure class="w3-col m4 l4">
        <img src="/figures/light_physics/images/DSCF9230.jpg" class="w3-card" />
        <figcaption>
        <strong>(a)</strong> Photograph of fluorescent safety vests.
        </figcaption>
    </figure>
    <figure class="w3-col m4 l4">
        <img src="/figures/light_physics/images/DSF0062.jpg" class="w3-card" />
        <figcaption>
        <strong>(b)</strong> Photograph of a fluorescent stone.
        </figcaption>
    </figure>
    <figure class="w3-col m4 l4">
        <img src="/figures/light_physics/images/SIGGRAPH_2012_FluoScene.synth.fullSpectrum.mis.hero.i2000.png" class="w3-card" />
        <figcaption>
        <strong>(c)</strong> Rendering of fluorescent objects using ART renderer [[ART]](https://cgg.mff.cuni.cz/ART/). The inner spheres are fluorescent while the outer ones are not.
        </figcaption>
    </figure>
    <figcaption>
    <strong>Figure 15:</strong> Example of scenes featuring fluorescent objects. In (a) and (b), fluorescent objects are lit with a near monochromatic blue LED torch. The objects reflect other colours than the one used to lit the scene. In (c), a rendering shows the same object with and without fluorescence in a daylight environment. Fluorescent objects appear brighter than the environment bringing energy from bandwidth where our eyes are less sensitive to bandwidth where it is more sensitive.
    </figcaption>
</figure>

A molecule re-emits a previously absorbed photon in a lower energy state than the one it was absorbed in: this means the re-emitted light from a collision event with such a molecule has a longer wavelength than the original incoming light. This shift from the absorbed frequency to the re-emitted one is spread around a main frequency as shown in Figure [16](#fig:stokes-shift). This is referred to as *Stokes shift*.

<figure id="fig:stokes-shift">
    <img src="/figures/light_physics/plot/output/energy.svg" />
    <figcaption>
        <strong>Figure 16:</strong> An example of the so-called *Stokes shift*, here shown for the material found in pink fluorescent 3M pink Post-it notes. Practically all fluorophores exhibit similar characteristics: namely, that there is one main band where energy is absorbed, and one where it is re-emitted. Note that one still needs the full re-radiation matrix of the fluorophore in question to generate such a plot, which only shows the cumulative shifting effect of the material. Figure <a href="#fig:reradiation-matrix">17</a> shows the entire re-radiation matrix of this material.
    </figcaption>
</figure>

Such phenomena can be described by a fluorescence response function $$\Phi(\lambda_i, \lambda_o)$$, which for an excitation wavelength $$\lambda_i$$ returns the amount of energy relaxed to another re-emission wavelength $$\lambda_o$$. For  $$\lambda_i=\lambda_o$$, this corresponds to the non-fluorescent reflectance introduced in the previous section.

### Re-radiation matrix

<figure id="fig:reradiation-matrix">
    <img src="/figures/light_physics/plot/output/matrix.svg" />
    <figcaption>
        <strong>Figure 17:</strong> The full re-radiation matrix \(\Phi(\lambda_i, \lambda_o)\) for the material shown in Figure <a href="#fig:reradiation-matrix">16</a>. Values lower than 0.006 are ignored in this plot, as they are considered measurement noise.
    </figcaption>
</figure>

The fluorescence response $$\Phi(\lambda_i, \lambda_o)$$ can be represented in a discretised form as a so-called re-radiation matrix. An example dataset is shown in Figure [17](#fig:reradiation-matrix). The incoming wavelength $$\lambda_i$$ lies on its vertical axis, and the outgoing wavelength $$\lambda_o$$ on its horizontal. The diagonal of such a re-radiation matrix describes the amount of light that does not undergo any wavelength shift.

### Shifting probability

*Kasha’s rule* states that the re-emission spectrum distribution should be the same, whatever wavelength within the absorbing area of the spectrum is used for excitation. Only the intensity of this re-emitted spectrum is modified. However, this rule does not always apply – at least not in the strict sense.

<figure id="fig:probability-shift">
    <img src="/figures/light_physics/plot/output/probability_shift.svg" />
    <figcaption>
        <strong>Figure 18:</strong> Re-emission probability distribution for several excitation wavelengths in the dataset shown in Figure <a href="#fig:reradiation-matrix">16</a>. This plot amounts to several vertical cuts approximately halfway through the centre of the wavelength-shifting activity, for different incident wavelengths. These show that Kasha's rule is not an exact rule, so that there is some variation: but the overall appearance of the spectra is quite similar overall.
    </figcaption>
</figure>

While the accumulated energy absorption and re-emission, as show in Figure [16](#fig:stokes-shift), represents, respectively, the sum of the columns and the lines of the re-radiation matrix, i.e. $$\int_\Lambda- \Phi(\lambda,\lambda_o)- \,\mathrm{d}\lambda_o$$ and $$\int_\Lambda- \Phi(\lambda_i,\lambda)- \,\mathrm{d}\lambda_i$$, the probability for a given wavelength to be the re-emitted may differ if the particle does not exactly follow Kasha’s rule (and as Figure [18](#fig:probability-shift) shows, such slight variations are actually the norm). Then, the distribution of possible re-emission wavelengths for an excitation wavelength $$j$$ is given by the corresponding column $$j$$ in the re-radiation matrix. On the other hand, from a re-emitted wavelength $$i$$, the possible spectrum of excitation wavelengths is given by the corresponding line $$i$$ in the matrix.

Conclusion
==========

In this chapter, we have presented light as a wave. We introduced radiometric units useful in computer graphics. We insist on the importance of considering light as an electromagnetic wave through its spectral power distribution and its polarisation state. We have exposed some visual effects due to the wave nature of light.

In computer graphics, we mostly use geometrical optics for light transport. We can use specific mathematical frameworks to account for some of wave properties. For instance, Stokes’ vectors account for polarisation in geometrical optics. Local models also handle properties of the wave nature of light like interferences.

For global light transport, we generally ignore effects like diffraction, causing wavefront propagation in occluded areas. At the time of writing this thesis, they are hard to evaluate globally and induce a huge memory overhead with an increasing complexity. They generally does not impact significantly the final rendering, with
wavelength we are working with.

We prefer to use local models to handle those complicated cases while providing a good approximations.

<!-- 
Résumé du chapitre
==================

Dans ce chapitre, nous avons présenté la lumière sous sa forme d’onde.
Nous avons introduit certaines unités radiométriques utiles en
informatique graphique. Nous avons insisté sur l’importance de
considérer la lumière comme une onde électromagnétique en la
caractérisant par sa distribution spectrale et son état de polarisation.
Nous avons présenté certains phénomènes liés à la nature ondulatoire de
la lumière.

Les phénomènes ondulatoires sont majoritairement ignorés en informatique
graphique. Le transport de la lumière suit généralement les règles de
l’optique géométrique. Toutefois, certains outils mathématiques
permettent la simulation d’une partie des phénomènes liés à la nature
ondulatoire de la lumière. Les vecteurs de Stokes permettent, par
exemple, la prise en compte de la polarisation de l’onde. Des modèles
locaux peuvent aussi permettre d’incorporer certains phénomènes
ondulatoires tels que les interférences.

Toutefois, pour le transport global, certains effets tels que la
diffraction, qui cause une propagation du front d’onde dans des zones où
l’optique géométrique considère que l’énergie est nulle, sont
généralement ignorés. Pour l’instant, certains de ces phénomènes sont
difficiles à évaluer efficacement car ils induisent une augmentation
drastique de la complexité et de la consommation mémoire. Enfin, ils ne
participent pas nécessairement de façon significative à l’apparence
finale d’une image et peuvent souvent être ignorés.

Des modèles locaux sont alors privilégiés proposant de bonnes
approximations. -->


# References

<div id="refs" class="references hanging-indent" markdown="1">

<div id="ref-belcour_practical_2017" markdown="1">

Belcour, Laurent, and Pascal Barla. 2017. “A Practical Extension to
Microfacet Theory for the Modeling of Varying Iridescence.” *ACM Trans.
Graph.* 36 (4): 65:1–65:14. <https://doi.org/10.1145/3072959.3073620>.

</div>

<div id="ref-debroglie:tel-00006807" markdown="1">

De Broglie, Louis. 1924. “Recherches sur la théorie des Quanta.” Theses,
Migration - université en cours d’affectation.
<https://tel.archives-ouvertes.fr/tel-00006807>.

</div>

<div id="ref-descartes1637" markdown="1">

Descartes, René. 1637. *Discours de La Méthode Pour Bien Conduire Sa
Raison et Chercher La Vérité Dans Les Sciences, Plus La Dioptrique, Les
Météores et La Géométrie Qui Sont Des Essais de Cette Méthode*. A Leyde
de l’imprimerie de Jan Maire.
<https://gallica.bnf.fr/ark:/12148/btv1b86069594/>.

</div>

<div id="ref-Dupuy2018Adaptive" markdown="1">

Dupuy, Jonathan, and Wenzel Jakob. 2018. “An Adaptive Parameterization
for Efficient Material Acquisition and Rendering.” *Transactions on
Graphics (Proceedings of SIGGRAPH Asia)* 37 (6): 274:1–274:18.
<https://doi.org/10.1145/3272127.3275059>.

</div>

<div id="ref-einstein1905" markdown="1">

Einstein, Albert. 1905a. “On a Heuristic Point of View about the
Creation and Conversion of Light.” *English Translation by Wikisource*.
English translation by Wikisource
<https://en.wikisource.org/?curid=59468>.

</div>

<div id="ref-doi:10.1002/andp.19053220607" markdown="1">

Einstein, Albert. 1905b. “Über einen die Erzeugung und Verwandlung des Lichtes
betreffenden heuristischen Gesichtspunkt.” *Annalen Der Physik* 322 (6):
132–48. <https://doi.org/10.1002/andp.19053220607>.

</div>

<div id="ref-fresnel_oeuvres_1866" markdown="1">

Fresnel, Augustin. 1866. *Oeuvres Complètes d’Augustin Fresnel*. Edited
by Léonor Fresnel, Henri de Senarmont, and Émile Verdet. Paris: Impr.
impériale. <http://gallica.bnf.fr/ark:/12148/bpt6k1512245j>.

</div>

<div id="ref-Holzschuch:2017:TMR:3072959.3073621" markdown="1">

Holzschuch, Nicolas, and Romain Pacanowski. 2017. “A Two-scale
Microfacet Reflectance Model Combining Reflection and Diffraction.” *ACM
Transactions on Graphics* 36 (4): 66:1–66:12.
<https://doi.org/10.1145/3072959.3073621>.

</div>

<div id="ref-huygens2015traite" markdown="1">

Huygens, Christiaan. 2015. *Traité de La Lumière*. Paris: Dunod.

</div>

<div id="ref-Maxwell1865" markdown="1">

Maxwell, James Clerck. 1865. “VIII. A Dynamical Theory of the
Electromagnetic Field.” *Philosophical Transactions of the Royal Society
of London* 155 (January): 459–512.
<https://doi.org/10.1098/rstl.1865.0008>.

</div>

<div id="ref-Planck1901" markdown="1">

Planck, Max. 1901. “Ueber Das Gesetz Der Energieverteilung Im
Normalspectrum.” *Annalen Der Physik* 309 (3): 553–63.
<https://doi.org/10.1002/andp.19013090310>.

</div>

<div id="ref-Tsuchiya1986" markdown="1">

Tsuchiya, Y., E. Inuzuka, T. Kurono, and M. Hosoda. 1986.
“Photon-Counting Imaging and Its Application.” In *Photo-Electronic
Image Devices, Proceedings of the Eighth Symposium*, 21–31. Elsevier.
<https://doi.org/10.1016/s0065-2539(08)61600-5>.

</div>

</div>

---

[^1]: 1 eV (electron volt) is the amount of energy of a single infrared
    photon ($$\lambda = 1240\:\mathrm{nm}$$).

[^2]: We chose to call the B-field “*magnetic induction*”. It can be
    called “*magnetic field*” which is confusing: the H-field (in
    amperes per meter [$$\mathrm{A.m^{-1}}$$]) being also called
    “*magnetic field*” on some textbooks. The B-field may also be
    designed as “*magnetic flux density*”. The H-field may also be
    designed as the “*magnetic field intensity*” or “*magnetic field
    strength*”.

[^3]: This is a simplified form of Maxwell equations in the considered
    conditions.

[^4]: This often holds for diamagnetic and paramagnetic materials.

[^5]: The Haidinger’s brush is a noticeable example showing our eyes are
    slightly sensitive to polarisation.

[^6]: We use $$\mathbf{S}$$ notation which is widely adopted in the
    literature. It shall not be confused with the previously introduced
    Poynting vector.
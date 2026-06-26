# Medical Imaging

Created: December 26, 2025 9:41 AM
Contact: pranav.joshi@alumni.iitgn.ac.in
Creator: Pranav Joshi

- Uses of MI
    - Bilogical Systems
        - visualise anatomy (structures in body)
        - visualise physiology (physics of said structures)
        - pathology (effects of diseases on body)
    - Physical properties
        - Attenuation
        - Scattering
        - Refractive index
        - Proton spin
- X-ray pioneers
    - Wilhem Roentgen
        
        Produced and detected X rays in 1885
        
    - Thomas Edison
        
        That famous quote, "Don’t talk to me about X-rays, I am afraid of them," was said by Thomas Edison in 1903 after his assistant, Clarence Dally, died from radiation poisoning due 
        to extensive X-ray experimentation. 
        
        This led Edison to abandon his own 
        X-ray research. 
        
        Edison, who developed fluoroscopes for X-ray imaging, witnessed firsthand the devastating effects of radiation exposure on Dally (a guy, not girl), whose body suffered severe damage requiring amputations before his death.
        
- CT pioneers
    - Allan M Cormack and Godfrey Houndsfield
        - Nobel Prize in Medicine
        - 1979
    - G.N. Ramachandran and A.V. Lakshminarayan
        
        Wrote the paper “Three-Dimensional Reconstruction from Radiographs and Electron Micrographs: Application of Convolutions instead of Fourier Transform”
        
- MRI pioneers
    - Paul Lauterbur and Peter Mansfield
        
        2003 Nobel Prize in Physiology
        
- X-ray and CT vs US vs MRI
    - X-ray has images with high temporal and spatial resolution.
    - X-ray uses ionizing radiation which isn’t good.
    - US is fast and inexpensive.
    - US cannot image all body areas and is operator dependent.
    - US gives poor resolution.
    - MRI is slow and expensive.
    - MRI yields high resolution.
- EM spectrum
    
    
    | Radiation Type | Wavelength (m) | Frequency (Hz) | Black Body Temperature (K) |
    | --- | --- | --- | --- |
    | Radio | 10^3 | 10^4 |  |
    | Micro-wave | 10^-2 | 10^8 | 1 |
    | Infrared | 10^-5 | 10^12 | 10^2 |
    | Visible | 0.5*10^-6 | 10^15 | 10^4 |
    | UV | 10^-8 | 10^16 |  |
    | X-ray | 10^-10 | 10^18 | 10^7 |
    | Gamma rays | 10^-12 | 10^20 |  |
    
    The temperatures can be estimated as :
    
    $$
    T = b/\lambda = (b/c)\times f \approx (10^{-11}\text{KHz}^{-1}) \times f
    $$
    
    Note that Radio and Visible frequencies from Sun rays can penetrate Earth’s atmosphere, while other frequencies cannot.
    
- Phenomenon used for imaging
    - X-ray relies on attenuation
    - US relies of Scattering and Reflection
    - MRI relies on Hydrogen proton density
- Image reconstruction
    - This is the process of creating an image from the signals measured
    - The various types of resolution:
        - spatial (think, the $\lambda/2$ diffraction limit)
        - noise
        - contrast
        - geometric distortion
        - artifacts
    - Clinical utility is dependent on the quality of the image
- Imaging planes
    - Coronal plane : The plane separating front of your body from back-side
    - Sagittal plane : The middle plane separating left and right
    - Axial plane : Any plane that cuts the body into an upper and lower region.
- What’s special about the particular frequencies ?
    
    The imaging depends on the 
    
    - source characteristics (think, $f_0$ being resonant freq in US and the frequencies for X rays, etc.)
    - tissue interaction (think, attenuation, harmonics, heating, etc.)
    - receiver characteristics
- Effect of source size on Diffraction
    
    For a wave source of length $D$ (like a slit), 
    
    - if $D \ll \lambda$ , then broad diverging fields are produced from source
    - if $D \gg \lambda$, then focused fields ($p$ for US, or $E$ for EM rad.) are possible
    
    Since $c = f\lambda$ , for (angular) lateral resolution  $\theta = \lambda /D \iff w(x) = \lambda \cdot (x/D)$ to be better (smaller $\theta)$, we need higher $f$. It should be a no-brainer to see that larger aperture improves (lateral) resolution.
    
    Similarly, for axial resolution, which is $\text{SPL}/2$ in US, which is of form $\text{SPL}/2 = n\lambda/2 \ge \lambda/2$ , we need a lower wavelength and thus higher frequency. This $\lambda/2$ is the NOT the diffraction limit… that comes from different physics. Do note that $\lambda/2 \ll w(x)$ for most $x$ as $x_f \gg D$ usually. 
    
    For 1mm or better (axial) resolution, we need $10^{14}\text{ Hz}$ for EM waves and at least $1 \text{MHz} = 10^6 \text{ Hz}$ for US.
    
- Exceptions to resolution $\lambda/2$
    - Using UCAs, the bubbles scatter light and can thus be “seen” by the system even though they are much smaller ( $\sim \mu\text{m}$ ) than the axial (and thus lateral too) resolution of $\lambda/2$ .
    - In US, super resolution imaging we localize the miro-bubbles directly by “inverting” the point spread function of one micro-bubble. Then the image constructed from just the centers of the bubbles (highlighted as bright, sharp dots) is much clearer. This beats the diffraction limit.
- X-rays : Interaction of radiation with tissue
    
    In EM waves, there’s a law called the Beer-Lambert law that states 
    
    $$
    \nabla \cdot I = -\mu I
    $$
    
    Here $I$  is the intensity and $\mu$ is the “linear attenuation coefficient” and NOT the magnetic permeability.
    
    Solving this equation in one dimension gives us 
    
    $$
    I = I_0 e^{-\mu x}
    $$
    
    Note that this $\mu$ is different from that used for US, namely the amplitude attenuation coefficient (measured in Np/cm or just $\text{cm}^{-1}$). 
    
    This one has units of $\text{cm}^{-1}$ and is computed simply as 
    
    $$
    \mu = \ln(I_0/I)/x
    $$
    
    Also note that since $h f = \frac{hc}{\lambda}$ is energy for photons, sometimes instead of being given the frequency or wavelength, you’ll be given the energy of the photon.
    
    Also not that the value of $\mu\lambda$ is used a lot to describe “transparency” of an EM wave to a certain material. For example, high energy gamma rays have a very low value of $\mu\lambda$ and are thus “highly penetrating”
    
    Also note that “penetrating” in context of tissue and in context of atmosphere are different things. 
    
    In the atmosphere, made mostly of Nitrogen and Oxygen, the excitation energy is high and thus low frequencies are able to pass without interaction whereas high energy photons excite the electrons in the atmospheric gases instead.
    
    The same isn’t true for the tissue which is made up of a lot of things with small excitation energies, like metals, semi-metals, coordinate compounds, electrolytes, etc.
    
    Here, the high energy photons don’t get to interact.
    
    Essentially, each material has its own attenuation “spectrum”, same goes with atmosphere and tissue.
    
- Dirac Delta functions
    
    A 2D delta function $\delta_2(x,y)$ has these properties : 
    
    $$
    \int_{\mathbb{R}^2}\delta_2 (x,y) dxdy =1 \\ \delta_2(x,y) = 0 \quad\forall (x,y) \ne \vec 0 \\ \int_{\mathbb{R}^2} f(x,y)\delta_2(x-x_1,y-y_1) dxdy = f(x_1,y_1)
    $$
    
    This is a (continuous) point-impulse essentially.
    
    Similarly, a 1D delta function has 
    
    $$
    \int f(x)\delta(x-x_1)dx = f(x_1)
    $$
    
    One can define *a* 2D delta function as
    
    $$
    \delta_2(x,y) = \delta(x)\delta(y)
    $$
    
    One should note that
    
    $$
    \delta(x/a) = a\delta(x) 
    $$
    
- Line Impulse
    
    For the line $L(\theta,l): (x,y)\cdot (\cos\theta,\sin\theta) = l$ , the impulse $\delta_L(x,y)$ can be defined as
    
    $$
    \delta_L(x,y) = \delta(x\cos\theta+y\sin \theta -l)
    $$
    
    If you define
    
    $$
    u = x\cos \theta + y\sin \theta \\
    v = -x\sin\theta + y\cos\theta
    $$
    
    then we can write
    
    $$
    \int_{\mathbb{R}^2}f(\vec x)\delta_L(\vec x)d\vec x^2 = \int_v\int_uf(\vec x)\delta(u-l)dudv = \int_v f(\vec x(l,v))dv = \\ \int_v f(l\cos\theta -v\sin\theta, l\sin\theta + v\cos\theta) dv
    $$
    
    Which is clearly the line integral across $L$ .
    
- Comb function / Sampling function / Impulse train
    
    $$
    \text{Comb}(x) = \sum_{-\infty}^\infty \delta(x-n) \\ 
    \text{Comb}(x,y) = \sum_{m=-\infty}^\infty\sum_{n=-\infty}^\infty \delta_2(x-n,y-m)
    $$
    
    If you need a different sampling rate than 1, you can use
    
    $$
    \text{Comb}(x,y\,|\,\Delta x,\Delta y) = \frac{1}{\Delta x\Delta y}\text{Comb}(\frac{x}{\Delta x},\frac{y}{\Delta y})
    $$
    
    Using the $\delta(x/a) = a\delta (x)$ property, it’s easy to see that
    
    $$
    \text{Comb}(x,y|\Delta x,\Delta y) = \sum_m\sum_n \delta_2(x-n\Delta x,y-m\Delta y)
    $$
    
    A planar CCD sensor has a 2D Comb function as impulse response.
    
    Note that
    
    $$
    \int \lim_{\Delta x\to 0}\Delta x\sum f(n\Delta x) \delta(x-n\Delta x) dx \\= \lim_{\Delta x\to 0} \sum_n f(n\Delta x) \Delta x = \int f(x)dx \\\implies f(x) = \lim_{\Delta x\to 0}\Delta x\sum f(n\Delta x) \delta(x-n\Delta x)
    $$
    
    This means that
    
    $$
    f(x) = \lim_{\Delta x\to 0}\Delta x \sum_nf(x)\delta(x-n\Delta x) \\ = \lim_{\Delta x\to 0} f(x)[\Delta x\sum \delta(x-n\Delta x)] \\= f(x)\lim_{\Delta x\to 0}\Delta x \sum_n \delta(x-n\Delta x) 
    $$
    
    All this means that 
    
    $$
    \lim_{\Delta x\to 0}\Delta x\,\text{Comb}(x|\Delta x) = 1
    $$
    
- Sinc and Rect
    
    We define
    
    $$
    \text{Rect}(x) = \begin{cases}0 & |x| > 1/2 \\ 1 & |x|\le 1/2\end{cases} \\
    \text{Rect}(x,y) = \text{Rect}(x)\cdot \text{Rect}(y)
    $$
    
    And
    
    $$
    \text{sinc}(x) = \begin{cases}\frac{\sin \pi x}{\pi x} & x \ne 0 \\ 1 & x=0\end{cases} \\
    \text{sinc}(x,y) = \text{sinc}(x)\cdot \text{sinc}(y)
    $$
    
- Sine and Cosine new notation
    
    $$
    s(x) = \sin(2\pi x) \\ c(x) = \cos(2\pi x) \\ 
    s_{\vec u}(\vec x) = \sin(2\pi \vec u \cdot \vec x) \\
    c_{\vec u}(\vec x) = \cos(2\pi\vec u \cdot \vec x) \\
    s_{u,v}(x,y) = \sin(2\pi (xu+yv)) \\
    c_{u,v}(x,y) = \cos(2\pi(xu+yv))
    $$
    
    Similarly, we define new notation for complex exponential as
    
    $$
    e(x,y) = c(x,y) + js(x,y)
    $$
    
- Linear systems
    
    Suppose we have a system $S$ that does
    
    $$
    S[f(\vec x)] = g(\vec x)
    $$
    
    Then, it’s linear iff
    
    $$
    S[\sum w_if_i] = \sum_i w_i g_i
    $$
    
    where $w_i$ are constant.
    
    Namely, homogenity (linear scaling) and additivity need to be followed.
    
    Shift invariant systems further have
    
    $$
    S[f(\vec x -\vec x_1)]=g(\vec x-\vec x_1)
    $$
    
- LSI and convolution
    
    Suppose $S$ is a LSI system, and
    
    $$
    S[\delta](x)=h(x)
    $$
    
    Then
    
    $$
    S[f](a) = S[\lim _{\Delta x\to 0}\Delta x\sum f(n\Delta x) \delta(a-n\Delta x)] \\ = \lim_{\Delta x\to 0} \Delta x \sum f(n\Delta x) h(a-n\Delta x) \\ = \int f(x) h(a-x) dx \\ = (f*h)(a)
    $$
    
    Similarly,
    
    $$
    S[\delta_r](\vec x) = h(\vec x) \\\implies S[f](\vec x) = (f*_rh)(\vec x)
    $$
    
    where $r$ is the dimensions we are dealing with.
    
- Laplace and Fourier transforms
    
    Note that there are two variations. 
    
    Unilateral :
    
    $$
    F(s) = \int_0 ^\infty f(t) e^{-st}dt
    $$
    
    This is the standard LT that most EE courses use. 
    
    Bilateral :
    
    $$
    F(s) = \int_{-\infty}^\infty f(t)e^{-st}dt
    $$
    
    From this, we can also define the fourier transform as $F(j\omega)$ , which will also be either unilateral or bilateral.
    
    Most EE courses assume causal signals, and so every signal $f(t)$ is actually to be interpreted as $f(t)u(t)$ .
    
    Some extra stuff :
    
    $$
    f(t) = e^{j\omega _0 t} \iff F(j\omega) = 2\pi \delta (\omega-\omega_0) = \delta (f-f_0)
    $$
    
    where $f = \omega/2\pi$ . 
    
    For other signals, 
    
    $$
    f(t) = \frac{1}{2\pi}\int_{-\infty}^\infty F(j\omega)e^{j\omega t}d\omega \\ = \int_\infty^\infty F(j2\pi f)e^{2\pi jft}df
    $$
    
    - Proof of 2nd statement
        
        $$
        f(t) = \frac{1}{2\pi }\int_{\omega}\int_\tau f(\tau)e^{-j\omega \tau}e^{j\omega t}d\tau d\omega \\ = \frac{1}{2\pi }\int_\tau f(\tau)(\int_\omega e^{j(t-\tau)\omega}d\omega)d\tau \\ = \int_\tau f(\tau )(\frac{1}{2\pi}{\cal F}\{e^{jt\omega }\}(\tau)) d\tau \\= \int_\tau  f(\tau )\delta(\tau -t) d\tau  = f(t)
        $$
        
    
    We can extend the fourier (and laplace too) transform to 2D as
    
    $$
    F(j\omega_x,j\omega_y) := \int_{y=-\infty}^\infty \int_{x=-\infty}^\infty e^{-j(\omega_x x+\omega_y y)}dxdy
    $$
    
    Defining $\omega_x = 2\pi u$ and $\omega_y = 2\pi v$ , we get
    
    $$
    F(u,v) = \int_{\mathbb{R}^2} f(x,y)e(-(ux+vy))dxdy \\ 
    f(x,y) = \int_{\mathbb{R}^2} F(u,v)e(ux+vy)dudv
    $$
    
    It’s clear that we are essentially taking a 1D FT along the vector $(u,v)$ . The magnitude gives the argument (frequency) of the FT and the unit vector gives the direction.
    
    Properties of FT :
    
    $$
    \boxed{{\cal F}\{f(x-x_0)\}(u) =  F(u)e(-ux_0)} \\
    \boxed{{\cal F}\{af(x)\}(u) =  aF(u)} \\
    \boxed{{\cal F}\{f(R_\theta \vec x)\}(u) =  F(R_\theta \vec u)}
    $$
    
    These are called the shift, scale, and rotation properties.
    
- Sampling and Aliasing
    
    Again, remember that
    
    $$
    \text{Comb}(t|\Delta t) = \sum_n \delta(t-n\Delta t)
    $$
    
    Now, taking a FT of this, and using 
    
    $$
    {\cal F}\{\delta(t-n\Delta t)\}(\omega) = e^{-j\omega n\Delta t}
    $$
    
    we can write
    
    $$
    \hat C(\omega) = {\cal F}\{\text{Comb}(t-n{\Delta t})\}(\omega) = \sum_n e^{-j\omega n\Delta t} = \lim_{N\to \infty} \sum_{n=-N}^N e^{-j\omega n\Delta t} \\ = \lim_{N\to \infty}z^N(z^{-(2N+1)}-1)/(z^{-1}-1) \\ = \lim_{N\to \infty }\frac{z^{-(N+1/2)}-z^{(N+1/2)}}{z^{-1/2}-z^{1/2}} \\ = \lim_{N\to \infty}\frac{\sin(\omega\Delta t(N+1/2))}{\sin(\omega\Delta t/2)}
    $$
    
    This is clearly periodic (in $\omega$) with a period of $2\pi/\Delta t$ and $\hat C(0) = \infty$ . 
    
    Unfortunately, it’s divergent. 
    
    We’ll need some other way … How about we start with a function like $\sum_n \delta(t-n\Delta t)f(n\Delta t)$ where $f$ *is* a smooth decaying function. 
    
    First, define
    
    $$
    CF(t) = \text{Comb}(t)\cdot f(t) = \sum_n \delta(t-n\Delta t) f(n\Delta t) = \sum_n \delta(t-n\Delta t)f[n]
    $$
    
    Then, we define
    
    $$
    \hat {CF}(\omega) = {\cal F}\{\sum_n \delta (t-n\Delta t)f[n]\}(\omega) \\= \sum_n f[n]e^{-j\omega n\Delta t}
    $$
    
    That’s .. the DTFT…
    
    Consider
    
    $$
    f[n] = e^{-|n|\sigma\Delta t}
    $$
    
    where $\sigma > 0$ . Then we have
    
    $$
    \hat {CF}(\omega) = \lim_{N\to \infty} (1 + \sum_{n=1}^N e^{-n\sigma \Delta t}(e^{-nj\omega \Delta t} + e^{nj\omega \Delta t})) \\ = -1+\lim_{N\to \infty}\sum_{n=0}^N (z^{-n} + \bar z^{-n}) \\ = -1 +\lim_{N\to \infty}(\frac{z^{-(N+1)}-1}{z^{-1}-1} + \frac{\bar z^{-(N+1)}-1}{\bar z^{-1}-1}) \\ = -1 + 2\lim_{N\to \infty} \Re (\frac{z^{-(N+1)}-1}{z^{-1}-1})
    $$
    
    Here $z = e^{s\Delta t}$ where $s = \sigma + j\omega$ . 
    
    $$
    \hat {CF}(\omega) = -1 - 2 \Re (z/(1-z))
    $$
    
    Now, if I set $\sigma \to 0$ …
    
    $$
    \hat {C}(\omega) = -1 +2\Re (z^{1/2}/(z^{1/2}-z^{-1/2})) = -1 + 2 \Re (e^{j\omega\Delta t/2}/(2j\sin(\omega \Delta t/2))) \\ = -1 + 1 = 0 \, \forall  \omega \text{ s.t. } z \ne 1
    $$
    
    Nice. That’s much better
    
    And $z = 1$ when $\omega = 2m\pi/\Delta t$
    
    in which case we can use the earlier idenity to say that $\hat C(\omega) \to \infty$ .
    
    Now, all that is remaining is to prove that the integral is finite.
    
    This again doable by first using $f(n\Delta t) = e^{-\sigma|n|\Delta t}$ to get the integral of $\hat {CF}$ over one period, showing it is 0 , and then letting $\sigma \to 0$ .
    
    After all that math, what we arrive at, is
    
    $$
    \hat C(\omega) = \frac{2\pi }{\Delta t}\sum_k \delta (\omega -\frac{2\pi k}{\Delta t})
    $$
    
    Essentially, what we have proved is that
    
    $$
    \text{DTFT}\{f[n]\}(\omega) = {\cal F}\{\text{Comb}(t|\Delta t)\cdot f(t)\}(\omega) = \hat {CF}(\omega)  \\= \frac{1}{2\pi}\hat C (\omega) * F(\omega)  \\ = \frac{1}{\Delta t}\sum _k F(\omega - \frac{2\pi k}{\Delta t})
    $$
    
    So clearly, if $F(\omega) = 0$ where $|\omega| \ge \pi /\Delta t$ , then 
    
    $$
    \text{DTFT}\{f[n]\}(\omega) = \frac{1}{\Delta t} F(\omega)
    $$
    
    in the range $|\omega | < \pi /\Delta t$
    
    This is basically the Nyquist criterion.
    
    The same also applies to DFT, which is done for periodic signals mainly. For aperiodic signals, you get a sampled version of the DTFT of the signal (assuming rest is 0) on doing the DFT.
    
    Now, we can also extend the Nyquist criterio to the 2D DTFT, which is just 2 one-dimensional DTFTs. 
    
    All you have to do is enforce Nyquist criterion for both axis, namely $u \le \frac{1}{2\Delta x}$ and $v \le \frac{1}{2\Delta y}$ , both for the input (2D) signal and for the DTFT range.
    
- Image Quality
    
    This is explained via
    
    - SNR
    - Constrast , CNR
    - Resolution (axial, lateral, temporal)
    - Artifacts
    - Distortion
    - Precision (Quantitative Accuracy)
    
    All these are governed by the physics and engineering of the US system.
    
- Task oriented metrics
    
    In opposition to the image quality metrics, you have the task related metrics such as
    
    - sensitivity $= \Pr (T^+|D^+)$
    - specificity $= \Pr(T^-|D^-)$
    - PPV = $\Pr (D^+|T^+)$
    
    The 1-specificity vs sensitivity curve is called the ROC, and the area under that, AUC is used as a metric. 
    
- Contrast
    
    In US, we defined it as $S_r - S_b$ or $20\log_{10}(S_r) - 20\log_{10}(S_b)$ on the decibels scale.
    
    From that, we define CNR as
    
    $$
    \frac{|S_r-S_b|}{\sqrt{\sigma_r^2 + \sigma_b^2}}
    $$
    
- Michelson Modulation
    
    Suppose you have an object to be imaged can be decomposed into more “images” using the 2D continuous FT (similar to how we do it with SVD, but in continuous domain) .
    
    These “images” as the eigenfunctions of the (LSI) ultrasound system and we can do all of our maths considering just one such (general) “image” and then adding the effects of all “images”.
    
    Again, just to be clear, for a single eigenfunction, consider
    
    $$
    R(x,y) = A + B\sin(kx)
    $$
    
    This will create an image $P(x,y)$ and we will have
    
    $$
    P(x,y) = (\text{PSF}*R)(x,y) \iff \\
    \hat P(u,v) = \hat {\text{PSF}}(u,v)\cdot \hat R(u,v)
    $$
    
    Here $P(x,y)$ will actually be sampled and so $\hat P(u,v)$ is obtained from the 2D DTFT of $P[n,m]$ , but these details aren’t important.
    
    Now, with this, we’ll have
    
    $$
    \hat P(u,v) \\= \hat {\text{PSF}}(u,v)\cdot [A\delta_2(u,v) + (B/2j)\delta_2(u-k,v) -(B/2j)\delta_2(u+k,v)] \\ = [A \cdot \hat {\text{PSF}}(0,0)] \delta_2(u,v) + [(B/2j)\cdot \hat{\text{PSF}}(k,0)]\delta_2(u-k,v) - [(B/2j)\cdot \hat{\text{PSF}}(-k,0)]\delta_2(u+k,v)
    $$
    
    But since $\hat {\text{PSF}}$ is the FT of a real valued function, thus $\hat {\text{PSF}}(-k,0) = \hat {\text{PSF}}(k,0)$. So, we can write :
    
    $$
    \hat P(u,v) = \\ [A\cdot \hat{\text{PSF}}(0,0)]\delta_2(u,v) + [(B/2j)\cdot \hat{\text{PSF}}(k,0)](\delta_2(u-k,v) - \delta_2(u+k,v))
    $$
    
    From this, we have
    
    $$
    P(x,y) = A\cdot \hat{\text{PSF}}(0,0) +B\cdot \hat{\text{PSF}}(k,0)\sin(kx)
    $$
    
    Now, we can assume WLOG that the PSF is normalised (since $P$ only needs to capture relative magnitudes and thus magnitudes can be scaled) such that $\hat{\text{PSF}}(0,0) =1$ and $\hat{\text{PSF}}(k,0) := \text{OTF}_x(k)$ .
    
    This gives
    
    $$
    P(x,y) = A + B\cdot \text{OTF}_x(k) \sin(kx)
    $$
    
    Here, OTF is the optical transfer function.
    
    Why is it named so ? 
    
    Because for $R(x,y) = A + B\sin(kx)$ , we define “complex modulation” as $B/A$ . Then, for $P(x,y)$ , one will have complex modulation of $(B/A)\cdot (\hat{\text{PSF}}(k,0)/\hat{\text{PSF}}(0,0))$ . 
    
    So, defining 
    
    $$
    \text{OTF}_x(k) = \frac{{\cal F}\{\text{PSF}\}(k,0)}{{\cal F}\{\text{PSF}\}(0,0)}
    $$
    
    we can simply write the new complex modulation as OTF times old one. 
    
    Now, for actual definition of modulation, you remove any phase and define it as $|B/A|$ . This leads to the Modulation Transfer Function
    
    $$
    \text{MTF}_x(k) =|\text{OTF}_x(k)|
    $$
    
    The phase component of OTF is sometimes reffered to as the Phase Transfer function (PTF).
    
    Now, what’s the significance of MTF ?
    
    For a perfect US system, we have a delta-like PSF and thus the FT is a uniform distribution. 
    
    Thus, for a perfect US system, we have a MTF of 1 for all frequencies that satisfy the Nyquist criterion.
    
    One should note that the MTF is basically the frequency response, just scaled. All the fancy “modulation” vocabulary is not important.
    
    Note that one need not use the sampled $P[n,m]$ to define the PSF and thus its DTFT. This is only when we want to think of the full system. Usually, MTF is defined only for the analog part (band pass filters and stuff) and not the full system. Of course, we still have sampling in the y direction, (with interval the same as pitch) , but for the x direction, you can define the MTF using only analog signals. And in that case, we want it to be a box (1 in range, 0 outside).
    
    Another way to define modulation is
    
    $$
    \frac{I_\text{max}- I_\text{min}}{I_\text{max}+ I_\text{min}}
    $$
    
    where $I$ is the pixel intensity or the corresponding (amplitude) reflectivity. 
    
    Thus, for the $R(x,y)$ we are dealing with, $I_\text{max} = |A| + |B|$ and $I_\text{min} = |A| -|B|$  
    
    This makes modulation the same as $|B|/|A|$ .
    
- Cascade of systems
    
    While it’s easy to think of PDFs as signals and use things like convolutions to do stuff like generating PDF of a sum of random variables, it’s un-intuitive to think of signals as PDFs.
    
    But the math is exactly the same.
    
    Every stage of the US chain has a PSF associated with it which produces a “spread” or strength $R_i$ , that is just the root-mean-squared-deviation from the source. One can think of the PSF as a PDF of sorts.
    
    Then, it’s easy to see that convolving with many PSFs (or in simple terms, passing through the components of the chain), we get the final spread of $R = \sqrt{\sum_i R_i^2}$ .
    
    This is what that we use as $R$esolution.
    
    Now although the spreading is deterministic, we can think of it as just probabilistic spreading (random walk) with very large sample size. So of course, noise (which actually *is* random) can also be a system in the $R$ equation. Although usually it’s not modeled like that, but rather as a probabilistic signal added. Namely, 
    
    $$
    P(x,y) = (R*\text{PSF})(x,y) + N(x,y)
    $$
    
    While you may think that “oh, so $P$ is just sum of two r.v. then”, that’s not correct. The first term have a “spread” given by the equation, which is NOT the standard deviation in the amplitudes themselves. Here, the sum of variances will apply to amplitudes and not to the location of points (resolution) in the image.
    
- SNR
    
    It’s the ratio of amplitude of main frequency and “amplitude” of noise (sum of other frequencies). 
    
    Note : This is different from using $\Delta f$ or $\sigma_f$ . That was good for the transmission phase, and for Rayleigh scattering and even for CNR where we were dealing with the envelope strength. But now, we are dealing with a varying function that has noise added, and not a constant signal for a pixel with noise that can be characterised via the variation.
    
    $$
    \text{SNR} = \frac{A_f}{A_N}
    $$
    
    Here we assume noise is of a particular frequency ? I honestly don’t know what’s going on..
    
    We usually express SNR in dB as $20\log_{10}(\text{SNR})$ .
    
- Attenuation and Absorption
    
    Since $I(x+\Delta x,t)= I(x,t)e^{-2\mu \Delta x} \approx (1-2\mu\Delta x)I(x,t)$ , basically, $2I(x,t)\mu\Delta x$ is the amount of energy absorbed per unit time by the material when the wave travelled by distance $\Delta x$. Time averaging this gives us $2I_\text{TA}(x)\mu \Delta x$. This will cause a temperature increase of $\Delta T$ which follows the heat capacity equation of $\rho C_p \frac{\Delta T}{\Delta t} = 2I(x)\mu$ where $C_p$ is the specific heat capacity of the material. This $2I(x)\mu$ thing is often denoted as $Q$, which means “heat flow” . Also, while using $\mu$ is theoretically correct assuming absorption as the reason for attenuation, practically there is also scattering which attenuates. So the true “absorption coefficient”, often (badly) denoted by $``\alpha"$ is actually lower. I won’t use the $\alpha$ notation to keep my sanity. Instead, let’s say the absorption coefficient is $\mu_h$ . Also, we can more to the derivative $\theta = \frac{dT}{dt}$.
    
    The final equation, without considering any heat conduction is :
    
    $$
    Q(x) = 2\mu_hI(x) = \rho C_p \theta
    $$
    
    Of course, one also needs to worry about the heat conduction and write a proper differential equation and so this will work at the very start when the temperature gradient isn’t there.
    
- Field II
    
    This is a simulation program, that simulates US systems. 
    
    Unlike Phantoms, which are physical materials, this simulation is entirely numeric.
    
    It uses the spatial impulse response (PSF) method and assumes linear accoustics. 
    
    It doesn’t take into account reverberations or other artifacts.
    
- X-rays
    - Use Bohr’s model rather than MOT for modeling
    - Radio-active decay creates Gamma rays, not X-rays.
    - X-rays have wavelength in $10^{-10}\text{m}$ to $10^{-12}\text{m}$ range.
    - X-rays used in medical imaging have energy range of $25 \text{ keV}$ to $500 \text{ keV}$ , which corresponds to $1240 \text{ eV nm} / 25\text{ keV} = 4*124 * 10^{-13} \text{m} \approx 0.5 * 10 ^{-10} \text{m}$ to $2.5\times 10^{-12}\text{m}$  .
    - Shells are K,L,M (forget about orbitals and spin for now)
    - The $n^\text{th}$ shell has $2n^2$ electrons (very basic, ik..)
    - Characteristic X-rays are result of electron in higher energy level going to lower energy level. Since the energy difference is not variable, it’s “characteristic” of the material. This usually happens when an electron in an inner shell gets knocked off as a result of collision with a high energy electron.
    - Bremsstrahlung X-rays are generated when an incoming (free) electron is decellerated due to interaction with the atom. This doesn’t change anything in the atom, but still generates EM waves which account for the lost kinetic energy.
    - *Bremsen* = braking
    *Strahlung* = radiation
    Bremsstrahlung = brake-ing radiation
    - Charge of electron is $e = 16 \times 10^{-20}\text{ C}$
    - Plank’s constant is $h \approx 2\pi \times 10^{-34}\text{Js} \approx 4 \times 10^{-15} \text{eVs}$
    - Note that the valence electrons aren’t responsible for characteristic X-ray creation, but rather the inner shell electrons.
    - Binding energy is energy needs to Ionise the atom.
    - X-rays are produced when electron emitted from the cathode of a vaccum tube (hence cathode rays) get accelerated due to a potential difference and then reach the anode (usually Tungsten) where they decelerate, creating Bremsstrahlung X-rays. Of course, characteristic X-rays are also generated.
    - Accounting for binding energy needed to free electrons from the shell at the cathode, the voltage that must be used to produce electrons is in the range of 30 to 150 keV. Again, remember that for voltage $V$ and binding energy $\phi$ , we have the braking radiation X-ray photons of energy $E =h\nu = q_eV - \phi$
    - The actual current through the vaccum to the anode surface is only 50 mA to 1.2 A out of the 5A or so current that is actually generated (and passes through the metal casing that is grounded (at 0V).
    - Only 1% of the (kinetic) energy that the electrons gain is converted to X-rays. Rest is converted to heat.
    - 80% of X-ray energy is Bremsstrahlung, while 20% is characteristic X-rays.
    - For safety purposes, the set-up is usually encased in a lead block (high electron density and thus high attenuation), save for an aperture when a filtering material is present that lets only X-rays passed.
    - The cathode is often immersed in an oil bath. This is for 2 reasons :
        - It is an insulating substance and prevents short circuits between the metal housing and the cathode (which has a very low potential)
        - Just like water, it can conduct and convect the heat away from the system to the surrounding as well as absorb the heat. This is needed since X-ray generation produces lots of heat.
    - The anode is often shaped as a plate attatched to a motor that rotates it (about its axis), with the cathode rays falling at a spot that is off-center.  This is again, for cooling purposes.
- Anti scatter grid
    
    Often, just outside the vaccum tube setup, we have an anti-scatter grid, which is an array of lead strips that catch any photons not moving at the intended angle.
    
    ![image.png](Medical%20Imaging/image.png)
    
    Suppose the kerf (interspace width) is $d$, the lead element width is $t$ and the pitch is $b = d+t$ , then we have:
    
    - Grid Ratio = $h/d$
    - Grid Frequency = $1/b$
    
    The parameters that are of interest:
    
    - Selectivity: The ratio of primary radiation (from source) transmitted to the scattered radiation transmitted
    - Grid Conversion Factor (GCF): Required increase in exposure/dose (measured as $mAs$) when using the grid (to compensate for photons absorbed by the grid) to when not using the grid.
- Effects of ionising radiation
    - Direct Damage
        
        Here, the double stranded helix structure of DNA breaks and thus he cell dies or is unable to function (remember, RNA is derived from DNA, which is then used to make proteins. Having wrong DNA means the whole thing is messed up)
        
    - Indirect Damage
        
        Here, the radiation first creates free radicals (think, $\text{O}_2^-{\large \cdot}$ or $\text{OH}{\large \cdot}$ , both of which are in equilibrium with $\text{H}_2 \text{O}_2$)
        
        Then, these free radicals cause a chain reaction (the same kind that causes alcohols to explode and makes peroxide a good cleaning substance) via the radical mechanism.
        
        This then causes damage to the DNA.. and thus the cell eventually stops functioning and dies.
        
- Radiation safety (radiation dosage/exposure)
    
    Let $E$ be the “exposure”, $T$ be the time period of exposure and $d$ be the distance from the source and $S$ be the effect (reduction in effective exposure) of shielding, which is fixed protective barriers and personal protective equipment. Then, we have :
    
    $$
    E \propto \frac{T}{Sd^2}
    $$
    
- X-ray imaging
    
    X-ray beams that are passed through the body are partially absorbed (attenuated)
    
    The surviving strength is captured on a X-ray sensitive film. 
    
    Lower strength (surviving) beams/rays give a white color (no change in color) while high strength rays cause the film to blacken. This is what used to be the X-ray “image”/photo.
    
    In the X-ray image, high attenuation (usually high density) objects like bones appear brighter (white) and low attenuation regions (say, the lungs) appear black.
    
    This practice is called radiography (since we use radiation ?)
    
    An upgrade to the film is Computed Radiography (CR) which uses photostimulable phosphor plates that record the X-rays (chemically) temporarily and then are *read* digitally using lasers. These plates are re-usable.
    
    The latest way to image is using Digital Radiography (DR) in which electronic “flat-panel” detectors directly capture X-rays and the signal is converted to digital data. This is similar to what happens in a camera, in that we use photo-diodes and thin-film-transistors (TFT) to get voltages from light intensity.
    
- Speed of electron in vaccum tube
    
    While for low voltages, of can simply use $\frac{1}{2}m_ev^2 = q_e V - \phi$ to get the speed of electron just before it hits the anode, for very high voltage, you need special relativity and the correct equation is
    
    $$
    \frac{1}{2}\frac{m_{e,0}}{\sqrt{1-v^2/c^2}}v^2 = q_e V -\phi
    $$
    
- Mass attenuation coefficient
    
    It is simply $\mu/\rho$ .
    
    As a reminder, $\mu$, the linear attenuation coefficint, is for intensity when talking about EM waves and for amplitude in US. 
    
- Photo-electric attenuation
    
    As you might remember, the energy at different energy levels is proportional to $Z^2$ for an atom. 
    
    It happens (for reasons that are too deep to go into right now), the normal means of attenuation of X-rays, namely the photoelectric effect (same as one used for generation of characteristic X-rays) is dependent on the atomic number. 
    
    Namely, the probability of an photon with energy $E$ ionising an atom  is proportional to something like $Z^4/E^3$. 
    
    The attenutation coefficient $\mu \propto Z^{2.94}$ .
    
    This works for a single atom substance. But for complex organic molecules, not really. So, we use an “effective” atomic number for a molecule computed as 
    
    $$
    Z_\text{eff} = \sqrt[n]{\sum_i f_iZ_i^n}
    $$
    
    Here, $Z_i$ is the atomic number of one of the atoms (not type of atom, but like, a single atom) and $f_i$ is the fraction of total electrons in the molecule bound to that atom (no, it’s not just $Z_i/\sum_i Z_i$ since we also have to include partial charges, ionic compound atoms, etc.) . Finally, $n$ is a fixed number, usually $n = 2.94$ .
    
    Note that this $Z_\text{eff}$ is VERY DIFFERENT from the one studied in chemistry for the sheilding effect of non-valence electrons.
    
    Again, all this is when attenuation happens via photo-electric effect. This is NOT the main mechanism of attenuation when the energy levels (energy of single photon) of the X-rays cross 100 keV or something. For that range, the main mechanism is Compton scattering, which doesn’t depend on $Z_\text{eff}$ all that much.
    
    As photon energy increases, the probability of the photon interacting with the tissue decreases and the photons pass through. That’s why gamma rays are highly penetrating. 
    
    Again, the metric used for this (what is more penetrating) is $\mu \lambda$ and not just $\mu$ .
    
- Rayleigh Scattering
    
    If the object size (in the tissue) is vely small (much smaller than X-rays), then we get Rayleigh scattering. Of course, considering we are heading with *X-rays* and not light, this doesn’t happen a lot. But still, the formula that governs it is
    
    $$
    I_\text{scat}(r,\theta) \propto I_\text{inc}\frac{nk^4}{r^2}(1+\cos^2\theta)
    $$
    
    Note that this is different from the $(1-\frac{3}{2}\cos\theta)$ thing that we had for Rayeligh scattering in US.
    
    Apart from that, it’s all the same.
    
    Also, there’s a contribution that comes from the refractive index of the small particle, which is too complicated to get into right now.
    
- Compton scattering
    
    Unlike Rayleigh scattering, where the wave is sent in all directions, or reflection where waves are reflected following snell’s law, compton scattering deflects the photon and changes its energy (thus the frequency too). 
    
    The equation governing this is :
    
    $$
    E' = \frac{E}{1+(1-\cos\theta)E/(m_ec^2)}
    $$
    
    Here $m_ec^2 \approx 511 \text{ keV}$ is the mass energy of an electron.
    
    This equation can be rewritten in a better form:
    
    $$
    {\Delta \lambda} = {\lambda'-\lambda}= (\frac{h}{m_ec})(1-\cos \theta)
    $$
    
    The probability of this interaction happening is proportional to the electron density of the material.
    
- Pair production mode of attenuation
    
    This happens when the energy of photon is very high, namely above $2m_ec^2 \approx 1.022 \text{ MeV}$
    
    This isn’t applicable for medical X rays which go to 500 keV maximum.
    
- Intensity and Number of photons
    
    Remember than the intensity of the beam is directly proportional to number of photons per unit area. So when we write $I = I_0 e^{-\mu x}$ or $\frac{dI}{dx} = -\mu I$ , we are implicitly writing $N = N_0 e^{-\mu x}$ .
    
- Half Value layer
    
    This is the thickness of a material which attenuates the X-rays so that the intensity (or number of photons) decreases to half the value before this layer. Essentially, $e^{-\mu \cdot \text{HVL}} = 1/2$ . This gives us
    
    $$
    \text{HVL} = \frac{\ln 2}{\mu} \approx \frac{0.693}{\mu}
    $$
    
    If the matrial doesn’t have uniform attenuation, we need to instead use
    
    $$
    \frac{I(x)}{I_0} = \frac{N(x)}{N_0}= \exp(-\int_0^x \mu(y)dy)
    $$
    
- CT
    
    The CT scanning machine is a big cyclinder, with a rotating part inside that has the X-ray source on one end and curved detectors on other end. 
    
    The detectors don’t create an image, but rather 1D data, which is basically the attenuation suffered by the rays before reaching the detector. This is in decibels of course. 
    
    One can assume that the “attenuation” over the tissue adds linearly since we are working over the dB scale (or at least, thinking in terms of exponential factors) giving 
    
    $$
    I(r,\theta) = I_0 e^{-p_(r,\theta)}
    $$
    
    Basically, suppose the X-ray source is currently at at angle $\theta$ to a reference array (the y axis usually), and the particular ray (among many emitted by the source when it produces a pulse) that we want to focus on is $r$ distance away from the center (origin). Then, the attenuation (the negative exponent only) will be
    
    $$
    p(r,\theta) =\int_{\mathbb{R}^2} \mu(x,y)\delta_{L(r,\theta)}(x,y)dxdy
    $$
    
    One can set $\mu(x,y) = 0$ where $\sqrt{x^2 + y^2} > R$ , the radius of the cylinder.
    
    This is a line integral. Try to remember the line impulse stuff that we did. Here
    
    $$
    \delta_{L(r,\theta)}(x,y) = \delta(x\cos\theta + y\sin\theta - r)
    $$
    
    For one such pulse, we get $p(r,\theta)$ for many $r$ (depends on how big the x-ray detector is) and a single $\theta$. Then, with multiple of these lines for many $\theta$, we get a full image called a sinogram. 
    
    Why a sinogram ? Because for a single object inside the cylindrical space, the image *looks* like the (shifted) graph of $a\sin(\theta)$ where $a$ is the distance of the object to the center.
    
    One should note that we DON’T have a graph .. we have an *image* , a 2D function $p(r,\theta)$ . 
    
    This is called the radon transform of $\mu(x,y)$ .
    
    Now, taking an “Inverse Radon Tranform” of $p(r,\theta)$ , we can recover $\mu(x,y)$, which is what we really want. 
    
    Now, this is just a 2D disc kind of image. of a cross section that would usually be un-imagable (think, the pelvic bones from a superior view)
    
    But if we repeat this same thing for different $z$, then we get a 3D distribution of $\mu(x,y,z)$ stored as a 3D tensor of course. 
    
    This is really useful since from this, we can visualise the insides of the body at any angle we want and thus diagnose easily.
    
- Inverse Radon transform
    
    The Radon Transform equation is
    
    $$
    p(r,\theta) = \int_{\mathbb{R}^2}\mu(x,y)\delta(x\cos\theta+y\sin\theta -r)dxdy
    $$
    
    From this, we can get
    
    $$
    b(x,y) = \int_{\theta=0}^\pi p(x\cos\theta +y\sin\theta,\theta)d\theta
    $$
    
    Basically, for each angle $\theta$ , we compute the distance $r = x\cos\theta + y\sin\theta$ from the origin of the ray passing through a point $(x,y)$ when the rays make angle $\theta$ to the y-axis. Then, we know that $\mu(x,y)$ contributes to $p(x\cos\theta+y\sin\theta,\theta)$. By summing all $p(x\cos\theta+y\sin\theta,\theta)$ for all $\theta$, the contribution scales more as compared to contributions of other points. 
    
    This is called the back-projection. 
    
    As you might have guessed, we will get a very noisy image after this. But thankfully this noise has a mathematical structure. 
    
    Essentially,
    
    $$
    b(x,y) = (\mu *B)(x,y) \\ \text{where }\;B(x,y) =\frac{1}{\sqrt{x^2+y^2}}
    $$
    
    - Proof
        
        $$
        b(x_0,y_0) = \int_{\theta=0}^\pi p(x_0\cos\theta+y_0\sin\theta,\theta)d\theta \\ =\int_0^\pi \int_{\mathbb{R}^2}\mu(x,y) \delta((x-x_0)\cos\theta +(y-y_0)\sin\theta)dxdyd\theta
        $$
        
        Define
        
        $$
        \mu_0(x,y) = \mu(x+x_0,y+y_0)
        $$
        
        With this, we can write
        
        $$
        b(x_0,y_0) = \int_0^\pi \int_{\mathbb{R}^2}\mu_0(x,y) \delta(x\cos\theta + y\sin\theta)dxdyd\theta \\ = \int_0^\pi \int_{\mathbb{R}^2}\mu_0(\vec x)\delta(\vec x\cdot \hat e_\theta)d\vec x^2 d\theta
        $$
        
        Now, let’s express $\vec x =r \hat e_\phi$ . This gives
        
        $$
        b(x_0,y_0) = \int_{\theta=0}^\pi\int_{\phi=0}^{2\pi} \int_0^\infty\mu_0(r\hat e_\phi) \delta(r\cos(\phi -\theta)) rdrd\phi d\theta
        $$
        
        Now, change the integral order to bring $\theta$ inside, giving us
        
        $$
        b(x_0,y_0) = \int_0^{2\pi}\int_0 ^\infty \mu_0(r\hat e_\phi) [\int_0^\pi \delta(r\cos(\phi -\theta)) d\theta] rdrd\phi
        $$
        
        Let’s assume that $\phi \in (-\pi/2,\pi/2)$ . It it’s not, we’ll only have a change in the sign, nothing much. 
        
        Now, this inner integral is what we are interested in.
        
        $$
        B(r,\phi) =\int_0^\pi \delta(r\cos(\theta -\phi))d\theta
        $$
        
        Since $|\theta -\phi| = \pi/2$ only for one $\theta$ as $\phi \in (-\pi/2,\pi/2)$ so we can reduce the range of the integral to an arbitrarily small amount using $\delta(r\cos(\theta-\phi)) = 0$ when $\theta -\phi \ne \pi/2$and substitute $u = r\cos(\theta-\phi)$ for that range . Doing the u-substitution, we get No…
        
        $$
        B(r,\phi) = -\int_{\epsilon}^{-\epsilon} \delta(u)\frac{1}{r\sin(\theta(u)-\phi)}du \\= \int_{-\epsilon}^{\epsilon} \delta(u)\frac{1}{r\sin(\theta(u)-\phi)}du
        $$
        
        Here $\epsilon$ is any sufficiently small number. 
        
        Now, since $u = 0 \iff \theta -\phi = \pi/2$ , we can write $B(r,\phi) = 1/r$ . 
        
        Using symmetry arguments , one can show that this works for $\phi \in (\pi/2,3\pi/2)$ too.
        
        Then, using continuity, one can show that this works for $\pi/2$ too and thus, for $(-\pi/2,3\pi/2)$. Then again, using symmetry arguments, one can say that it works for $-\pi/2$ and thus, the full 360 degree range. 
        
        Now, coming back, we have
        
        $$
        b(x_0,y_0) = \int_0^{2\pi}\int_0 ^\infty \mu_0(r\hat e_\phi) \frac{1}{r} rdrd\phi \\ = \int_{\mathbb{R}^2} \mu_0(\vec x)\frac{1}{|\vec x|} dxdy \\ = \int_{\mathbb{R}^2}\mu(\vec x + \vec x_))\frac{1}{|\vec x|}dxdy \\ = \int_{\mathbb{R}^2}\mu(x,y)\frac{1}{|\vec x -\vec x_0|} dxdy
        $$
        
        Since we have $B(\vec x) = 1/|\vec x|$ , so of course
        
        $$
        B(\vec x_0-\vec x) = \frac{1}{|\vec x_0 -\vec x|} =\frac{1}{|\vec x -\vec x_0|}
        $$
        
        And thus, 
        
        $$
        b(x_0,y_0) = \int_{\mathbb{R}^2}\mu(\vec x)B(\vec x_0 -\vec x)d\vec x^2 \\ =(\mu *B)(x_0,y_0)
        $$
        
    
    Now, with this, can write
    
    $$
    {\cal F_2}\{b\}(\vec \omega) = \hat b = \hat \mu \cdot \hat B
    $$
    
    It happens that
    
    $$
    {\cal F_2}\{B\}(\vec \omega) = \frac{1}{|\vec \omega|}
    $$
    
    What this means is
    
    $$
    \hat \mu = \hat b |\vec \omega|
    $$
    
    Once we have this, we can just compute the iFFT and get $\mu$ .
    
    That is how the intuitive thing goes, but in practice, a different algorithm is used, which involves back-projecting 
    
    $$
    Q(r,\theta) \\= {\cal F^{-1}_\omega}\{|\omega|\hat p(\omega,\theta)\} \\= {\cal F^{-1}_\omega}\{ |\omega|{\cal F_r}\{p(r,\theta)\}(\omega)\}
    $$
    
    to get $\mu(x,y)$ . Note that the FFTs here are 1D as opposed to 2D. 
    
    While this actually no change in time complexity if everything is done using software, on hardware, this algorithm is much better since we can parallelize and it also gives better image quality since there’s intertwining of the 1D rows, causing lower interpolation errors.
    
- Uses of CT
    
    CT is used to do angiography (imaging blood vessels), often for the coronary artery (connected to heart).
    
    Iodine based contrast agents can be used to visualise better. To do this, a catheter is inserted *inside* the blood vessel which injects a dye that enables high speed x-ray videography.While this may seem pretty messed up, it’s actually the standard medical procedure. What’s more fucked up is that this is often done to image vessels in the heart. Oh, and this catheter doesn’t go in in a straight-forward manner.. nope. 
    
    ![image.png](Medical%20Imaging/image%201.png)
    
    Honestly, I wish I had never read about this stuff..
    
    Now, you may wonder .. why go through all this trouble ? 
    
    Coronary artery can have calcification which builds up as a plaque. This can’t be imaged from the outside coz rib cage. And this can’t be imaged via normal CT without contrast agents coz it’s too complex and we need high temporal resolution. So, to get a direct and final image/video, we do this fucked up procedure of inserting stuff into the body.
    
- MRI
    - Non-ionizing radiation (unlike X-rays)
    - Uses proton spin in H atoms, which is either $+1/2$ or $-1/2$ .
    - Uses radio frequency (10-100 MHz) EM waves too
    - Can image full body as opposed to just a specific part
    - Spatial Resolution is on the scale of millimeters
    - Really good contrast.
    - Uses magnetic fields of 1 to 3 Tesla of strength (Note that 1T = 10000 Gauss)
    - Stronger magnetic fields (7 to 9 T) give sharper images, which can be used for small animal imaging.
    - Acquisition isn’t fast like X-ray or even US.
    - Very bulky and expensive set-up making it useless for NDT usage.
    - Uses superconduction (< 4K temp. electromagnets) to create strong magnetic fields with low power usage.
- Protons are magenets
    
    Proton spins are directed at random directions naturally in body. Under a strong magnetic field, the spins all align with the magnetic field, in either parallel (more common, stable equilibrium) or anti-parallel (unstable) positions.
    
- Gyromagnetic Precession
    
    Note that while the parallel and anti-parallel states are equilibria, there is another kind of steady state. Fist, let’s assum that the strong magnetic feild that we are using is $B_0\hat z$ . Now, suppose the magnetic moment of the proton is $\vec \mu$ , then the torque that is generated due to the magnetic feild is $\vec \mu \times B_0\hat z$ which then acts like a “centripital” accileration (where $\vec \mu$ is the velocity), because the angular momentum of the proton is along $\vec \mu$. Thus, the spin rotates about the z-axis, at some inclination $\theta$ and with angular frequency $\omega = \frac{d\phi}{dt}$ where $\phi$ is the angle that the spin vector’s projection on the x-y plane makes with the positive x-axis. Here, $\theta$ doesn’t change. 
    
    An interesting this is that the magnetic field induced due to the dipole moment $\vec \mu$ has its x component (and y too) oscilating in a sinusoidal fashion, similar to what happens in a turbine. This can be used to generate current in a coil. 
    
    We have 
    
    $$
    \omega = \gamma B \\ 
    f = \frac{\omega}{2\pi} = \frac{\gamma}{2\pi}B
    $$
    
    Here, $\gamma$ is the gyromagnetic ratio, given in (radians/s)/T . The $(\frac{\gamma}{2\pi})$ thing has units of MHz/T and is actually what is reported. It has a value of 42.58 MHz/T .
    
    And the frequency $f$ is called the Larmor frequency. 
    
- QM and time/ensemble average
    
    Actually, due to QM, we have $|\sin(\theta)| = 1/\sqrt{3}$ for the spin regardless of its state. Here $\theta$ is the angle made with the x-y plane. 
    
    This angle is around 54 degrees.
    
    So essentially, the spin vector is rotating on a cone around the z-axis.
    
    This isn’t a problem since the phase (starting $\phi$) is a random variable and ensemble averaging $\vec \mu$ over a block of the material gives us a magnetization purely in the z direction. This is because $\theta = \arccos(1/\sqrt 3)$ is more stable (low energy) than $\theta = -\arccos(1/\sqrt 3)$ .
    
    This is a problem since now the case with spin rotating in the xy plane with be ensemble averaged to 0 and produce no reading. 
    
    To change this, we use another magnetic field.
    
- RF Pulse
    
    Now, we produce another feild $\vec B_1 = B_1 \hat e_\phi$ where $\hat e_\theta = (\cos \phi,\sin \phi,0)$ . One can examine the effects of this on a proton spin by looking at everything in the rotating reference frame. Namely, using the basis $(\hat e_\phi,\hat z \times \hat e_\phi,\hat z)$ rather than $(\hat x,\hat y,\hat z)$ . 
    
    For the sake of simplicity, I will still refer to the axis as x-axis, y-axis, z-axis. 
    
    Now, in the rotating reference frame, we have $B_1$ entirely along the x-axis, like, all the time.
    
    Accounting for the geometric precision, with $B_1 = 0$ , we would have the spin be a constant vector in the rotating frame, with $\theta = \arccos(1/\sqrt 3)$ and a randomly set $\phi$ . 
    
    But with non-zero $B_1$ , the spin further rotates abound the x-axis. Time averaging this, we get a magnitisation in the $\hat e_\theta$ direction. 
    
    This (or its $\hat x$ component) is what we actually measure using the coils. 
    
    In actuality, $B_1$ isn’t on for the whole duration, but rather just one quarter of a cycle. This is the RF-pulse that people take about. 
    
- Relaxation
    
    Great. So now we can get reading from the H atoms. But that’s still useless data since every atom will give the same reading. The only thing that might change between tissues is the density, but that doesn’t create enough contrast.
    
    So instead, we rely on another phenomenon.
    
    After shutting down the $B_1$ field (after the pulse), there are two things that happen :
    
    1. The magnetisation due to sync along $\hat e_\phi$ slowly weakens as spins go out of sync. This is called a T2 decay.
    2. As the magnetisation weakens, the spins stop rotating about $\hat e_\phi$ and go back to their primary axis of rotation, namely the the z-axis. This is called T1 decay or relaxation.
    
    These decays are different for different tissues. 
    
    Using the decays, we can get data. 
    
    Then doing something a bit like the inverse radon transform, but different, we can reconstruct a 3D “image” (tensor of pixel values).
    
- Uses of MRI
    - Alzhiemer’s disease (imaging the brain)
    - Spinal disc (imaging spinal cord and backbone)
    - ACL in knee (no idea what this is..)
    - Multiple Sclerosis (plaques and lesions in brain)
- Artifacts
    - Respiratory Blurring
    - Aliasing : Noise Spikes
        
        A noise spike (in the frequency spectrum) can be formed due to 
        
        - RF interference
        - Gradient malfunction (wtf even is this ?)
    - Aliasing : Moire Patterns
    - Bowel movement artifact
        
        (yes, this is literally the movement of bowels through the gut)
        
        Any motion introduces a discontinuity in the phase-encoding direction (honestly, I’m confused af)
        
        These are then inverse FTed to sinc functions. 
        
        These since functions produces “ghosting”
        
    - Dental filling (again, no idea..)
- Constrast agents
    
    Ah yes, the one constant in all imaging techniques..
    
    Dynamic Constrast Enhanced MRI is used to detect tumors. 
    
    The idea is that after addition of contrast agents, the gain in the signal for tumor cells is muss higher as compared to healthy tissue. 
    
    This gives us very useful images that directly describe the position of tumor.
    
- Other techniques
    - MRI angiography (blood vessels in the brain mainly)
    - Functional MRI imaging (idk.. is it like what parts of brain are currently active or something ?)
    - Diffusion Tensor Imaging (I really have no idea, but it seems to be producing really high quality renders)
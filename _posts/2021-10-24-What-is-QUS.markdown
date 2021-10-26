---
layout: single
title: "What is Quantitative Ultrasound?"

date:   2021-10-23
categories: Technical Explanation
author_profile: true
read_time: true
classes: wide

excerpt:  "In this post, I will provide a brief explaination about Quantitative ultrasound, and you can check the references for more information."
header:
  overlay_image: "/assets/posts/post2/PMback.png"
  overlay_filter: 0.7
--- 

When I started to research about Quantitative Ultrasound (QUS), information related to QUS was limited to journal papers and scientific books. That made it hard and time-consuming process to get familiar with this concept and get a quick introductory describtion about these techniques. In this post, I will provide a brief explaination about Quantitative ultrasound, and you can check the references for more information.

<p align="center">
  <img alt="QUS" src="/assets/posts/post2/PM.png">
  <figcaption align="center">Figure 1</figcaption>
</p>

Quantitative ultrasound (QUS) techniques have been developed to derive quantitative measures from ultrasound data that are independent of instrument and imaging parameters and with a lower level of operator dependence for tissue characterization applications. The QUS techniques can be used in conjunction with sliding window analysis to generate color-coded parametric images that represent the underlying tissue characteristics. The contrast in QUS parametric images is principally based on the underlying tissue’s biophysical properties, and can give richer and more robust information about tissue micro-structure compared to the conventional B-mode images. Since different tissues consists of components with various shapes, spatial organization, and mechanical properties, QUS methods aim to estimate these properties using appropriate models and theory of how ultrasound interacts with soft tissues.
<br>

Initial studies on QUS developed basic theories to process ultrasound signals to obtain QUS parameters describing soft tissue properties and remove system dependence. In particular, Lizzi et al. and Insana et al. introduced QUS methods based on the backscatter coefficient. In addition, other QUS studies were performed which relied on measurement approaches not directly related to the backscatter coefficients. Some of these studies include using scanning acoustic microscopy, inverse and forward scattering models of ultrasound tomography, and also envelope-statistics modeling and quantification. QUS techniques have been used in several tissue characterization applications including prostate cancer diagnosis and characterization , monitoring chronic remodeling in liver tissue and breast mass characterization. Moreover, QUS has been used for monitoring tumor response to cancer treatments including radiation therapy, chemotherapy and ultrasound-stimulated microbubble therapy. In particular, these studies have demonstrated the association of QUS parameters and histology in different tissue characterization applications.
<br>

In order to estimate the QUS spectral and backscatter parameters, the mean power spectrum can be acquired by averaging the square magnitude of the fast Fourier transform (FFT) of window through ultrasound radiofrequency (RF) lines. Next, the average power spectrum is normalized using the average power spectrum of a reference phantom with known attenuation coefficient within window to remove the effects of system transfer functions and transducer beam-forming.

<p align="center">
  <img alt="QUS" src="/assets/posts/post2/PMgen.png">
  <figcaption align="center">Figure 2</figcaption>
</p>



In the next step, through a linear regression analysis, the best fit line to the normalized power spectrum will be acquired within the -6 dB bandwidth centered at the transducer center frequency. The -6 dB bandwidth is estimated from the power spectrum of the reference phantom. Spectral slope (SS) and spectral intercept (SI) are the slope and extrapolated 0-MHz intercept of the line of best fit, and midband fit (MBF) is the value of the line-approximated power spectrum at the center of the -6 dB frequency bandwidth (fc). The backscatter parameters including the effective scatterer diameter (ESD) and effective acoustic concentration (EAC) can be estimated by fitting a form factor model (e.g. spherical Gaussian model)  to the backscatter coefficient (BSC).

<p align="center">
  <img alt="QUS" src="/assets/posts/post2/QUS_Slide.gif">
  <figcaption align="center">Figure 3</figcaption>
</p>

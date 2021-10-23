---
layout: single
title: "Getting deeper in classification with segmentation"

date:   2021-10-23
categories: PaperSumm
author_profile: true
classes: wide
read_time: true

excerpt:  "We showed segmenting tumor region could result to achieve better and more informative biomarkers for classification."
header:
  overlay_image: "/assets/post1/paper2.jpg"
  overlay_filter: 0.7

---

In this study, we showed that extracting features from segmented regions of tumor would improve the classifier model to predict the responsiveness of the tumor to neo-adjuvant chemotherapy (NAC).

The data that we applied our model consisted of quantitative ultrasound (QUS) images of 181 locally advanced breast cancer (LABC) patients before the start of chemotherapy. For determining the labels, we used histopathology outcome which was acquired from the resection operation at the end of their chemotherapy.

<p align="center">
  <img alt="model" src="/assets/post1/model.png">
  <figcaption align="center">Figure 1</figcaption>
</p>


For segmentation, HMRF-EM algorithm introduced by Wang were used. HMRF-EM is a distribution-based clustering algorithm which also considers the neighboring information for segmentation. The Matlab codes for implementation can be find [here](https://www.mathworks.com/matlabcentral/fileexchange/37530-hmrf-em-image). Figure 1 demonstrates the output of segmentation for a sample QUS images.

<p align="center">
  <img alt="segmentation" src="/assets/post1/slide2.gif">
  <figcaption align="center">Figure 2</figcaption>
</p>

In the next step, the features were extracted from the segmented regions. Features such as mean value and SNR of QUS images in the segmented regions and whole tumor in addition to the proportional area of the regions were calculated and used for classificaiton. 


{% highlight ruby %}
# Compute the SNR feature 
def signaltonoise(a, axis=0, ddof=0):
    a = np.asanyarray(a)
    m = a.mean(axis)
    sd = a.std(axis=axis, ddof=ddof)
    return np.where(sd == 0, 0, m / sd)

# Organize the features based on the order of mean value of first QUS image
def organize_data(area, intensity, snr):
    idx = intensity[3, :].argsort()[::-1]
    area = area[idx]
    for i in range(intensity.shape[0]):
        intensity[i, :] = intensity[i, idx]
        snr[i, :] = snr[i, idx]
    return area, intensity, snr

def get_area_intens_snr(data, segRes, numSeg=3):
    area = np.zeros(numSeg)
    intensity = np.zeros((data.shape[2], numSeg))
    totalIntensity = np.zeros(data.shape[2])
    totalSNR = np.zeros(data.shape[2])
    snr = np.zeros((data.shape[2], numSeg))
    dReshaped = data.reshape(-1, data.shape[2])
    resReshaped = segRes.reshape(-1)
    for i in range(numSeg):
        area[i] = segRes[segRes == i].shape[0]
        for j in range(data.shape[2]):
            intensity[j, i] = np.sum(dReshaped[segRes == i, j])
            dataPar = dReshaped[:, j]
            snr[j, i] = signaltonoise(dataPar[resReshaped == i])
    for k in range(data.shape[2]):
        totalIntensity[k] = np.sum(dReshaped[segRes < 6, k])
        dataPar = dReshaped[:, k]
        totalSNR[k] = signaltonoise(dataPar[resReshaped < 6])
    totalIntensity = np.divide(totalIntensity, np.sum(area))
    intensity = np.divide(intensity, area)
    intensity[np.isnan(intensity)] = 0
    snr[np.isnan(snr)] = 0
    area = area / np.sum(area)
    area, intensity, snr = organize_data(area, intensity, snr)
    out = []
    out.extend(area)
    out.extend(intensity.reshape(-1))
    out.extend(totalIntensity)
    out.extend(snr.reshape(-1))
    out.extend(totalSNR)
    return out
{% endhighlight %}

After feature extraction, we applied multi-step feature selection algorithm to reduce the features into 4 finalized features. At the end, AdaBoost algorithm was applied for prediction of tumor response to NAC, and we showed that our model is able to predict the therapy outcome with the state of art accuracy and AUC. Also, survival analysis indicated that patients predicted as responders had higher survival rates rather than patients predicted as non-responder. 


<p align="center">
  <img alt="model" src="/assets/post1/auc.png">
  <figcaption align="center">Figure 3</figcaption>
</p>

For more information, please check out our [paper](https://pubmed.ncbi.nlm.nih.gov/34290259/).




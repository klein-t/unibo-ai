# Digitization and camera sensors

## Digitization in practice

The sensor is a 2d array of photodetectors, which convert incident light into a **proportional electric charge**. Then, in the case that the output has to be digital, the ADC circuitry converts digitizes the signals.

Today, the two main sensor technologies are **CCD** and **CMOS**.

## Camera parameters

So, what should we look at when buying a camera? We'll now provide an intuitive explanation, while formal definitions and measurements can be found in the *EMVA Standard 1288*.

### Signal to Noise Ratio (SNR)

This is a very important parameter: noise has a large impact in image processing and computer vision. Basically, noise is generated by: 

- *Photon Shot Noise*, the number of photons collected is not stable. The light captured by the camera is not deterministic, but it is a random variable governed by a Poisson statistic;
- *Electronic Circuitry Noise*, generated by the electronics which read out the charge and amplify the signal;
- *Quantization Noise*, related to the ADC;
- *Dark Current Noise*, charge due to thermal excitement observed at each pixel even in the dark. Therefore, it happens even when the shutter is closed! This one is common in solid state sensors. This phenomenon is highly related to **temperature**: the *hotter*, the *more noise*.

Given this, measurements of the same pixel are gonna change even if the image is static. Therefore, the measurement at iteration $i$ will be $I_i (p) = I_i^* (p) + n(p)$, where $I_i^*$ is the real signal while $n(p)$ is the noise.

Now, given this model, the only thing we can do is taking more measurements and averaging them: when we do so, the $n(p)$ tends to delete itself (let's say positive and negative noises alternate in a approximately standard distribution). **We assume noise to be IID, and have zero average:** $N(0, \sigma^2)$.

So, the question becomes: I have my image, how can I take more measurements in a little time? The solution might be averaging neighbouring pixels!

To assess how much noise is there in a certain camera, there's a parameter, the **SNR**, which has to be measured to a well defined procedure, but in essence this ratio has to be high. It is typically measured in *dB*. 

### Dynamic Range (DR)

Let's say we have our pixels, the amount of charge stored in each pixel must be higher than a minimum quantity named $E_{min}$ . We know that because of the dark current, every pixel will always have a certain minimum value. To measure the signal, to be distinguishable from noise, the signal has to be over a certain threshold, i.e. $E_{min}$, **detectable irradiation**. On the other hand, the charge stored in each pixel cannot exceed a certain quantity, $E_{max}$, i.e. the **saturation irradiation**. The ratio between the minimum amount of charge you have to sense in order to perceive a signal, and the maximum amount of charge is called **Dynamic Range**, and similarly to the SNR, ***the higher, the better***. Why is this? This enables us to capture low light and high light regions within the same picture. 

An active research field in image processing deals with creating ***High Dynamic Range*** images by combining together a sequence of images of the same subject.

## CCD vs CMOS

Unlike CCD, **CMOS** allowa the electronic circuitry to be integrated within the **same chip** as the sensor (*one chip camera*): this provides compactness, less power consumtion, lower costs.

**CMOS** sensor allow an arbitrary window to be read-out without having to receive the full image. This means that you can retrieve **just a few pixels** instead of the whole image like a CCD does. Imagine you're trying to track an object, you don't need every part of the image!

**However**, CCD typically provide higher quality images, higher SNR, higher DR, better uniformity. Because of that, CCD are used in high end applications, while CMOS are used in low cost devices.

## Colour sensors

CCD/CMOS are sensitive to light ranging from *near-ultraviolet*, through the *visible spectrum* up to *near infrared*. The sensed intensity at a pixel results from integration over the range of wavelengths of the spectral distribution of the incoming light multiplied by the spectral response function of the sensor. As such, CCD/CMOS cannot sense colour. So, **how does it work?** 

To create a colour sensor, an array of optical filters is placed in front of the photodetectors, as to render each pixel sensitive to a specific range of wavelengths. In the most common Bayer CFA green filters are twice as much as red and blue ones to mimic the higher sensitivity of the human eye in the green range. However, the true resolution of the sensor is smaller due to the green channel being subsampled by a factor of 2, the blue and red ones by 4.

A **full resolution colour sensor** can be achieved by deploying an **optical prism** to split the light beam into 3 RGB beams sent to 3 distinct sensors, equipped with corresponding filters. 

## Sensor sizes

CCD/CMOS sensors come in different sizes, which are specified in inches for the sake of legacy wrt old cameras based on cathode tube rays. Nowadays, the size diminished. The provided sizes have nothing to do with the real sizes, it's just for legacy sake. A bigger sensor is tipically better, it can have bigger pixels. A smaller sensor will have very small pixels which are tipically very noisy. 














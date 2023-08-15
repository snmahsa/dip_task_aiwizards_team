
# Introduction

Digital image processing involves transforming images from the real-world domain into digital domains, extracting useful information from images, and applying changes according to specific needs and objectives. This process has widespread applications in various fields such as medicine, security, robotics, computer vision, artificial intelligence, and more.

Filtering is another important process in digital image processing. In this stage, filters and masks are applied to the image to highlight specific aspects or modify it. For example, filters can be used for noise removal, edge enhancement, image alignment, or applying special effects.

# DipWizards Package

This repository contains the DipWizards package developed by the AIWizards team. As a member of the AIWizards team, I have contributed to the development of this package. DipWizards is a  Python package for generating noise and applying filters to grayscale and color images.

## Installation

To install the DipWizards package, use the following command:

```shell
pip install dipwizards
```
## Usage
### Generating Noise

DipWizards provides several noise generation functions for adding random noise to images. Here are some examples:

### Gaussian Noise
```python
import DipWizards.utils as utl
noise_generator = utl.ImageNoiseRGB(image)
noisy_image = noise_generator..add_noise('gauss', var=0.4)
```
### Poisson Noise
```python
noise_generator = utl.ImageNoiseRGB(image)
noisy_image = noise_generator.add_noise('poisson')
```
### Salt-and-Pepper Noise
```python
noise_generator = utl.ImageNoiseRGB(image)
noisy_image = noise_generator.add_noise('s&p', amount=0.2, s_vs_p=0.3)
```
## Applying Filters

DipWizards provides various filters for image enhancement. Here are some examples:
### Mean Filter
```python
fmean_gauss  = utl.SpatialFilterRGB(img_gauss).apply_filter('mean',   3, 0)
```
### Median Filter
```python
fmedian_gauss  = utl.SpatialFilterRGB(np.uint8(img_gauss)).apply_filter('median', 3,0)
```
### adaptive Filter
```python
fmedian_adapt  = utl.SpatialFilterRGB(np.uint8(img_gauss)).apply_filter('adaptive', 3, 0)
```
### Frequency Filter
```python
frequency = utl.FrequencyFilterRGB2(img_gauss_1)
filter_image = frequency.low_pass_filter(50)

```
## Examples

Here is an example of how to use the DipWizards package to generate noise and apply filters:
```python
import DipWizards.utils as utl
import cv2
import numpy as np
import matplotlib.pyplot as plt
import PIL
import requests
from io import BytesIO
import sys
from skimage.metrics import structural_similarity as compare_ssim

image= cv2.imread( "Image/20230526_141939.jpg")
x = utl.ImageNoiseRGB(image)
img_gauss = x.add_noise('gauss', var=0.4)
utl.show_mult_img(1, 2, [img_gauss, image])

fmean_gauss  = utl.SpatialFilterRGB(img_gauss).apply_filter('mean',   3, 0)
fmedian_gauss  = utl.SpatialFilterRGB(np.uint8(img_gauss)).apply_filter('median', 3,0)
fmedian_adapt  = utl.SpatialFilterRGB(np.uint8(img_gauss)).apply_filter('adaptive', 3, 0)
utl.show_mult_img(1,3, [fmean_gauss,fmedian_gauss, fmean_gauss])
compare_ssim(image, fmedian_gauss, multichannel=True, channel_axis=-1, data_range=1.0)

```

![Sample Image](https://github.com/snmahsa/myrep/blob/main/output.png)


```python
compare_ssim(image, fmedian_gauss, multichannel=True, channel_axis=-1, data_range=1.0)
```

```
0.7817538716636611
```

![Sample Image](https://github.com/snmahsa/myrep/blob/main/sp.png)

```python
compare_ssim(image, fmedian_sp, multichannel=True, channel_axis=-1, data_range=1.0)
```

```
0.707133375578977
```
![Sample Image](https://github.com/snmahsa/myrep/blob/main/hist.png)

```python
compare_ssim(img_sp, histo_result, multichannel=True, channel_axis=-1, data_range=1.0)
```

```
0.7997069942886444
```


In this example, an example of image filtering performance with SSIM is the structural similarity measure of images. The corresponding notebook is available in this repository and you can see more examples of them.

[The mentioned notebook]( https://github.com/snmahsa/dip_task_aiwizards_team/blob/main/BGR_Imagr.ipynb)

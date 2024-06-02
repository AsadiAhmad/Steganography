# Steganography
Steganography is for hiding text in the image without changeing image look with openCV and Numpy Library

## Summery :
This project first 

## Tech :hammer_and_wrench: Languages and Tools :
<div>
  <img src="https://github.com/devicons/devicon/blob/master/icons/python/python-original.svg" title="Python" alt="Python" width="40" height="40"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/opencv/opencv-original.svg"  title="OpenCV" alt="OpenCV" width="40" height="40"/>&nbsp;
  <img src="https://github.com/devicons/devicon/blob/master/icons/numpy/numpy-original.svg"  title="Numpy" alt="Numpy" width="40" height="40"/>&nbsp;
</div>

## Tutorial
### Step1: Install Librarys
We need to have installed Python, OpenCV and Numpy

for windows and ubuntu we need install python, OpenCV and Numpy

and for Google colab just install OpenCV

install OpenCV
```sh
!pip install opencv-python
```

install Numpy
```sh
!pip install numpy
```

### Step2: Import Librarys
import opencv,numpy library and cv2_imshow for showing picture in google colab

```sh
import cv2
import numpy as np
from google.colab.patches import cv2_imshow
```

### Step3: Load Image
Upload your image into google colab or for local device using a local image.

found your image location and copy the path

```sh
image_path = "/content/Wallpaper.jpg"
image = cv2.imread(image_path)
cv2_imshow(image)
```

<img src="/Image/Wallpaper.png"/>

### Step4: Load text data
### Step5: Convert text to binary
### Step6: Calculate size of image
### Step7: Extend binary bits
### Step8: Spereate binary text into channel parts
### Step9: Seperate image to channel parts
### Step10: Decode text into image
### Step11: Build image
### Step12: Encode text from image

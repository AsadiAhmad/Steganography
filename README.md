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

<img src="/Images/Wallpaper.jpg"/>

### Step4: Load text data
here you can enter your text to hide it in image

```sh
text = """here is your text"""
```

### Step5: Convert text to binary
you need to convert your text into binary text

```sh
def text_to_bin(text):
    binary = ''.join(format(ord(char), '08b') for char in text)
    return binary
binary_text = text_to_bin(text)
print(binary_text)
```

here is the sample of binary converted:

010000000110100101101101

### Step6: Calculate size of image
now you need to know what is your image size and how much it can hold data within

```sh
height, width, channels = image.shape
image_size = height*width
max_chars = int((channels*image_size)/8)
```

```sh
print("image height : " + str(height))
print("image width : " + str(width))
print("image size : " + str(image_size))
print("max charechter can hide in picture : " + str(max_chars))
print("image can hide : " + str((channels*image_size)/80) + " Words")
```

here is some information about our image :

image height : 720

image width : 1280

image size : 921600

max charechter can hide in picture : 345600

image can hide : 34560.0 Words

### Step7: Extend binary bits
Here you should change the format of your text into image to fit the text to image

if your text is to big for your image here you see the error

```sh
def extend_binary_text(image_size, binary_text, max_chars):
    needed_bits = len(binary_text)
    if(needed_bits > max_chars*8):
        print("text size is too high")
        return

    extended_binary_text = binary_text.ljust(max_chars*8, '0')
    return extended_binary_text
extended_binary_text = extend_binary_text(image_size, binary_text, max_chars)
```

### Step8: Spereate binary text into channel parts
### Step9: Seperate image to channel parts
### Step10: Decode text into image
### Step11: Build image
### Step12: Encode text from image

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
Because we have RGB image for using maximum space from the image we should separate the text into 3 part

```sh
def divide_string_parts(text, channels):
    part_length = len(text) // channels
    text_parts = []
    
    for i in range(channels):
        part_start = part_length * i
        part_end = part_length * (i + 1)
        text_parts.append(text[part_start:part_end])
    
    return text_parts
text_parts = divide_string_parts(extended_binary_text, channels)
```

### Step9: Seperate image to channel parts
Sperate image into Red Green and Blue frame

```sh
if channels == 3:
    blue_channel, green_channel, red_channel = cv2.split(image)
    blue_matrix = np.array(blue_channel)
    green_matrix = np.array(green_channel)
    red_matrix = np.array(red_channel)
```

### Step10: Decode text into image
Here is our main function for decoding data into image in here we remove the first bit(LSB) of a pixel then replace it with our data then do it for all pixels

```sh
def decimalToBinary(n): 
    return format(n, '08b')

def binaryToDecimal(n):
    return int(n,2)

counter = 0
for i in range(height):
    for j in range(width):
        red_matrix[i,j] = binaryToDecimal(decimalToBinary(red_matrix[i,j])[0:7] + text_parts[0][counter])
        green_matrix[i,j] = binaryToDecimal(decimalToBinary(green_matrix[i,j])[0:7] + text_parts[1][counter])
        blue_matrix[i,j] = binaryToDecimal(decimalToBinary(blue_matrix[i,j])[0:7] + text_parts[2][counter])
        counter += 1
```

### Step11: Build image
We need to gather Red Green and Blue Frame and Biuld our image.

```sh
reconstructed_image = cv2.merge([blue_matrix, green_matrix, red_matrix])
cv2.imwrite("/content/ImageWithData.png", reconstructed_image)
cv2_imshow(reconstructed_image)
```

<img src="/Images/ImageWithData.png"/>

if you notice you cant see any changes from the picture.

### Step12: Encode text from image
Encode the image with reading the image by 8bit and extract the text.

```sh
def bin_to_text(binary):
    text = ''.join(chr(int(binary[i:i+8], 2)) for i in range(0, len(binary), 8))
    return text

def cut_binary_at_8_zeros(binary_str):
    for i in range(0, len(binary_str), 8):
        chunk = binary_str[i:i+8]
        if chunk == '00000000':
            return binary_str[:i]
    return binary_str

def decode_text_from_image(image_path):
    image = cv2.imread(image_path)
    blue_channel, green_channel, red_channel = cv2.split(image)

    blue_matrix = np.array(blue_channel)
    green_matrix = np.array(green_channel)
    red_matrix = np.array(red_channel)

    text1 = ""
    text2 = ""
    text3 = ""
    counter = 0
    for i in range(height):
        for j in range(width):
            text1 = text1 + decimalToBinary(red_matrix[i,j])[-1]
            text2 = text2 + decimalToBinary(green_matrix[i,j])[-1]
            text3 = text3 + decimalToBinary(blue_matrix[i,j])[-1]
            counter += 1
    concated_binary_text = text1 + text2 + text3
    cuted_binary_text = cut_binary_at_8_zeros(concated_binary_text)
    return bin_to_text(cuted_binary_text)

decode_text_from_image("/content/ImageWithData.png")
```

after running this method you can see the hided text

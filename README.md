# MTCNN-PureC
MTCNN face detection with C and Arm-CMSIS-DSP

## Introduction
The project is a MTCNN face detection based on C. To implement MTCNN in MCU, the project doesn't rely on any library and you can use [ARM-CMSIS-DSP](https://github.com/ARM-software/CMSIS_5) to accelerate the matrix multiplication.
The input data is a RGB CHW txt, and output is the keypoints of face and bounding box of face.


This project is the C implementation of MTCNN, no dependent library, mainly written for the MCU of the arm platform, and can be accelerated by the [ARM-CMSIS-DSP](https://github.com/ARM-software/CMSIS_5) library during deployment For matrix multiplication operations, please refer to the official documentation.

This project simplified `arm_math.h` and `arm_mat_mult_f32.c` while keeping the API unchanged, so as to run on the PC platform.


The input is a text file in RGB CHW format, and the output is the face bounding box and face key points.

## Usage
```shell
git clone https://github.com/notplus/MTCNN-PureC.git
cd MTCNN-PureC
mkdir build
cd build
cmake ..
make
```

## Demo
![picture 1](https://github.com/notplus/MTCNN-PureC/blob/master/1.jpg)

### Input

The input is a text file generated from an RGB CHW format image, which can be generated using the following code. In addition, when using it, you need to modify the image size in `include/test.h`.

```python
import numpy as np
import cv2
img = cv2.imread("1.jpg")
img_ = img[:,:,::-1].transpose((2,0,1))
np.savetxt('input1.txt', img_.reshape(-1), "%d")
```

### Output  
* boundingBox3 is 160 72 450 362         //(x1, y1, x2, y2)
* keyPoint0 is 259.010193 188.661850  
* keyPoint1 is 350.958679 183.481461   
* keyPoint2 is 309.558563 237.440964   
* keyPoint3 is 267.242126 291.008728   
* keyPoint4 is 354.936646 283.069946   

### Print with opencv
![picture 2](https://github.com/notplus/MTCNN-PureC/blob/master/result.jpg)


## Implement Details
The project mainly refers to [MTCNN-light](https://github.com/AlphaQi/MTCNN-light) and remove OpenCV and OpenBLAS dependencies.      
Convolution is implemented by im2col and matrix multiplication.  


This project mainly refers to [MTCNN-light](https://github.com/AlphaQi/MTCNN-light), and removes OpenCV and OpenBLAS dependencies.

# 7. OpenCV Basic Lesson

## 7.1 Computer Image Processing Fundamentals

OpenCV (Open Source Capture Vision) is a free computer vision library that can process images and video is used to complete various tasks, such as displaying the signal input by the camera and allowing the robot to recognize objects in life.

Although python has its own image processing library PIL, its function is weaker than OpenCV. OpenCV provides with a complete Python port, Python3.5 and python-opencv libraries have been integrated in the mirroring system we provide file. You can directly use this powerful computer vision library.

Next, I will briefly explain the basic knowledge of computer image processing, and the knowledge of OpenCV common functions.

We know that an image is composed of pixels, so how does the computer store and recognize different images? Each pixels can be represented by the R, G, and B values of the three primary colors ranging from 0-255. OpenCV uses a ternary for each pixel array representation, and then save this array to record all the information of the image. But it should be noted that the array of the three color channels of the RGB image recorded in OpenCV, the recording order will become BGR, so we often call the image is a BGR image.

For other images such as HSV and Lab standards, they are also stored in the form of a multivariate array. An OpenCV the image is a two-dimensional or three-dimensional array of type .array, and an 8-bit grayscale image (only black and white images) is a two-dimensional array, a 24-bit BGR image is a

three-dimensional array. For example, for a BRG image, image\[0,0,0\] the first value represents the Y coordinate or row of the pixel, and 0 represents the top; the second value represents the x coordinate or column of the pixel, and 0 represents the far left; the third value represents the color channel.

These arrays of recorded images can be accessed separately like ordinary Python arrays to obtain a certain color separately the value of the channel, or the image of a certain area of the image.

## 7.2 OpenCV Module Instruction

### 7.2.1 OpenCV Module

The OpenCV module is named cv2 in Python library. It integrates all OpenCV functions for computer vision, machine learning, image processing used by OpenCV.

User can use the cv2 module to realize face and object recognition, video and image search, TV channel advertisement recognition and street view image stitching,etc.

### 7.2.2 The Use of OpenCV Module

There are two main forms of using OpencCV module, command line call and program call.

* **Command Line Call**

1. First, enter “**python3**” command in command line terminal and press “**Enter**” to start the interactive environment of Python. (Take the terminal interface after connecting SSH as an example )

   <img class="common_img" src="../_static/media/chapter_7\section_2\media\image2.png" style="width:500px"  />

2. Then, enter “**import cv2**” command to import OpenCV module, and then you can directly call the function in it.

   <img class="common_img" src="../_static/media/chapter_7\section_2\media\image3.png" style="width:500px"  />

* **Program Call**

1. First, you need to create a new program file with suffix .py, such as “**test.py**”.

   <img class="common_img" src="../_static/media/chapter_7\section_2\media\image4.png" style="width:200px"  />

2. Then, enter “**import cv2**” command in .py file and then import module before using OpenCV function.

   <img class="common_img" src="../_static/media/chapter_7\section_2\media\image5.png" style="width:500px"  />

### 7.2.3 OpenCV Module and Common Function

In the following lesson, let’s learn about some functions commonly used by OpenCV：

1)  **`cv2.imread(filepath,flags)` function for read a image.**

`filepath`: the full path of image to be read.

`flags`: Image loading mode.

`cv2.IMREAD_COLOR`: default parameter. Read a color image and ignore the alpha channel.

`cv2.IMREAD_GRAYSCALE`: read grayscale image.

`cv2.IMREAD_UNCHANGED`: read complete image including the alpha channel.

2)  **`cv2.imshow(wname,img)` function for displaying image**

`wname`: display the name of window displaying image.

`Img`: the image to be displayed ( the image read by cv2.imread function ). The window size is automatically adjusted to image size.

3)  **`cv2.flip(img,flipcode)` for flipping image**

`img`: the image to be flipped.

`flipcode`: flipping effect control. When greater than 0, filp along with y-axis; when equal to 0, flip along x-axis; when less than 0, flip along both x-axis and y-axis simultaneously.

4)  **`cv2.imwrite(file,img,num)` function for saving a image**

`file`: the file name to be saved

`img`: the image to be saved

`Num`: optional parameter. For JPEG format images, this parameter indicates the image quality (CV_IMWRITE_JPEG_QUALITY) ranges from 0 to100. Its value is 95 by default. For PNG format images, this parameter indicates the compression level (CV_IMWRITE_PNG_COMPRESSION) ranges from 0 to 9. Greater value means smaller size and longer compression time. Its value is 3 by default.

5)  **`cv2.putText(img, text, org, fontFace, fontScale, color, thickness) `function for outputting text on images**

`img`: Image

`text`: the text to be output

`org`: the coordinates of the starting point of the text. The first parameter is the width and the second is the height.

`fontFace`: font

`fontScale`: font size

`color`: font color

`thickness`: font bold

## 7.3 Basic Operations of OpenCV

### 7.3.1 Image reading and writing

Read the image: `cv2.imread(Location, Model)`

`Location`——Want to read the image address. The address can be an absolute path or a relative path, but note that the usage of path slashes in different operating systems.

`Model`——Image loading mode, the first is cv2.IMREAD_COLOR, which is used to load a color image, but does not load its own Alpha channel (recording transparency); the second is cv2.IMREAD_GRAYSCALE, which is used to load one Grayscale image; the third type is cv2.IMREAD_UNCHANGED, which loads the Alpha channel while loading the image.

Display image: `cv2.imshow(‘Name’,Pic)`

`Name`——The name of the window displaying the image.

`Pic`——The image to be displayed (the image object that has been read in using `cv2.imread()` before).

Example: Create a new py file, and put a picture with the full name `camera.png` in the same folder of the py file, enter the following code, you can see the image displayed after running, press any key to display the image hide.

<img class="common_img" src="../_static/media/chapter_7\section_3\media\image2.jpeg" style="width:400px" />

> [!NOTE]
>
> **The `cv2.waitKey()` function will wait for any key of the keyboard to be pressed, and the `cv2.destroyALLWindows()` function will close all windows.**

### 7.3.2 Video reading and writing

Video can be seen as a fast switching image, so video reading and writing can actually be seen as a continuation of image reading and writing.

Camera initialization: `cv2.VideoCapture(Number)`.

`Number`-------the serial number of camera, and it is 0 usually.

> [!NOTE]
>
> **Before running the program, run “sudo systemctl stop roscore” command to close Ros.**

When you complete the operations in this lesson, you need run “**sudo systemctl start roscore**” command to open Ros again. If it is opened, other games will be affected.

If the robotic arm connects to the computer in direct connection mode, please set Number as “**http://192.168.149.1:8080/stream?topic=/usb_cam/image_rect_color**”. If the robotic arm connects to the computer in LAN mode, just modify 192.168.149.1 as IP address obtained in LAN mode.

You can follow the steps below to connect to the computer remotely in LAN mode.

**Step 1**: according to the tutorial in “**[2. Quick User Experience-> 2.1 APP Control-> 2.1.4 LAN Mode Connection]()**”, enter the LAN mode to obtain the corresponding IP address.

<img class="common_img" src="../_static/media/chapter_7\section_3\media\image3.png" style="width:500px" />

Step 2: connect your computer to the WiFi.

<img class="common_img" src="../_static/media/chapter_7\section_3\media\image4.png" style="width:500px"  />

Step3: search the obtained IP address in NoMachine to connect the robotic arm remotely, The rest steps are the same as the direct connection mode.

<img class="common_img" src="../_static/media/chapter_7\section_3\media\image5.png" style="width:500px"  />

Read the first frame of the camera

Capture-----it refers to camera object defined before.

For example: display the camera image on the desktop. And you can press “**q**” key to remove the image.

<img class="common_img" src="../_static/media/chapter_7\section_3\media\image6.png" style="width:500px"  />

> [!NOTE]
>
> **`cv2.waitKey(delay)`** is waiting for keyboard input and can refresh the image in the video. `delay` in the bracket refers to wait time. After one frame is displayed, the next frame will be displayed in “**delay**” ms.

## 7.4 Image processing methods Introduction

### 7.4.1 Image preprocessing

Usually, we need to perform special processing on the original image. For example, when doing facial recognition, we often need to convert the image to a grayscale image. Before formally learning image processing, let's first look at the conversion of different color spaces in OpenCV.

There are hundreds of methods for converting between different color spaces in OpenCV. At present, there are three common color spaces in the field of computer vision: grayscale, BGR, HSV (tone Hue, saturation, brightness value). The YCrCba color space is useful in our gameplay course, where Y refers to the brightness, Cr refers to the difference between the red part of the RGB input signal and the brightness value of the RGB signal, and Cb refers to the blue part of the RGB input signal The difference between the brightness value and the RGB signal. The feature of this color space is to separate brightness and chroma, which is suitable for image processing and is often used in human skin color detection.

Color conversion: `cv2.cvtColor(Img,Transform_model)`.

Img-image object.

Transform_model-Specifies the color conversion mode.

Note that the color and light mixing here is different from the pigment mixing. The pigment has color because it reflects the light of that color. When multiple colors are mixed, they follow the subtractive color mixing, and the light on the screen is the light emitted by the screen, which follows the principle of color enhancement.

### 7.4.2 Image Processing Principles

In OpenCV, most of the processing of images and videos involves the concept of Fourier transform. Fourier observed that all waveform in mathematics can be obtained by superimposing a series of simple sinusoids with different frequencies. It is inferred and proved that any waveform that people see is obtained by superposition of other waveform.

When we process images, we can get the area of interest by removing part of the waveform.

In addition to Fourier transform, high-pass filters and low-pass filters are often mentioned in the image processing process.

Among them, the high-pass filter is a filter that detects a certain area of the image, and then enhances the brightness of the pixel according to the brightness difference between the pixel and the surrounding pixels.

The high-pass filter will increase the brightness gap between pixels and surrounding pixels, and is generally used in edge detection.

Low-pass filtering is a filter that smoothes the brightness of a pixel when the brightness difference between a pixel and surrounding pixels is less than a certain value. It is mainly used for denoising and blurring, such as the most commonly used blur filter (smoothing filter): Gaussian blur, which is essentially a low-pass filter that weakens the strength of high-frequency signals.

### 7.4.3 Edge detection

Each picture contains a lot of content, and it is often need to separate different content when processing images.

There is always an edge between two adjacent areas with different gray values, and the edge is the performance of the gray value discontinuity. In general, the purpose of edge detection is to detect the edge of an image, that is, where the image is significantly different, to prepare for the subsequent further image processing.

For example, if we want to find oranges from a picture that contains apples, oranges, and pears at the same time, then we need to first determine which of the objects are in the picture and which are the background. Here we are interested in fruits. Edge detection can detect the contour edges of fruits in the picture, helping the computer to determine which parts of the picture are objects and which parts are the background, and prepare for the subsequent further determination of which are oranges and which are not oranges.

OpenCV provides many edge detection filter functions, including `Laplacian()`, `Sobel()` and `Scharr()`. These filter functions will convert non-edge areas to black, and edge areas to white or other saturated colors.

However, in actual processing, these functions are easy to misidentify the noise as an edge, so it is necessary to blur the image before finding the edge to remove the noise. OpenCV also provides many blur filter functions, commonly used are `blur()` (simple arithmetic average), `medianBlur()` (median filtering), `GaussianBlur()`.

There is also a very convenient Canny function in actual use, which can easily realize edge detection with only one line of code.

`cv2.Canny(Pic,Minval,Maxval)`.

`cv2.Canny(Pic,Minval,Maxval)`.

`Pic`——The image object whose edges are to be detected.

`Minval`——The minimum gray gradient threshold. When the image gray gradient is lower than Minval, it will be discarded.

`Maxval`——The maximum gradient value threshold. When the image gray gradient is higher than Maxval, it will be considered as an edge. When the image gray gradient is between Minval and Maxval, if it is connected to the edge, it is part of the boundary, otherwise it is discarded.

The Canny edge detection algorithm actually uses the following 5 steps to process the image:

1) Use a Gaussian filter to smooth the image and filter out noise.

2) Calculate the gradient intensity and direction of each pixel in the image.

3) Use Non-Maximum Suppression on the edge to eliminate spurious response caused by edge detection.

4) Use dual thresholds on the detected edges to remove false positives, that is, determine which of the gradient values ​​are between Minval and Maxval are edges and which should be discarded.

5) Analyze all edges and the connections between them, suppress isolated weak edges, to ensure that true edges are left and unobvious edges are eliminated.

Example: Create a new py file, and put a picture with the full name "**camera.png**" in the same folder of the py file, enter the following code, after running, you can see the white outline of the image appears on the screen, and other places change It is black, and the image is hidden after pressing any key.

<img class="common_img" src="../_static/media/chapter_7\section_4\media\image2.png" style="width:500px" />

### 7.4.4 Contour detection

In computer vision, it is often necessary to detect the contours of objects in images or videos, and on this basis calculate polygon boundaries, shape approximations, and calculate regions of interest.

In OpenCV, you can call the `findContours()` function to detect contours. The specific parameters of the function are as follows:

`findContours(Img,Model,Method)`

`Img`——The picture object whose contour is to be detected. Note that the picture needs to be a grayscale picture.

**Model——Indicates the detection mode of the contour:**

`cv2.RETR_EXTERNAL`:It means that only the outer contour is detected.

`cv2.RETR_LIST`: The detected contour does not establish a hierarchical relationship.

`cv2.RETR_CCOMP`: Establish two levels of contours, the upper layer is the outer boundary, and the inner layer is the boundary information of the inner hole. If there is a connected object in the inner hole, the boundary of this object is also on the top layer.

`cv2.RETR_TREE`：Establish the outline of a hierarchical tree structure.

**Method-Represents the contour approximation method and detection strategy, specifically as follows:**

`cv2.CHAIN_APPROX_NONE` stores all contour points, and the pixel position difference between two adjacent points does not exceed 1, that is, max(abs(x1-x2), abs(y2-y1))==1.

`cv2.CHAIN_APPROX_SIMPLE` compresses the elements in the horizontal, vertical, and diagonal directions, and only retains the end point coordinates in that direction. For example, a rectangular outline only needs 4 points to save the outline information.

cv2.CHAIN_APPROX_TC89_L1, CV_CHAIN_APPROX_TC89_KCOS uses the teh-Chinl chain approximation algorithm.

The `findContours()` function has three return values: the modified image, the contour of the image, and their levels.

### 7.4.5 Line and circle detection

Hough transform is the theoretical basis behind straight line and shape detection. It was proposed by Richard Duda and Peter Hart in the 1960s.

Straight line detection can be done by either of HougLines and HoughLinesP. The first function uses the standard Hough transform, and the second function uses the probabilistic Hough transform.

The probabilistic Hough transform is an optimized version of the standard Hough transform. It only performs line detection by analyzing a subset of points and estimating the probability that these points belong to a straight line. This algorithm requires less calculation and is fast to execute.

**Probability Hough transform:**

**`cv2.HougLinesP(img,rho,theta,threshod,minLineLength,maxLineGap)`**

`img`——The image to be processed must be a grayscale image (binary image). Generally, the result image of canny edge detection is used.

`rho`——The distance accuracy of the line segment in pixels. For double type, 1.0 is recommended.

`theta`——The angular accuracy of the line segment in radians. numpy.pi/180 is recommended.

`threshod`——Threshold, all straight lines below this threshold will be deleted.

`minLineLength`——The minimum length of the line segment in pixels, set according to the application scenario.

`maxLineGap`——The maximum allowable gap (break) between two line segments in the same direction is judged to be a line segment. If it is less than the set value, the two line segments will be regarded as one line segment. The larger the value, the larger the allowable break on the line segment, the more likely it is Detect potential straight line segments.

OpenCV can use the HoughCircles function to detect circles, which is similar to using the HougLines function.

`cv2.HoughCircles(image, method, dp, minDist, circles, param1, param2, minRadius, maxRadius)`

`image`——input image, need grayscale image (binary image).

`method`——Detection method, commonly used CV_HOUGH_GRADIENT.

`dp`——in order to detect the reciprocal of the ratio of the resolution of the accumulator image at the inner circle center to the input image, such as dp=1, the accumulator and the input image have the same resolution, if dp=2, the accumulator has half of the input image That big width and height.

`minDist`-represents the minimum distance between the center of two circles.

`param1`——The default value is 100, which is the corresponding parameter of the detection method set by the method. For the current only method, the Hough gradient method cv2.HOUGH_GRADIENT, it represents the high threshold passed to the canny edge detection operator, and the low threshold is high Half of the threshold

`param2`——The default value is 100. It is the corresponding parameter of the detection method set by the method. For the current only method Hough gradient method cv2.HOUGH_GRADIENT, it represents the accumulator threshold at the center of the detection stage. The smaller it is, the better More circles that don't exist at all are detected, and the larger the circle, the closer the circle can pass the detection to the perfect circle.

`minRadius`——The default value is 0, the minimum value of the circle radius.

`maxRadius`——The default value is 0, the maximum value of the circle radius.

Example: Create a new py file, and put a picture with the full name "camera.png" in the same folder of the py file, enter the following code, after running, you can see that the detected circle is marked with a green line on the screen Circle the outline and mark the center of the circle. Press any key to close the image window.

<img class="common_img" src="../_static/media/chapter_7\section_4\media\image3.png" style="width:500px" />

If you want to detect polygons, you can combine the `cv2.findContours` function and the `cv2.approxPloyDP` function.

## 7.5 Advanced Image Processing Technology

### 7.5.1 Facial Detection and Recognition

Extracting the details of the image is very useful for generating stable classification results and tracking results. These extracted results are called features. For a given image, the features may be different due to the size of the area which can be called the window size. Even if the window sizes are different, two images that differ only in scale should have similar characteristics. Therefore, generating features that can be adapted to windows of different sizes is a very critical point in image processing.

The collection of the same feature in these different size windows is called cascade. Haar feature in OpenCV is a feature for real-time face tracking. The Haar cascade is scale-invariant, which means that its characteristics can be applied to images with different window sizes.

OpenCV provides Haar cascaded classifiers and trackers with constant scale, and can be saved as a specified file format. However, it should be noted that OpenCV's Haar cascade does not have rotation invariance. For example, Haar cascade does not consider the inverted face image to be the same as the upright face image.

The operation of detecting faces in still images or videos is very similar. Video facial recognition just reads each frame of image from the camera, and then uses the facial recognition method in the static images to detect.

Before programming the facial recognition, copy the facial recognition XML file in the haarcascades folder in the OpenCV source code (address in Raspberry Pi: /usr/share/opencv/haarcascades) to the saved facial recognition Python code Folder.

Example: Detect a face through the camera and circle the face in a rectangle.

<img class="common_img" src="../_static/media/chapter_7\section_5\media\image2.png" style="width:500px" />

Face recognition generally uses scripts to generate original sampled images at first. Detects human faces, crop the gray frame area, adjust it to a fixed size, and finally save it in a folder. This face data will be used to train the face recognition model later.

After the sampling is completed, next step is face recognition. OpenCV 3 supports three face recognition methods, which are Eigenfaces, Fisherfaces and Local Binary Pattern Histogram (LBPH). After one of algorithm is selected, training and identification can be carried out.

### 7.5.2 Image Recognition and Retrieval

OpenCV can detect the main features of an image, and then extract these features to make it an image descriptor. These image features can be used as a database for image search, which can help you find the elements you are looking for in the image library. For example, if you want to find out who has a specific tattoo in tens of thousands of pictures, you can use the tattoo as an image descriptor to search for matching in each picture.

Image feature detection includes corner points and spots. A small change of a pixel at a certain point in an image in any direction will cause a large change in the gray value, then we call this point a corner point or key point. Spots refer to areas in a two-dimensional image that have color differences and gray-scale differences with the surrounding colors.

The most common feature detection and extraction algorithms in OpenCV are as follows:

Harris: detect corner point

SIFT: detect spot（blob）

SURF: detect spot

FAST: detect corner point

BRIEF: detect spot

ORB: This algorithm represents the FAST algorithm with direction and the BRIEF algorithm with rotation invariance.

Feature matching after detection has Brute-Force, which is based on FLANN.

The Brute-Force matching method compares two descriptors and list a matching results. It is called brute force because the algorithm basically does not involve optimization. All the features of the first descriptor are compared with the features of the second descriptor, and all possible combinations are listed.

FLANN is short for Fast_library_for_Approximate_Nearest_Neighbors. It is a collection of algorithms for searching for the nearest similar point on large data sets and high-dimensional features. These algorithms have been optimized and have high processing efficiency.

### 7.5.3 Deep Learning

In addition to the aforementioned, OpenCV can also detect a moving target in the lens and track and predict the trajectory of the target (using Kalman filter).

With ANN (artificial neural network) part in the ml module of OpenCV, we can complete some machine learning projects, such as handwriting recognition and human-computer interaction.

OpenCV belongs to the field of artificial intelligence. The above courses are just an introductory guide for beginners to lead everyone to understand the application principle and learning direction of OpenCV. However, it is far from enough to rely on this tutorial to master OpenCV technology. If you have strongly interests, please check the related books.

## 7.6 Color Recognition

### 7.6.1 Camera Horizontal Installation

<img class="common_img" src="../_static/media/chapter_7\section_6_1/media/image1.png" style="width:500px" />

### 7.6.2 Getting Ready

In this section, you need to adjust JetMax robotic arm to the flat view. For installation detail, you can refer to “**[7.6.1 Camera Horizontal Installation]()**” in this folder.

### 7.6.3 Project Logic

Step 1: [Retrieve](https://context.reverso.net/%E7%BF%BB%E8%AF%91/%E8%8B%B1%E8%AF%AD-%E4%B8%AD%E6%96%87/retrieve) the camera image

Process the real-time image by OpenCV

Step 2: Image binarization

OpenCV represents all pixels in an image with 0 and 1 and displays the pixel with a value of 0 in black and the pixel with a value 1 in white.

Step 3: Dilation and Erosion

The purpose of erosion process is to debur the boundaries of the image. Dilation process will expand the boundaries of the image to fill the non-targeted pixel points at the boundaries or inside of the targeted object.

Step 4: Find out the contour location

Find out the contour location of the targeted object by demarcating the black and white areas.

Step 5: Frame the recognized color object.

Convert the recognized color objects (red, green and blue) into the coordinates before scaling, and then determine whether it is the largest color object.

The source code of the program is located in **/Home/ros/src/Ai_JetMax/scripts/color_detect.py**

<img class="common_img" src="D:/线上资料整理/1.Jetson系列/4. JetMax/7.OpenCV Basic Lesson/chapter_7/section_6/media/image2.png" style="width:500px" />

### 7.6.4 Project Process

<img class="common_img" src="D:/线上资料整理/1.Jetson系列/4. JetMax/7.OpenCV Basic Lesson/chapter_7/section_6/media/image3.png" style="width:50px" />The entered command must be strictly distinguished among uppercase, lowercase and spaces. In addition, you can press “**Tab**” to complete the keyword.

1. Double-click <img class="common_img" src="D:/线上资料整理/1.Jetson系列/4. JetMax/7.OpenCV Basic Lesson/chapter_7/section_6/media/image4.png" style="width:50px"  /> on system desktop.

2. Enter “**cd ros/src/Ai_JetMax**” command, and then press “Enter”to come to the category of game programming.

   ```py
   cd ros/src/Ai_JetMax
   ```

3. Then, enter “**rosrun Ai_JetMax color_detect.py**” command and press “Enter” to start the game.

   ```py
   rosrun Ai_JetMax color_detect.py
   ```

4. If you want to exit the game programming, press “**Ctrl+C**” in the terminal interface. If the exit fails, you can press it multiple times.

### 7.6.5 Project Outcome

> [!NOTE]
>
> **Please start this game under the solid color background and move the colored block with suitable speed.**

After running the program, JetMax will recognize the color of the objects within the detected range. When the object in red, green or blue is recognized, the terminal interface will frame the object and display the color name.

<img class="common_img" src="D:/线上资料整理/1.Jetson系列/4. JetMax/7.OpenCV Basic Lesson/chapter_7/section_6/media/image7.png" style="width:500px"  />

### 7.6.6 Project Analyst

After running the program, turn on the camera first through calling **`rospy.Subscriber`** function and retrieve the picture taken by the camera.

<img class="common_img" src="D:/线上资料整理/1.Jetson系列/4. JetMax/7.OpenCV Basic Lesson/chapter_7/section_6/media/image8.png" style="width:500px"  />

<img class="common_img" src="D:/线上资料整理/1.Jetson系列/4. JetMax/7.OpenCV Basic Lesson/chapter_7/section_6/media/image9.png" style="width:500px"  />

After the camera is turned on, call **`image_proc(img)`** function, and then perform a series of operation, including Lab conversion, image binaryzation, corrosion, dilation, outline locating, colored object framing and giving recognition information feedback.

- **Convert into Lab**

In the image information read by OpenCV, each frame is arranged by pixels composed of B, G and R color components. Great changes will take place in three-primary colors under different light condition.

Through calling **`cv2.cvtColor`** function, convert RGB color space into Lab color space. The program is as follow.

  <img class="common_img" src="D:/线上资料整理/1.Jetson系列/4. JetMax/7.OpenCV Basic Lesson/chapter_7/section_6/media/image10.png" style="width:500px" />

Before conversion, the program reduce noise of the picture, that is use **`cv2.GaussianBlur`** function for Gaussian filter.

The first parameter **`np.copy(img)`** refers to the input image.

The second parameter **`(5, 5)`** refers to the size of the Gaussian kernel. Larger kernel sizes generally result in a greater degree of filtering, more blurring in the output image, and increased computational complexity

The third parameter **`5`** represents the allowable variance near its average value in gaussian filtering; The larger this number, the greater the allowable variance around the average; The smaller the value, the smaller the allowable variance around the average.

- **Image binarization**

When turning on the camera, the information of preliminary processed image can only be effectively used after contour extraction and location determination. We process the real-time image by OpenCV.

OpenCV represents all pixels in an image with 0 and 1. It displays the pixel with a value of 0 in black and the pixel with a value 1 in white. This method is image binarization process.

Image binaryzation is performed through calling **`cv2.inRange`** function. The program is as follow:

<img class="common_img" src="D:/线上资料整理/1.Jetson系列/4. JetMax/7.OpenCV Basic Lesson/chapter_7/section_6/media/image11.png" style="width:500px"  />

- **Dilation and Erosion**

In order to reduce interference and make the image smoother, we process the grayscale image obtained after the binarization by dilation and erosion.

The purpose of erosion process is to debur the boundaries of the image. Dilation process will expand the boundaries of the image to fill the targeted pixel points at the boundaries or inside of the non-targeted object.

Call **`cv2.erode`** function for erosion and call **`cv2.dilate`** function for dilation. The program is as follow.

<img class="common_img" src="D:/线上资料整理/1.Jetson系列/4. JetMax/7.OpenCV Basic Lesson/chapter_7/section_6/media/image12.png" style="width:500px"  />

**`getStructuringElement`** function is used in processing. This function is used to generate structure element of different shapes.

The first parameter **`cv2.MORPH_RECT`** represents that the structure element is rectangle.

The second parameter **`(3, 3)`** represents the rectangle dimension is 3X3.

- **Find out the contour location**

All the previous steps on image is to obtain the location of the targeted object. Next, find out the contour location of the targeted object by demarcating the black and white areas.

The contour is located through calling **`cv2.findContours`** function. The specific program as follow:

<img class="common_img" src="D:/线上资料整理/1.Jetson系列/4. JetMax/7.OpenCV Basic Lesson/chapter_7/section_6/media/image13.png" style="width:500px" />

- **Frame the colored object**

After locating the contour, by using **`cv2.circle`** function, draw 2 circles. One serves as center, the other is used to frame the colored object.

<img class="common_img" src="D:/线上资料整理/1.Jetson系列/4. JetMax/7.OpenCV Basic Lesson/chapter_7/section_6/media/image14.png" style="width:500px"  />

Take **`cv2.circle(img, (int(center_x), int(center_y)), int(r), hiwonder.COLORS[color_name.upper()], 2)`** for example.

The first parameter **`img`** represents that the image corresponding to the colored object.

The second parameter **`(int(center_x), int(center_y))`** represents the center coordinate of the circle we draw, which is depended by the detected object.

The third parameter **`int(r)`** represents the radius of the circle, which is also depended by the detected object.

The fourth parameter **`hiwonder.COLORS[color_name.upper()]`** represents the color of the circle, which is also depended by the detected object.

The fifth parameter `2` represents the width of the circle line. The larger the value, the larger the width.

- **Recognition information feedback**

  After the colored object is recognized, the following information will be given.

1. In the program, through using **`cv2.putText`** function, add the obtained color information.

   <img class="common_img" src="D:/线上资料整理/1.Jetson系列/4. JetMax/7.OpenCV Basic Lesson/chapter_7/section_6/media/image15.png" style="width:500px"  />

   The first parameter **`img`** represents the specific colored image with word explanation.

   The second parameter **`color_name.upper()`** represents the color name of the detected object.

   The third parameter **`(int(center_x), int(center_y))`** represents the coordinate of the added words.

   The fourth parameter **`cv2.FONT_HERSHEY_SIMPLEX`** represents the font of the added words.

   The fifth parameter **`1.2`** represents the size of the added words.

   The sixth parameter **`(255, 255, 255)`** represents the color of the added words. These three values all ranges from 0 to 255. The words consist of three colors, including red, green and blue. The first value 255 represents red value, the second is green value, and the third is blue value.

   The seventh parameter **`2`** represents the font weight of the added words.

2. In program, use **`cv2.line`** function to draw 2 straight line and a cross to offer location of the colored object.

   <img class="common_img" src="D:/线上资料整理/1.Jetson系列/4. JetMax/7.OpenCV Basic Lesson/chapter_7/section_6/media/image16.png" style="width:500px"  />

Take **`cv2.line(img, (int(img_w / 2), int(img_h / 2 - 10)), (int(img_w / 2), int(img_h / 2 + 10)), (0, 255, 255), 2)`** for example.

The first parameter **`img`** represents the specific colored image of the drawn straight line.

The second parameter **`(int(img_w / 2), int(img_h / 2 - 10))`** represents the starting coordinate of the straight line

The third parameter “**`(int(img_w / 2), int(img_h / 2 + 10))`**” represents the ending coordinate of the straight line.

The fourth parameter “**(0, 255, 255)**” represents the color of the straight line. The setting method is the same as that of the sixth parameter in **Recognition information feedback**

The fifth parameter “**2**” represents the width of the line.

## 7.7 Color Threshold Adjustment

We all know that different light sources will have different effect on the color of the object. Therefore, there will be differences in recognition when perform color-related functions. If this difference affects the realization of the function, it needs to be eliminated.

To solve this problem above, we will learn LacConfigClient tool in this section .

### 7.7.1 Start LacConfigClient

1)  Open NoMachine software and double-click to open “**LacConfigClient**” in the interface.

<img class="common_img" src="../_static/media/chapter_7\section_7\media\image2.png" style="width:100px"  />

2)  After entering the software, you can see the LacConfigClient interface shown as follow:

<img class="common_img" src="../_static/media/chapter_7\section_7\media\image3.png" style="width:500px"  />

> [!NOTE]
>
> **Note: If there is no image returned by camera in the pop-up interface, it indicates the camera fails to connect. Then, you need to check whether the camera cable is connected well.**

### 7.7.2 The instruction and distribution of LacConfigClient Interface

The disLacConfigClient interface is divided into image display area and recognition adjustment area.

|     **Area Name**      |                    **Area Distribution**                     |
| :--------------------: | :----------------------------------------------------------: |
|     Image display      | <img class="common_img" src="../_static/media/chapter_7\section_7/media/image4.png" style="width:500px"  /> |
| Recognition adjustment | <img class="common_img" src="../_static/media/chapter_7\section_7/media/image5.png" style="width:500px"  /> |

- **Image Display Area**

|                           **Icon**                           |                   **Function Instruction**                   |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| <img class="common_img" src="../_static/media/chapter_7\section_7/media/image4.png" style="width:500px"  /> | The left side is the image processed. The right side is the original image. |

- **Recognition Adjustment Area**

In recognition adjustment area, the color properties can be adjusted. The corresponding functions of each part are shown in the following table.

|                           **Icon**                           |                   **Function Instruction**                   |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| <img class="common_img" src="../_static/media/chapter_7\section_7/media/image6.png" style="width:500px"  /> | Used to adjust the value of the L component of the image. (The function of A and B sliders bar is similar to this, both for adjusting the value of the corresponding component of the image.) |
| <img class="common_img" src="../_static/media/chapter_7\section_7/media/image7.png" style="width:500px"  /> |         Select the recognition color to be adjusted          |
| <img class="common_img" src="../_static/media/chapter_7\section_7/media/image8.png" style="width:500px"  /> |            Used to save the adjusted effect value            |
| <img class="common_img" src="../_static/media/chapter_7\section_7/media/image9.png" style="width:500px"  /> |        Used to add the types of the color recognized         |
| <img class="common_img" src="../_static/media/chapter_7\section_7/media/image10.png" style="width:500px"  /> |           Used to apply the adjusted effect value            |

### 7.7.3 Adjust the Default Color Effect

Take adjusting red as an example and the same method to other colors. The specific adjustment steps as follow:

1)  Start LacConfigClient on the system desktop. After camera is connected, select “**red**” in the color selection box of the recognition adjustment area.

<img class="common_img" src="../_static/media/chapter_7\section_7\media\image11.jpeg" style="width:500px"  />

2)  Point the camera at the color you want to adjust. Then, drag the slider of L,A and B in recognition adjustment area to adjust threshold until the color area to be recognized in the left screen becomes white and other areas become black.

<img class="common_img" src="../_static/media/chapter_7\section_7\media\image12.jpeg" style="width:500px"  />

LAB threshold adjustment parameters table:

| **Color Component** | **Color Component Value** | **Corresponding Color Range** |
| :-----------------: | :-----------------------: | :---------------------------- |
|          L          |           0~255           | Black- White (-L ~ +L)        |
|          A          |           0~255           | Green - Red (a ~ +a)          |
|          B          |           0~255           | Blue -Yellow (-b ~ +b)        |

Adjustment Tips:

1.  Firstly, adjust the value of L,A and B in the left side of adjustment area to 0 and the right side to 225.

2.  For example, we need to recognize red here. All red colors are near “**+a**” so keep the value of “**A**” component in the right side unchanged and drag the left slider to increase the A value.

3.  Then, modify the value of “**L**” and “**B**” components according to the surrounding. If the red is lighter, increase the value of “**L**” component in the left side. If the it is darker, decrease the value of "**L**" component in the right side. If the red is warmer, increase the value of "**B**" component in the left side; If it is colder, decrease the value of "**B**" component in the right side.

4.  Next, click “**Save**” button in recognition area to save the adjusted parameter values.

<img class="common_img" src="../_static/media/chapter_7\section_7\media\image13.jpeg" style="width:500px"  />

### 7.7.4 Add New Recognition Color 

In addition to the three built-in recognition colors, we can also add other colors. There are two methods to add.

1.  Adjust the LAB value of default colors to the LAB value of actual color.

2.  Use “**Add**” button to add new recognition color.

Based on the principle of easiest operation and fastest effect, this lesson only introduces the first method, we will introduce the first method in this lesson.

We’ll take adding purple as an example. The specific steps as follow:

1)  Click “**LAB_Tool**” in the system desktop. After the camera is connected, select “**black**” in the red box.

<img class="common_img" src="../_static/media/chapter_7\section_7\media\image14.jpeg" style="width:500px"  />

2)  Point the camera at purple color. Then, drag the corresponding sliders of L, A, and B until the color area to be recognized in the left screen becomes white and other areas become black.

<img class="common_img" src="../_static/media/chapter_7\section_7\media\image15.jpeg" style="width:500px"  />

3. Click “**Save**” button in recognition area to save the adjusted parameter values.

   <img class="common_img" src="../_static/media/chapter_7\section_7/media/image16.jpeg" style="width:500px"  />
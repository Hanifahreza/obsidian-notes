## Read and Show Image
```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

%matplotlib inline

img = cv2.imread('mountain.jpg', 1)
# img = cv2.resize(img, (500,500))
print(img.shape)
cv2.imshow('mountain', img)
cv2.waitKey(0)
cv2.destroyAllWindows()

#============plot===========
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
plt.imshow(img)
```
![[Pasted image 20231108210831.png]]
## Accessing and Modifying Pixel Values
```python
img = cv2.imread('mountain.jpg', 1)
img2 = cv2.imread('mountain.jpg', 1)
img3 = cv2.imread('mountain.jpg', 1)
img[20, 40] = 255 # img[y,x]
img2[0:20,0:40] = 255

roi = img[50:100, 100:150]
img3[0:50, 0:50] = roi 
cv2.imshow('mountain', img)
cv2.imshow('mountain2', img2)
cv2.imshow('mountain3', img3)
cv2.waitKey(0)
cv2.destroyAllWindows()

#============plot===========
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
img2 = cv2.cvtColor(img2, cv2.COLOR_BGR2RGB)
img3 = cv2.cvtColor(img3, cv2.COLOR_BGR2RGB)
plt.subplot(131),plt.imshow(img),plt.title('pixels')
plt.xticks([]), plt.yticks([])
plt.subplot(132),plt.imshow(img2),plt.title('area')
plt.xticks([]), plt.yticks([])
plt.subplot(133),plt.imshow(img3),plt.title('roi')
plt.xticks([]), plt.yticks([])
plt.show()
```
![[Pasted image 20231108211010.png]]
## Splitting and Merging Image Channels
```python
img = cv2.imread('mountain.jpg', 1)
b, g, r = cv2.split(img)
img2 = cv2.merge((r, g, b))
img3 = cv2.merge((g, r, b))

plt.subplot(131),plt.imshow(img),plt.title('bgr')
plt.xticks([]), plt.yticks([])
plt.subplot(132),plt.imshow(img2),plt.title('rgb')
plt.xticks([]), plt.yticks([])
plt.subplot(133),plt.imshow(img3),plt.title('grb')
plt.xticks([]), plt.yticks([])
plt.show()
```
![[Pasted image 20231108211242.png]]
## Plot Histogram of Image
```python
img = cv2.imread('road.jpg',1)
hist = cv2.calcHist([img],[0],None,[256],[0,256]) # only blue channel

"""images : it is the source image of type uint8 or float32. it should be given in square brackets, ie, "[img]".
channels : it is also given in square brackets. It is the index of channel for which we calculate histogram. For example, if input is grayscale image, its value is [0]. For color image, you can pass [0], [1] or [2] to calculate histogram of blue, green or red channel respectively.
mask : mask image. To find histogram of full image, it is given as "None". But if you want to find histogram of particular region of image, you have to create a mask image for that and give it as mask. (I will show an example later.)
histSize : this represents our BIN count. Need to be given in square brackets. For full scale, we pass [256].
ranges : this is our RANGE. Normally, it is [0,256]."""

img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
plt.subplot(1,2,1), plt.imshow(img)
plt.subplot(1,2,2), plt.plot(hist)
```
![[Pasted image 20231108211657.png]]
```python
img = cv2.imread('road.jpg',1)
color = ('b','g','r')
for i,col in enumerate(color):
    histr = cv2.calcHist([img],[i],None,[256],[0,256])
    plt.plot(histr,color = col)
    plt.xlim([0,256])
plt.show()
```
![[Pasted image 20231108211746.png]]
## Image Blurring
```python
img = cv2.imread('1.png')
blur = cv2.blur(img,(5,5))

cv2.imshow('original', img)
cv2.imshow('blur', blur)
cv2.waitKey(0)
cv2.destroyAllWindows()

plt.subplot(121),plt.imshow(img),plt.title('Original')
plt.xticks([]), plt.yticks([])
plt.subplot(122),plt.imshow(blur),plt.title('Blurred')
plt.xticks([]), plt.yticks([])
plt.show()
```
![[Pasted image 20231108211842.png]]
## 2D Convolution ( Image Filtering )
```python
img = cv2.imread('1.png')
kernel = np.ones((5,5),np.float32)/25
img2 = cv2.filter2D(img,-1,kernel)

cv2.imshow('original', img)
cv2.imshow('blur', img2)
cv2.waitKey(0)
cv2.destroyAllWindows()

plt.subplot(121),plt.imshow(img),plt.title('Original')
plt.xticks([]), plt.yticks([])
plt.subplot(122),plt.imshow(img2),plt.title('convolution')
plt.xticks([]), plt.yticks([])
plt.show()
```
![[Pasted image 20231108212236.png]]
## Gaussian Blurring
```python
img = cv2.imread('1.png')
blur = cv2.GaussianBlur(img,(5,5),0)
cv2.imshow('original', img)
cv2.imshow('Gaussian', dst)
cv2.waitKey(0)
cv2.destroyAllWindows()

plt.subplot(121),plt.imshow(img),plt.title('Original')
plt.xticks([]), plt.yticks([])
plt.subplot(122),plt.imshow(blur),plt.title('Gaussian')
plt.xticks([]), plt.yticks([])
plt.show()
```
![[Pasted image 20231108212332.png]]
## Bitwise AND, OR, XOR
```python
array = '1 1 1 1 1 0 0 0 1 1 1 1 1 0 0 0 1 1 1 1 1 0 0 0 1 1 1 1 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0'
array = array.split(' ')
array = [int(x) for x in array]
array = np.reshape(array, (8,8))

array2 = '0 0 0 1 1 1 1 1 0 0 0 1 1 1 1 1 0 0 0 1 1 1 1 1 0 0 0 1 1 1 1 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0'
array2 = array2.split(' ')
array2 = [int(x) for x in array2]
array2 = np.reshape(array2, (8,8))

_and = cv2.bitwise_and(array, array2)
_or = cv2.bitwise_or(array, array2)
_xor = cv2.bitwise_xor(array, array2)

#============plot===========
fig, axs = plt.subplots(1,5,figsize=(10,4))

axs[0].imshow(array,cmap="gray")
axs[0].set_title('1')
print(array)

axs[1].imshow(array2,cmap="gray")
axs[1].set_title('2')
print(array2)

axs[2].imshow(_and,cmap="gray")
axs[2].set_title('and')
#print(_and)

axs[3].imshow(_or,cmap="gray")
axs[3].set_title('or')
#print(_or)

axs[4].imshow(_xor,cmap="gray")
axs[4].set_title('xor')
#print(_xor)
```
![[Pasted image 20231108212423.png]]
## Basic Threshold Functions
- If the pixel value is smaller than the threshold, it is set to 0, 
- Otherwise it is set to a maximum value
```python
array = '255 220 185 150 115 80 45 10 255 220 185 150 115 80 45 10 255 220 185 150 115 80 45 10 255 220 185 150 115 80 45 10 255 220 185 150 115 80 45 10 255 220 185 150 115 80 45 10 255 220 185 150 115 80 45 10 255 220 185 150 115 80 45 10'
array = array.split(' ')
array = [int(x) for x in array]
print(array)
img = np.reshape(array, (8,8))

ret,thresh1 = cv2.threshold(img,127,255,cv2.THRESH_BINARY)
ret,thresh2 = cv2.threshold(img,127,255,cv2.THRESH_BINARY_INV)
ret,thresh3 = cv2.threshold(img,127,255,cv2.THRESH_TRUNC)
ret,thresh4 = cv2.threshold(img,127,255,cv2.THRESH_TOZERO)
ret,thresh5 = cv2.threshold(img,127,255,cv2.THRESH_TOZERO_INV)

titles = ['Original Image','BINARY','BINARY_INV','TRUNC','TOZERO','TOZERO_INV']
images = [img, thresh1, thresh2, thresh3, thresh4, thresh5]

for i in range(6):
    plt.subplot(2,3,i+1),plt.imshow(images[i],'gray')
    plt.title(titles[i])
    plt.xticks([]),plt.yticks([])
plt.show()
```
![[Pasted image 20231108212521.png]]
## Adaptive Threshold
- The algorithm calculate the threshold for a small regions of the image
- So we get different thresholds for different regions of the same image
- It gives us better results for images with varying illumination
```python
img = cv2.imread('2.jpg',0)
img = cv2.medianBlur(img,5)
ret,th1 = cv2.threshold(img,127,255,cv2.THRESH_BINARY)
th2 = cv2.adaptiveThreshold(img,255,cv2.ADAPTIVE_THRESH_MEAN_C,\
            cv2.THRESH_BINARY,11,2)
th3 = cv2.adaptiveThreshold(img,255,cv2.ADAPTIVE_THRESH_GAUSSIAN_C,\
            cv2.THRESH_BINARY,11,2)
# Block Size: 11 - It decides the size of neighbourhood area.
# C: 2 - It is just a constant which is subtracted from the mean or weighted mean calculated.

cv2.imshow('img1', img)
cv2.imshow('img2', th1)
cv2.imshow('mean', th2)
cv2.imshow('Gaussian', th3)
cv2.waitKey(0)
cv2.destroyAllWindows()

#============plot===========
titles = ['Original Image', 'Global Thresholding (v = 127)',
            'Adaptive Mean Thresholding', 'Adaptive Gaussian Thresholding']
images = [img, th1, th2, th3]
for i in range(4):
    plt.subplot(2,2,i+1),plt.imshow(images[i],'gray')
    plt.title(titles[i])
    plt.xticks([]),plt.yticks([])
plt.show()
```
![[Pasted image 20231108212719.png]]
## Otsu's Binarization
- It automatically calculates a threshold value from image histogram for a bimodal image
```python
import cv2 as cv
import numpy as np
from matplotlib import pyplot as plt

img = [cv.imread]
assert img is not None, "file could not be read, check with os.path.exists()"

# global thresholding
ret1,th1 = [cv.threshold]

# Otsu's thresholding
ret2,th2 = [cv.threshold]

# Otsu's thresholding after Gaussian filtering
blur = [cv.GaussianBlur]
ret3,th3 = [cv.threshold]

# plot all the images and their histograms
images = [img, 0, th1,
img, 0, th2,
blur, 0, th3]

titles = ['Original Noisy Image','Histogram','Global Thresholding (v=127)',
'Original Noisy Image','Histogram',"Otsu's Thresholding",
'Gaussian filtered Image','Histogram',"Otsu's Thresholding"]

for i in range(3):
	plt.subplot(3,3,i*3+1),plt.imshow(images[i*3],'gray')
	plt.title(titles[i*3]), plt.xticks([]), plt.yticks([])
	plt.subplot(3,3,i*3+2),plt.hist(images[i*3].ravel(),256)	
	plt.title(titles[i*3+1]), plt.xticks([]), plt.yticks([])
	plt.subplot(3,3,i*3+3),plt.imshow(images[i*3+2],'gray')
	plt.title(titles[i*3+2]), plt.xticks([]), plt.yticks([])

plt.show()
```
![[Pasted image 20231109113111.png]]
## Canny Edge Detection
```python
img = cv2.imread('1.png', 1)
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
blur = cv2.GaussianBlur(gray, (5,5), 0)
canny = cv2.Canny(blur, 50 , 150)
cv2.imshow("original",img)
cv2.imshow('canny', canny)
cv2.waitKey(0)
cv2.destroyAllWindows()

#============plot===========
canny = cv2.cvtColor(canny, cv2.COLOR_BGR2RGB)
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
fig, axs = plt.subplots(1,2,figsize=(10,4))

axs[0].imshow(img)
axs[0].set_title('original')
axs[1].imshow(canny,cmap="gray")
axs[1].set_title('canny')
```
![[Pasted image 20231109094505.png]]
## Image Gradients Edge Detection
- Sobel operators is a joint Gausssian smoothing plus differentiation operation, so it is more resistant to noise
- We can specify the direction of derivatives to be taken, vertical or horizontal  
- We can also specify the size of kernel by the argument `ksize`
- If `ksize` = -1, a 3x3 Scharr filter is used which gives better results than 3x3 Sobel filter
```python
img = cv2.imread('sudoku.png',0)
laplacian = cv2.Laplacian(img,cv2.CV_64F)
sobelx = cv2.Sobel(img,cv2.CV_64F,1,0,ksize=5)
sobely = cv2.Sobel(img,cv2.CV_64F,0,1,ksize=5)

plt.subplot(2,2,1),plt.imshow(img,cmap = 'gray')
plt.title('Original'), plt.xticks([]), plt.yticks([])
plt.subplot(2,2,2),plt.imshow(laplacian,cmap = 'gray')
plt.title('Laplacian'), plt.xticks([]), plt.yticks([])
plt.subplot(2,2,3),plt.imshow(sobelx,cmap = 'gray')
plt.title('Sobel X'), plt.xticks([]), plt.yticks([])
plt.subplot(2,2,4),plt.imshow(sobely,cmap = 'gray')
plt.title('Sobel Y'), plt.xticks([]), plt.yticks([])
plt.show()
```
![[Pasted image 20231109111414.png]]
## Contours
- Contours can be explained simply as a curve joining all the continuous points (along the boundary), having same color or intensity
- The contours are a useful tool for shape analysis and object detection and recognition
```python
img = cv2.imread('road.jpg',1)
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
plt.subplot(1,2,1),plt.imshow(img)
plt.title('image'), plt.xticks([]), plt.yticks([])

gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
ret, thresh = cv2.threshold(gray, 127, 255, 0)
contours, hierarchy = cv2.findContours(thresh, cv2.RETR_TREE, cv2.CHAIN_APPROX_SIMPLE)
img2 = cv2.drawContours(img, contours, -1, (0,255,0), 2)

print(len(contours))

cv2.imshow('mountain',img2)
cv2.waitKey(0)
cv2.destroyAllWindows()

plt.subplot(1,2,2),plt.imshow(img2,cmap='gray')
plt.title('image2'), plt.xticks([]), plt.yticks([])
plt.show()
```
![[Pasted image 20231109094748.png]]
## Lines, Rectangles, and Text on Image
```python
img = cv2.imread('2.jpg', 1)
cv2.line(img, (0,0), (img.shape[1],img.shape[0]), (0,255,0),5)
cv2.line(img, (img.shape[1],0), (0,img.shape[0]), (0,255,0),5)
cv2.rectangle(img, (80,30), (320,400), (0,0,255),5)
font = cv2.FONT_HERSHEY_SIMPLEX
cv2.putText(img, 'jacob', (300,500), font, 1, (255,255,255), 2, cv2.LINE_AA)
cv2.imshow('img', img)
cv2.waitKey(0)
cv2.destroyAllWindows()

#============plot===========
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
plt.imshow(img)
```
![[Pasted image 20231109094848.png]]
## Mask Operation
- Get a **specific region** of an image as defined by a **mask**
```python
# import required libraries
import cv2
import numpy as np

# read input image
img = cv2.imread('car.jpg')

# Convert BGR to HSV
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)

# define range of blue color in HSV
lower_yellow = np.array([15,50,180])
upper_yellow = np.array([40,255,255])

# Create a mask. Threshold the HSV image to get only yellow colors
mask = cv2.inRange(hsv, lower_yellow, upper_yellow)

# Bitwise-AND mask and original image
result = cv2.bitwise_and(img,img, mask= mask)

# display the mask and masked image
cv2.imshow('Ori',img)
cv2.waitKey(0)
cv2.imshow('Mask',mask)
cv2.waitKey(0)
cv2.imshow('Masked Image',result)
cv2.waitKey(0)
cv2.destroyAllWindows()
```
![[Pasted image 20231109113942.png]]
![[Pasted image 20231109113847.png]]
![[Pasted image 20231109113907.png]]
## Face Detection using CascadeClassifier
- Object Detection using Haar feature-based cascade classifiers (2001)
- Use [[Boosting#AdaBoost|AdaBoost]]
```python
face_cascade = cv2.CascadeClassifier("haarcascade_frontalface_default.xml")
img = cv2.imread('1.jpg')
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
faces = face_cascade.detectMultiScale(gray, scaleFactor = 1.05, minNeighbors = 5)

for x,y,w,h in faces:
    img = cv2.rectangle(img, (x,y),(x+w,y+h),(0,255,0),5)

cv2.imshow("face", img)
cv2.waitKey(0)
cv2.destroyAllWindows()

#============plot===========
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
plt.imshow(img)
```
![[Pasted image 20231109095205.png]]
## Template Matching
```python
import cv2
import numpy as np

img = cv2.imread('Dhoni-and-Virat.jpg',1)
cv2.imshow('Original',img)
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)

template = cv2.imread('virat.jpg',0)
cv2.imshow('Template',template)
w,h = template.shape[0], template.shape[1]

matched = cv2.matchTemplate(gray,template,cv2.TM_CCOEFF_NORMED)
threshold = 0.8

loc = np.where( matched >= threshold)

for pt in zip(*loc[::-1]):
   cv2.rectangle(img, pt, (pt[0] + w, pt[1] + h), (0,255,255), 2)

cv2.imshow('Matched with Template',img)
```
![[Pasted image 20231109095739.png]]
![[Pasted image 20231109095749.png]]
![[Pasted image 20231109095758.png]]
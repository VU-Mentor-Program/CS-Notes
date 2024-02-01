---
tags: 
Created: 2023-09-21 13:57:36
Links: "[[Pervasive Computing]]"
---
# Windowing
Many of the image processing operations can be selectively applied to a user defined region within the image. This region is known as the **region of interest**(**ROI**).
# Point processing
- When you change the brightness on your TV you change each pixel in the same way.
- These operations can be the result of applying an arithmetic function to the pixel
## Histogram
An image histogram plots how often each pixel value appears in the image against the value themselves.
![[histogram-4-1843420717.png|500]]
- **Histogram stretching**: 
  $f_1$ is the left-most non-zero bin in the histogram
  $f_2$ is the right-most non-zero bin in the histogram of the input image.$$g(x,y)=\frac{255}{f_{2}-f_{1}}\times(f(x,y)-f_{1})$$
- **Segmentation**: We can separate objects from the background with tools such as Thresholding or Edge detection
	- Thresholding: Any pixel brighter than a certain level should become white, all others darker than that level will become black -> high contrast black and white image
# Neighbourhood processing
- The value of a pixel in the output is determined by the value of the pixel at the same position in the input **and the neighbours**, together with a neighbourhood processing
- Use a small neighbourhood of a pixel in an input image to get a new brightness value in the output image
- **Correlation**: 
	- Correlation is an operation which works by scanning through the image and applying a mask to each pixel.
	- The mask is called kernel
	- The kernel is filled by numbers, not always equal to one—denoted *kernel coefficients*.
	- These coefficients weight the pixel value they are covering
	- The output of the correlation is a sum of weighted pixel values.
- Edge detection: Edges are local discontinuity in the pixel value that exceeds a given threshold
	- Edge detection can be obtained by a correlation with a kernel
# Morphological operations
Morphology is a branch of image processing which is particularly useful for analysing **shapes** in images.
- Kernels are **structuring elements** and contain 0's and 1's
  ![[SCR-20230921-tncf.png|300]]
- Structuring elements are applied using either a **Hit** (Dilation) or a **Fit** (Erosion) operation
	- *Erosion*: Center the STREL on each '1' pixel. If a neighbour is '0', then the pixel will be switched to '0'
	  ![[SCR-20230921-towo.png|300]]
	  The binary image decreases in size, small objects disappear, objects split into smaller objects
	- *Dilation*: Center the STREL on each '0' pixel. If a neighbour is '1', then the pixel will be switched to '1'
	  ![[SCR-20230921-toqo.png|300]]
	  The binary image increases in size, objects merge, and small holes are filled
	- *Closing*: Dilation + Erosion -> removes small holes and joins narrow isthmuses between objects
	- *Opening*: Erosion + Dilation -> removes small, isolated noisy objects while main object is preserved
# BLOB analysis
**B**inary **L**arge **OB**jet refers to a group of connected pixels in a binary image. Small objects are considered as noise.
- Connectivity: Decides which pixels are neighbours. Connected pixels are called a BLOB (connected component)
	- ![[Blob connectivity.png|500]]
- Labeling: Extracted BLOBs are labeled differently

Matlab has a function `bwlabel` which returns a matrix with labels and the number of BLOBs
# Conclusion
- Even before classification, one can extract some useful context information from the environment.
- You know now how to process an acquired image by histogram stretching, thresholding, filtering and morphological operations.
- You will practice in Lab3 with counting objects in an image by using connected components labeling

---
References:
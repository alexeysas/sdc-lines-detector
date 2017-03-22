#**Finding Lane Lines on the Road** 

##Writeup Template

###You can use this file as a template for your writeup if you want to submit it as a markdown file. But feel free to use some other method and submit a pdf if you prefer.

---

**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./test_pipeline/HLS_filter.jpg "HLS filtered"
[image3]: ./test_pipeline/canny.jpg "Canny Edges"
[image4]: ./test_pipeline/region.jpg "Region of Interest"
[image5]: ./test_pipeline/segments.jpg "Hough Segments"

---

### Reflection

###

The processing pipeline consisted of 6 steps. 

1. I converted the images to HLS color scheme to extract yellow and white color from the image - the most common color for the road lines. Experementaly found that HLS provides better results compared to RGB and HSV for this specific task. This step is mostly used for the optional challenge video due to its complex shadows nature. First two test videos works fine with this step skipped with minimum noticible artifacts. 

![alt text][image2]

2. Applyed grayscale to make single channel image.

3. Removed noise using Gaussian Blur so reduce chance of detecting noisy lines.

4. Extracted edges using Canny edge detector gradients based algorithm

![alt text][image3]

5. Applied Region Of Interest to consider only area in front of car to reduce chance of detecting unrelevant lines.

![alt text][image4]

6. Used Probabilistic Hough Line Transform to find possible lines.

![alt text][image5]

7. Removed lines with horizontal scope as they are unlikely road lines. 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


###3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...

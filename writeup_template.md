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

---

### Reflection

###

The processing pipeline consisted of 6 steps. 

1. I converted the images to HLS color scheme to extract yellow and white color from the image - the most common color for the road lines. Experementaly found that HLS provides better results compared to RGB and HSV for this specific task. This step is mostly used for the optional challenge video due to its complex shadows nature. First two test videos works fine with this step skipped with minimum noticible artifacts. 

![alt text][image2]

2. Applyed grayscale, then I .... 

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by ...

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


###2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when ... 

Another shortcoming could be ...


###3. Suggest possible improvements to your pipeline

A possible improvement would be to ...

Another potential improvement could be to ...

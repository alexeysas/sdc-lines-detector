# **Finding Lane Lines on the Road**

[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"
[image2]: ./test_pipeline/HLS_filter.jpg "HLS filtered"
[image3]: ./test_pipeline/canny.jpg "Canny Edges"
[image4]: ./test_pipeline/region.jpg "Region of Interest"
[image5]: ./test_pipeline/segments.jpg "Hough Segments"
[image6]: ./test_pipeline/final.jpg "Final image"
[image7]: ./test_images/solidYellowLeft.jpg "Initial"

[video1]: ./test_videos_output/solidWhiteRight.mp4 "Sample 1"

---

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect the work in a written report

![alt text][image7]

### Reflection

The processing pipeline consisted of 6 steps. 

1. I converted the images to HLS color scheme to extract yellow and white color from the image - the most common color for the road lines. Experimentally found that HLS provides better results compared to RGB and HSV for this specific task. This step is mostly used for the optional challenge video due to its complex shadows nature. First two test videos works fine with this step skipped with minimum noticeable artifacts. 

![alt text][image2]

2. Applied grayscale to make single channel image.

3. Removed noise using Gaussian Blur so reduce chance of detecting noisy lines.

4. Extracted edges using Canny edge detector gradients based algorithm

![alt text][image3]

5. Applied Region Of Interest to consider only area in front of car to reduce chance of detecting irrelevant lines.

![alt text][image4]

6. Used Probabilistic Hough Line Transform to find possible lines.

![alt text][image5]

7. Removed lines with horizontal scope as they are unlikely road lines. 

8. As a final step we need to create two lines based on segments data. The easiest way to collect identified segments to left and right cluster of lines is to use slope sign. However, this method can produce some artifacts if we have some noisy lines identified far from the original lines. So I've tried to apply different approach. The idea is to create lines clusters based on angle and distance between lines (not points). After clusters are created if we have exact two clusters - we are done. If we have 3 or more clusters we need to get rid of noisy clusters using some metric. Good metric is an open question there. 

9. Finally I used linear regression to combine lines together and got final result.

![alt text][image6]


### Shortcomings 

1. The potential shortcoming is that approach will not work so good if we have lines different color from white and yellow. Even if first step(HLS color filter) is removed to help with this tasks there will be difficulties in detecting lines for complex shadowed roads.

2. Due to imperfect nature of my clustering algorithm there will be issues wilt line detection for the noisy road especially with long vertical artifacts. 

3. As we filtered out mostly-horizontal segments - algorithm is not useful for the detecting lines for the turns.

### Improvements

1. One of the possible improvement is to find a way to use average lines from the previous frames in the video stream to correct wrong lines behavior and make them more smooth. Also this historic data can definitely help to improve clustering algorithm metric to filter out noisy segments.

2. Another improvement is to fit curved lines instead of linear regression approach. For example some ideas can be borrowed from this work:  https://arxiv.org/pdf/1501.03124.pdf

### Samples

https://github.com/alexeysas/sdc-lines-detector/blob/master/test_videos_output/solidWhiteRight.mp4
https://github.com/alexeysas/sdc-lines-detector/blob/master/test_videos_output/solidYellowLeft.mp4
https://github.com/alexeysas/sdc-lines-detector/blob/master/test_videos_output/challenge.mp4

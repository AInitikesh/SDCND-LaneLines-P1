**Finding Lane Lines on the Road**

The goals / steps of this project are the following:
* Make a pipeline that finds lane lines on the road
* Reflect on your work in a written report


[//]: # (Image References)

[image1]: ./examples/grayscale.jpg "Grayscale"

---

### Reflection

### 1. Describe your pipeline. As part of the description, explain how you modified the draw_lines() function.

My pipeline consisted of 6 steps. First, I converted the images to grayscale, then applied gausian_blur on the image with kernel of size 5. In third step I used canny edge function to detect the boundries. In fourth step I defined the region that I want to focus on (lane lines) and masked it. In 5th step I applied hough transfomation to detect the lane lines in masked region. In step 6th I merged the real input image and the lines detected in step 5.

In order to draw a single line on the left and right lanes, I modified the draw_lines() function by identifing the slopes and y intercepts of each lines using np.polyfit. Then I made seperate arrays of all the points and slopes contibuting to left lane line and right lane line by making an hypothesis that left lane lines will have slopes between [0.45, 0.75] and right lane lines between [-0.85, -0.6] . Then I found the mean of all left and right points as well as slopes. Using mean slope, mean y and mean x of left and right lane lines I calculated the y intercepts using line equation b = y - mx. Haivng all this I calulated the upper and lower x coordinates for left and right lane lines using equation x = (y - b) / m where y is the mean or max value that an y intecept can have ie for calculating upper x coordinate y min is used and for calculating lower x coordinates y max is used. Now we have (x1 = upper_left_x, y1 = y_min), (x2 = lower_left_x, y2 = y_max) for left lane line and (x1 = upper_right_x, y1 = y_min), (x2 = lower_right_x, y2 = y_max) for rifht lane line.

If you'd like to include images to show how the pipeline works, here is how to include an image: 

![alt text][image1]


### 2. Identify potential shortcomings with your current pipeline


One potential shortcoming would be what would happen when the car moves of the lane lines. If the lane lines move off the masked region this model would fail. 

Another shortcoming could be the environmental condtions like what if another car comes upon a lane line. Even there may be a road which has poor or no lane lines marked. Day and night conditions may affect.


### 3. Suggest possible improvements to your pipeline

A possible improvement would be to detect all the objects that may come as an hurdle in lane detection ie cars , pedestrians. 

Another potential improvement could be to focus on road and not just on the lane lines. we can even identify the end to end road boundries and the detect in which lane does the car lies.

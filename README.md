# **Finding Lane Lines on the Road** 

---

### 1. 5 Steps of Finding Lane Lines Pipeline and Introduction of enhanced drawing lines

Step1) COLOR SELECTION  
Firstly, I select colors above RGB thresholds. The colors below the thresholds are processed to black [0,0,0].  
This selection could be helpful to focus on the range of specific colors.  
  
Step2) REGION MASKING  
I use triangular region masking. Basically, this is to focus on the specific region in this masking.  
However, the three endpoints used for the masking could be also utilized for the enhanced draw line function as parameters.  
  
Step3) CANNY EDGE DETECTION  
I convert the image color to gray and then apply it to canny function. This function helps to detect edges of the image.  
  
Step4) HOUGH TRANSFORM  
I detect the lines which are what I want by using hough function.  
  
Step5) ENHANCED DRAW FUNCTION  
Before drawing the edges to one line by using cv2.line function, I have to filter the lane lines by comparision of slopes.  
The slopes have to be equal or more than the absolute minimum value of the slope used in the triangular masking.  
And then distributing the edges to left side or right side by checking whether these are positive or negative values.  
After finding two endpoints and the fit linear polynominal slope and fit y-axis value in each left side and right side, 
I draw the left line and right line by using cv2.line() with the information.  
  
### 2. Identify potential shortcomings with your current pipeline
  
One shortcoming is that the color selection process and the region masking are used appropriately?  
In the 3rd step (CANNY EDGE DETECTION), I think that converting the image color to gray is enough to detect edges.  
Of course, by using the color selection and the region masking, I could focus on the specific color range and region before applying to convert the image to gray. However, by using them, some necessary lane line information could be filtered.  
  
Another shortcoming could be the complex configuration of the parameters. I have designed some values of the triangular region masking are utilized to draw line as thresholds. I intended to reduce the number of configuration parameters by give some dependency with each other. However, it could backfire on me. Because of the dependency, the configuration of the parameters could be more tricky.
  
### 3. Suggest possible improvements to your pipeline
  
Frist of all, I have to research the dependency between the steps and then how to effect in each other.  
And then I collect how many parameters need to be configured in the pipeline.  
After that I have to find a way how to configure them easily. (i.e. some tools)  
  
Another thing is that I have to make a function with the logic for the part of enhanced line drawing.  
I should consider how to handle with value error by some missing information when drawing the lines (i.e. error handling).  
I have to enhance the functionality of distribution between left lines and right lines. Currently, I have not yet considered if the calculated slope value is infinite. Considering this case, how about adding the x-axis value of the center of the car?  Because the slope value closing infinite means that we are driving on straight at least.

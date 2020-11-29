## Advanced Lane Finding
[![Udacity - Self-Driving Car NanoDegree](https://s3.amazonaws.com/udacity-sdc/github/shield-carnd.svg)](http://www.udacity.com/drive)
![Lanes Image](./examples/example_output.jpg)

The goal for this project was to create a pipeline of image processing procedures that would ifentify and mark the car lanes on the  images of the road. This pippeline then shold be applicable as a porcessing tool that can be applied to a sequence of frames from a given video.
---

The steps of this project are the following:

* Compute the camera calibration matrix and distortion coefficients given a set of chessboard images.
* Apply a distortion correction to raw images.
* Use color transforms, gradients, etc., to create a thresholded binary image.
* Apply a perspective transform to rectify binary image ("birds-eye view").
* Detect lane pixels and fit to find the lane boundary.
* Determine the curvature of the lane and vehicle position with respect to center.
* Warp the detected lane boundaries back onto the original image.
* Output visual display of the lane boundaries and numerical estimation of lane curvature and vehicle position.

The images for camera calibration are stored in the folder called `camera_cal`.  The images in `test_images` are for testing the pipeline on single frames. 

The Jupyter notebook Project2.ipynb goes through all steps and displays the results of intermediate steps with comments.

There is a cell with the original process_image() method that always searches the lanes from scratch in each frame.

There is also a cell with the Pipeline class whose process_image() member method stores the polynomial coefficients and re-uses them between the frames for efficiency. There is a code for a sanity check that compares the lanes in each new frame and if they do not pass it reuse the lane coefficients from the previous frame.

The Pipeline's process_image() works really well on the `project_video.mp4`.
It does not work well on the `challenge_video.mp4` and I did spend some time analyzing the root cause.
It clear that the lane detection procedure gets confused by the lines created by the shadow from the road separator and from uneven pavement in the middle of the car lane. I saved few frames from the clip and applied the same filters used on the test_images and the results were clearly pointing to a problem. There were usually more than 2 lines.  I could not figure out the filtering technique that would help. Would be curious to know how this is avoided in real applications.



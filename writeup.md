## Project: Search and Sample Return

### Notebook Analysis
#### 1. Run the functions provided in the notebook on test images (first with the test data provided, next on data you have recorded). Add/modify functions to allow for color selection of obstacles and rock samples.
To locate passable areas, the captured image is processed with a threshold filter. The threshold of `> rgb(160, 160, 160)` turned out to be good. For rock sample detection I created the `rock_sample_detection()` function, which uses a threshold of `rgb(160, 160, 160)` for the rock samples.


#### 1. Populate the `process_image()` function with the appropriate analysis steps to map pixels identifying navigable terrain, obstacles and rock samples into a worldmap.  Run `process_image()` on your test data using the `moviepy` functions provided to create video output of your result.
For the `process_image()` function I first added functionality in order to filtering out the navigable terrain, obstacles, and samples and then added the remaining steps to convert the filtered image to rover coordinates and convert those coordinates to world coordinates based on the rover's position. I then use these coordinates to update the world map.

### Autonomous Navigation and Mapping

#### 1. Fill in the `perception_step()` (at the bottom of the `perception.py` script) and `decision_step()` (in `decision.py`) functions in the autonomous mapping scripts and an explanation is provided in the writeup of how and why these functions were modified as they were.
The `perception_step()` function is closely related to the `process_image()` function from the jupyter notebook. It extends the function by also updating the `Rover.vision_image` and `Rover.nav_angles` and returning the updated Rover instance.

#### 2. Launching in autonomous mode your rover can navigate and map autonomously.  Explain your results and how you might improve them in your writeup.  

**Note: running the simulator with different choices of resolution and graphics quality may produce different results, particularly on different machines!  Make a note of your simulator settings (resolution and graphics quality set on launch) and frames per second (FPS output to terminal by `drive_rover.py`) in your writeup when you submit the project so your reviewer can reproduce your results.**  

I ran the simulator at a resolution of 1280x720 with fantastic graphics quality.
Currently I only changed the `perception_step()` function. The rover completes the given tasks `(with a fidelity of round about 62 %)` except the NASA Sample Return Challenge, where it also has to pick up all the sample rocks and returning them to the starting point. In the future I will be adding the optimisation tips like a wall following functionality or only taking valid transformed images into account by checking if the rover's roll and pitch angles are near zero. At the moment, under certain circumstances, there is still the problem that the rover drives permanently in a circle or does not recognize smaller obstacles. In Addition the rover could save a lot of time if it detects areas that have already been used and does not explore them several times.

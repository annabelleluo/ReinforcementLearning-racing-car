 # Develop an autonomous car racing agent

 To get started, follow the steps below to create the necessary environment and install the required dependencies.

 ## Environment Setup
 Create a new conda environment with Python 3.7 and activate it:
 
```python
conda create --name project_rl python=3.7
conda activate project_rl
```

## Dependencies Installation
Install the following dependencies in the given order:
```python
pip install swig
pip install opencv-python
pip install pandas
pip install Pillow
pip install stable-baselines
pip install tensorflow==1.15
cd Custom_Gym  && pip install -e ."[Box2D]"
pip install pyglet==1.3.2 # for Windows users, 1.5.11 for Mac users
pip install scikit-image
pip install wandb
pip install protobuf==3.20

```
Note: You may receive a dependency incompatibility warning between stable-baselines and our version of gym. This is normal and does not affect our project's scope.

To use Jupyter Notebook with the correct environment, follow these steps:

```python
conda activate project_rl
pip install ipykernel
python -m ipykernel install --user --name project_rl
```

## Get Started

After performing the above steps, you can launch the different notebook with the right kernels. These includes all the steps to train, evaluate and record videos for the different agents

### Pre-trained Model

Weights for the different agent trained on both the baseline and a more complex environment are available inside the Model Weight folder
Check the notebook to see how to load the pre-trained agent.

### Control the environment complexity and parameters

Complexity is set through 3 parameters: 
- num_tracks: 1 for basic track, 2 for more complex tracks with intersection (X, t type)
- num_lanes: number of lanes for the track 1 for normal, 2 for multiple lanes
- num_lanes_changes: number of time two lanes will be merged into 1 over the track

Obstacles/Bonus are controled by 2 parameters
- num_obstacles: number of obstacles by sub section of the track (if different than 0 then there are obstacles)
If the car touched an obstacle, 50 points are deducted from the score
- prop_good_obstacles: probability (set between 0-1) for an obstacles to be a bonus (yellow color instead of red + reward 50 points if touched)


Example of a baseline environment:
```python
env = lambda : CarRacing(
        grayscale=1,
        show_info_panel=0,
        discretize_actions="hard",
        frames_per_state=4,
        num_lanes=1,
        num_lanes_changes=1,
        num_tracks=1,
        allow_reverse=False,
        max_time_out=2,
        verbose=0,
        num_obstacles=0
        )
```
Example of a complex environment
```python
env = lambda : CarRacing(
        grayscale=1, ## 0 = RGB images, 1 = Grayscale images 
        show_info_panel=0, ## 0 to not show the score panel, 1 if you want
        discretize_actions="hard",
        frames_per_state=4, ## Number of frame to stack (if RGB images then it will be automatically reset to 1)
        num_lanes=1, ## number of lanes
        num_lanes_changes=1, ## number of time two lanes will be merged into 1 over the track
        num_tracks=2, ## Complexity of track, 1 for the original gym environment, 2 to include intersectionq
        max_time_out=2, ## how long the car is allowed to go out of track before termination
        verbose=0, ## Whether you want to output track generation message
        num_obstacles=5, ## Number of obstacles per sub-sections of the track
        prop_good_obstacles=0.5 ## 50% chance for an obstacle to be generated as a bonus
        )
```
 The above environment has both obstacles and bonuses (50% chance for an obstacle to be generated as a bonus) and includes intersections.


 ### Videos of the Pre-trained agent
 
 Videos for illustration of the trained agent are available inside the video sub-folder of the illustrations folder.

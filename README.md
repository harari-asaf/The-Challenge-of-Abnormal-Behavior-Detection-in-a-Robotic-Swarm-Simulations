# Here is the code for simulating drones swarm flights with anomalies using Microsoft AirSim Simulator.
This simulations been used in the "RS-CAD: Collaborative Anomaly Detection in Robotic Swarms" paper.
To recieve ready to use data please contect us via email. 

## Getting Started
First of all, make sure you have downloaded [Airsim](https://github.com/microsoft/AirSim), you got Unreal engine on your computer, and the [Blocks Enviroment](https://microsoft.github.io/AirSim/unreal_blocks/) is set up.

Open the Blocks enviroment. It should look like this:

![sc1](https://user-images.githubusercontent.com/60989064/107655204-029d0c00-6c8c-11eb-8929-e678b6461758.png)

It is recommended to remove all objects to avoid collisions.

The current Play Mode is Selected Viewport. Change it to Simulate:
Click expand toolbar -> Active Play Mode -> Simulate
It is recommended to change the Perspective field to Top (click Perspective -> top).

![guide](https://user-images.githubusercontent.com/60989064/108129041-4a6dca00-70b6-11eb-9ad3-0d7b8e399a6f.gif)

Now, the project can be run. Choose the Scenario you want to run. You can change its configuration file before running if it is desirable.
First, start playing the simulation by clicking: Click to expand toolbar -> Play. (If an error saying "There were no compatible vehicles created for current SimMode! Check your settings.json." pops, you can ignore it).
After doing so, run the main file of the scenario.

When the simulation ends, the generated data file should be located (if not configurated differently) in the data folder. 

## Project Organization

    ├── README.md          <- The top-level README for developers using this project.
    ├── AirSim
    |   └── settings.json          <- Simulation settings file
    |
    ├── DISC4BoTs
        |
        ├── avoidance          <- Avoidance scenario folder - drones are moving towards a goal 
        |                          while avoiding obstacles in their way          
        │   └── config.ini          <- Configuration file
        │   ├── avoidance.py          <- Avoidance scenario class, including the regular and malicious behaviour patterns
        │   └── avoidance_main.py          <- Avoidance main and monitor functions, used to run this scenario
        │
        ├── data             <- Where the recorded data of the scenario is saved
        │
        ├── followpath          <- Followpath scenario folder - drones are moving in a shared, random path
        │   └── config.ini          <- Configuration file
        │   ├── followpath.py          <- Followpath scenario class, including the regular and malicious behaviour patterns
        │   └── followpath_main.py          <- Followpath main and monitor functions, used to run this scenario
        |
        ├── PythonClient              <- Airsim's client folder. Necessarry for the project
        |
        ├── simple          <- Simple scenario folder - drones are moving towards a point
        │   └── config.ini          <- Configuration file
        │   ├── simple.py          <- Simple scenario class, including the regular and malicious behaviour patterns
        │   └── simple_main.py          <- Simple main and monitor functions, used to run this scenario
        |
        ├── survey         <- Survey scenario folder - drones are scanning an area.
        |                     Each drone got its own path
        │   └── config.ini          <- Configuration file
        │   ├── survey.py          <- Survey scenario class, including the regular and malicious behaviour patterns
        │   └── survey_main.py          <- Survey main and monitor functions, used to run this scenario
        |
        ├── data_testing.py         <- Script that tests and fixes the recorded data after it was generated by the scenario script
        ├── RepeatedTimer      <- Helper class used for generating the data
        └── scenario.py            <- Abstract class of a general scenario
 
 ## Explanation
 ### Scenario Types
 | Avoidance | Followpath | Simple | Survey |
| --- | --- | --- | --- |
| Drones are moving from one axis towards another parallel axis. In their way there are simulated obstacles, from which they are supposed to avoid. Initial positions, scenario time and route are random. | Following a random path. All five drones following a certain path - randomly going from one point to another. Initial positions and scenario time are predetermined. The route is random. | Moving in a certain structure from (0,0) to (0, 100) All five drones moving along the y axis together. Initial positions, scenario time and route are predetermined. | Surveying a rectangle. Each drone has its own random area to survey, therefore a different path. Initial positions, scenario time and route are random. |
 
 ### Anomaly Types
| Shift | Random | Path |
| --- | --- | --- |
| When shift anomaly type is activated, one of the drones will start moving towards a random very far away point, causing it to move on a straight line. | When random anomaly type is activated, one of the drones will start moving towards a point which is randomaly re-chosen few times a second. | When path anomaly type is activated, one of the drones will start moving on a random path, from one point to another. |

"none" anomaly type can be chosen. If so, no anomaly will be activated.
 
 ## Examples
 These are examples for run simulations for each of the different scenarios (x5 speed). The black lines represent a regular drones' route, while the red lines represent a malicious drone's route.
 
 ### Avoindance
 
Type | Shift | Random | Path |
| --- | --- | --- | --- |
| Avoidance | ![avoidanceshift](https://user-images.githubusercontent.com/60989064/108128510-85bbc900-70b5-11eb-8892-78a65151c725.gif) | ![avoidancerandom](https://user-images.githubusercontent.com/60989064/108127512-ffeb4e00-70b3-11eb-92cd-9122b756c99a.gif) | ![avoidancepath](https://user-images.githubusercontent.com/60989064/108126978-370d2f80-70b3-11eb-8356-0ee06a131edb.gif) |
Followpath | ![68747470733a2f2f696d372e657a6769662e636f6d2f746d702f657a6769662d372d6137393863366437346434612e676966](https://user-images.githubusercontent.com/60989064/107873858-45462a80-6ebe-11eb-997d-5921e0e879eb.gif) | ![68747470733a2f2f696d372e657a6769662e636f6d2f746d702f657a6769662d372d6435363232313137303430352e676966](https://user-images.githubusercontent.com/60989064/107874042-7115e000-6ebf-11eb-8829-74752bd4afa9.gif) |![68747470733a2f2f696d372e657a6769662e636f6d2f746d702f657a6769662d372d6166383862633033393837322e676966](https://user-images.githubusercontent.com/60989064/107874009-4af04000-6ebf-11eb-8c1b-1fc79f2a7254.gif) |
| Simple | ![68747470733a2f2f696d372e657a6769662e636f6d2f746d702f657a6769662d372d6265323133353365623134352e676966](https://user-images.githubusercontent.com/60989064/107874027-5e9ba680-6ebf-11eb-97d7-980a6b3019f3.gif) | ![68747470733a2f2f696d372e657a6769662e636f6d2f746d702f657a6769662d372d6563343130356431636133322e676966](https://user-images.githubusercontent.com/60989064/107874063-8db21800-6ebf-11eb-9d9e-ff3b7e92b90f.gif) | ![68747470733a2f2f696d372e657a6769662e636f6d2f746d702f657a6769662d372d3263376635666332636636332e676966](https://user-images.githubusercontent.com/60989064/107873814-fd270800-6ebd-11eb-8e41-4e3bd471b366.gif) |
| Survey | ![68747470733a2f2f696d372e657a6769662e636f6d2f746d702f657a6769662d372d6165653532373434643330632e676966](https://user-images.githubusercontent.com/60989064/107873860-47a88480-6ebe-11eb-9adf-ce994883a318.gif) | ![68747470733a2f2f696d372e657a6769662e636f6d2f746d702f657a6769662d372d6637653466343435313761662e676966](https://user-images.githubusercontent.com/60989064/107874073-a6bac900-6ebf-11eb-8e59-f4ad750acd60.gif) |  ![68747470733a2f2f696d372e657a6769662e636f6d2f746d702f657a6769662d372d6463666339306366306533662e676966](https://user-images.githubusercontent.com/60989064/107873952-d2897f00-6ebe-11eb-979c-e0f51f5a6f53.gif)
  |

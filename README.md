# Rulebook - Carla Simulator

In this project a rulebook is designed that determines the behavior of an autonomous agent. For this purpose goal states and trajectories are generated in the local planner. The behavior planner receives the trajectories and applies the predefined rules. The rulebook is tested using scenarios in the Carla Simulator.


<img src="https://i.imgur.com/eS0NaXS.gif"/>


# Scenario
A scenario describes the interaction of an autonomous agent with predefined obstacles. The course of this interaction is determined by the rulebook. All components for a scenario are defined in a JSON file. Scenarios are located in the scenarios folder.
```json
"scenario": {
		"id": 1,
		"description": "A straight line where no obstacles interact with the player."
	}
```
## Rulebook
A rulebook consists of a set of rules. These rules are stored in the rulebook according to their priority. The priority is determined by the index of the rule in the list. 

```json
{
	"rulebook_library": [
		{
			"rulebook": {
				"id": 0,
				"description": "",
				"rules": []
			}
		}
	]
}
```
## Rule
A rule describes a certain behavior. The function is passed all possible trajectories and applies the logic of the rule to them. The output then consists of the trajectories that have fulfilled the rule satisfactorily. 
```json
{
	"rules": [
		{
			"name": "lane_keeping",
			"description": "Only trajectories that are within the lane marking are selected.",
			"group": 1,
			"function": "function_trajectory_lane_keeping"
		}
	]
}
```
## Obstacles

Obstacles can be pedestrians or vehicles and can be placed freely in the world. Their direction of movement can be adjusted.

```json
"obstacle_walker": [
		{
			"transform": {
				"location": {
					"x": -7.53,
					"y": 135.21,
					"z": 1.37
				},
				"rotation": {
					"pitch": 0,
					"yaw": 270,
					"roll": 0
				}
			},
			"blueprint": "walker.pedestrian.0001",
			"walk_direction": {
				"x": 0,
				"y": 0,
				"z": 0
			},
			"speed": 0,
			"jump": false
		}
	]
```
```json
{
	"obstacle_vehicle": [
		{
			"transform": {
				"location": {
					"x": -4.8,
					"y": 147,
					"z": 1.37
				},
				"rotation": {
					"pitch": 0,
					"yaw": 270,
					"roll": 0
				}
			},
			"blueprint": "vehicle.tesla.model3",
			"autopilot": 1
		}
	]
}

```
# Usage
First start the Carla Server:
```
./CarlaUE4.exe Town02 -quality-level=Low
```
To execute a scenario the following command must be executed:
```
python main.py --scenario s_id --rulebook r_id
```
- s_id: number of the scenario
-  r_id number of the rulebook in scenario s_id

# Installation
The Carla version used here is:
```
[0.95](https://github.com/carla-simulator/carla/releases/tag/0.9.5)
```
The Python version to be used for this is:
```
3.7.x
```
To install all required packages:
```
\rulebook_carla

python -m pip install -r requirements.txt
```

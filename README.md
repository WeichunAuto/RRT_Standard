<div align="center">
  <h1>The Standard RRT Algorithm</h1>
</div>
</br>

### Programming Languages Used for This Project
<ul>
  <li>Python</li>
</ul>

### Libs Used under Python for This Project
<ul>
  <li>numpy</li>
  <li>matplotlib</li>
</ul>


## Introduction
The Rapid Exploration Random Tree (RRT) algorithm is a random sampling algorithm for state space, which avoids the large computational burden caused by precise modeling of space by detecting collisions at sampling points. It can effectively solve path-planning problems in high-dimensional spaces and complex constraints. This method is probability complete and non-optimal. It can easily handle obstacles and differential constraints and is widely used in the area of autonomous robot path planning.

In this project, I aimed to apply the standard RRT algorithm and the standard RRT algorithm with an adaptive lead point method to solve the obstacle avoidance problem for robots in given environments, simulate them and observe and compare the performance between them in different environments.

## The Process of Standard RRT
<ol>
  <li>Departure point as a seed, begins to grow branches;</li>
  <li>Randomly generate a lead point P in the search space;</li>
  <li>Find the closest point to P on the tree and mark it as C;</li>
  <li>Grow a step size in the direction of P if there are no obstacles to collision. If there is an obstacle to collision then repeat the process from steps 2-4;</li>
</ol>
<img width=80%; src="https://github.com/BobbyAuto/RRT_Standard/blob/main/images/Standard%20RRT%20Process.png"/>

## The Process of Standard RRT with an adaptive lead point
In the standard RRT algorithm, the lead point P was randomly generated, which enables the tree to explore the search space more. The strategy of this method is to set the lead point to the destination point with a 50% of possibility which enables the tree more targeted to grow towards the destination point. Therefore, theoretically, it has a higher performance of finding a feasible path to the destination.

```python
rand = random.random()
if rand < 0.5:
    x, y = self.destination
  else:
    x = np.random.uniform(self.searchSpace['min_right'], self.searchSpace['max_left'])
    y = np.random.uniform(self.searchSpace['max_down'], self.searchSpace['min_top'])
return (x, y)
```
## Definition of Key Parameters

<ul>
  <li><b>safeRadius</b>: </br>
    Because the robot has its size, we need to define a safe radius to represent the size. In this project, the value of safeRadius is 5.</li>
  <li><b>stepSize</b>: </br>In each iteration, the growth length of the tree. In this project, the value of stepSize is 1.5 times of the value of safeRadius.</li>
  <li><b>targetRadius</b>: </br>When a tree is growing and the distance between one node and the destination point is less than the value of targetRadius, we believe that the RRT tree has discovered a feasible path. In this project, the value of targetRadius is 5 times of the value of safeRadius.</li>
</ul>

## Definition of Environment-1
departure = (-380, -50) was represented by the blue dot on the below environment map</br>
destination = (400, 100) was represented by the red dot on the below environment map.</br></br>
Note that, the unit of the X-axis is meters.

<img width=80%; src="https://github.com/BobbyAuto/RRT_Standard/blob/main/images/Environment-1.png"/>

## Experiment-RRT Standard
<img width=80%; src="https://github.com/BobbyAuto/RRT_Standard/blob/main/images/Result_Standard.png"/>

## Experiment-RRT Standard with an adaptive lead point
<img width=80%; src="https://github.com/BobbyAuto/RRT_Standard/blob/main/images/Result_Adaptive.png"/> 

## Performance Comparision
In this section, with the same environment filled same obstacles which was shown in the previous section and parameters setting, we will run this algorithm 20 times respectively and compare their performance by measuring the time consumed in finding a feasible path. The result was shown below:

<img width=80%; src="https://github.com/BobbyAuto/RRT_Standard/blob/main/images/Performance%20Comparision.png"/> 

By observing the above diagram, we can see the method with an adaptive lead point is acting performance around average four times higher than the standard RRT algorithm.
#### One More Experiment in Another Environment
departure = (0, -25) was represented by the blue dot on the below environment map</br>
destination = (300, 105) was represented by the red dot on the below environment map.</br></br>

<img width=80%; src="https://github.com/BobbyAuto/RRT_Standard/blob/main/images/Environment-2.png"/>

In this type of environment, the generated tree and the feasible walking path will look like below:

<img width=80%; src="https://github.com/BobbyAuto/RRT_Standard/blob/main/images/Result_Standard-2.png"/>
<img width=80%; src="https://github.com/BobbyAuto/RRT_Standard/blob/main/images/Result_Adaptive-2.png"/>


With this environment and the same parameters set, we again will run this algorithm 20 times respectively and compare their performance by measuring the time consumed in finding a feasible path. The result was shown below:

<img width=80%; src="https://github.com/BobbyAuto/RRT_Standard/blob/main/images/Performance Comparision-2.png"/>

<b>Surprisingly, we obtained completely opposite results！！</b>

## Conclusion
The standard RRT algorithm with an adaptive lead point method is not always more effective than the standard RRT algorithm, it totally depends on the environment and the situation you are facing. Concluded from the experiments, normally when the obstacles are more discrete in an environment, The standard RRT algorithm with an adaptive lead point method is more effective than the Standard RRT algorithm.

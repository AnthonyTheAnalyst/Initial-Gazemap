# Initial-Gazemap

#####This is an early sample of a project that was later used to create a proprietary heatmap. #######

This code creates a simple gazemap overlay over a video using x, y and ms data points. 
The video output that this provides will have a white border which I subsequently used to add info about the GazeMap. 


The data that was used for this project was derived from getting eyetracking data from multiple data sources. 
All data sources were eventually converged into seperate csv files containing 3 columns (x-coordinates, y-coordinates, ms). 
The code is built off of those parameters. If your data is different you'll have change lines 51-128 as that is the section that pulled
from mulitple csv files to converge all the data to feed the program.
   
   
 The actual plotting of points and aligning them to a video starts on line 132 of this code. 
 
 
 I hope this helps someone!

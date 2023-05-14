# Proposal for Semester Project
 
**Patterns & Trends in Environmental Data / Computational Movement
Analysis Geo 880**
 
| Semester:      | FS23                                                             |
|:---------------|:---------------------------------------------------------------- |
| **Data:**      | Pooled POSMO tracking data                                       |
| **Title:**     | Improved Transport Mode Detection & Public Transport Punctuality |
| **Student 1:** | Lukas Bieri (bieriluk)                                           |
| **Student 2:** | Valentin Hett (hettval1)                                         |
 
## Abstract 
<!-- (50-60 words) --> 
In this semester project we will evaluate if Transport Mode Detection of GPS-tracking data can be improved using the stepwise procedure described in (Sadeghian et al., 2022) implemented in R and using publicly available public transport timetables. We will figure out, if this newly classified data can be used to assess punctuality of public transport for this sample.
 
## Research Questions  <!--(50-60 words)-->
1. Can Transport Mode Detection (TMD) for the pooled POSMO tracking data be improved using (a) the stepwise procedure described in (Sadeghian et al., 2022) and with (b) public transport timetables?
2. Is it possible to accurately assess the punctuality of public transport using the data provided by POSMO?
 
## Results / products
<!-- What do you expect, anticipate? -->
The data analysis in R will result in a reclassified data set with transport mode information as well as an assessment of the accuracy of this method of classification. 
If the GPS-data is precise and accurate enough and we can set appropriate thresholds for the algorithms, we expect a materially better TMD then the one provided by POSMO. If that is the case, it should also be possible to use the data to assess punctuality for public transport for this sample based on the tracking data.
 
## Data
<!-- What data will you use? Will you require additional context data? Where do you get this data from? Do you already have all the data? -->
The tracking data is provided voluntarily and anonymised by students in this module. They tracked their movement using the POSMO-App. The data contains tracking data for several month from throughout Switzerland. The data is entity-based point data in a continuous movement space with time stamps in three dimensions (coordinates and time).  
To help with TMD, we will also be using publicly available data on stations, routes and timetables for public transport. These are provided by the Swiss public transportation companies in Open-Data-Platforms such as opentransportdata.swiss and data.stadt-zuerich.ch.
 
## Analytical concepts
<!-- Which analytical concepts will you use? What conceptual movement spaces and respective modelling approaches of trajectories will you be using? What additional spatial analysis methods will you be using? -->
As we are looking at all the collected movement data, we operate in an unconstrained movement space, however we make use of constrained movement spaces for detecting the mode of transport, since passive forms of movement like trains and busses are restricted to their respective routes and cars (usually) to roads.  
In order to verify the method, the system boundaries are initially set as the ZVV public transportation network. The system boundaries can be extended or even further limited, depending on the outcomes of the analysis.
 
**Improved Transport Mode Detection**
 
*1. Noise reduction*
The tracking data from the pool of POSMO app data is combined, cleaned, outliers are removed, and the data is resampled using linear interpolation to have a consistent time lag between points. The parameters for these steps are derived from repeated Explorative Data Analysis (EDA) by visualization and descriptive statistics. 
 
*2. Segmentation*
The trajectories are cut into segments using the method as described in (Laube & Purves, 2011). This is done by detecting static fixes using a temporal moving window (v) to calculate the mean Euclidian distance between the points and comparing this to a threshold (d) for non-movement. Short segments are removed.
 
*3. Features extraction*
Features are calculated as the basis for the TMD such as: speed, acceleration, step length and time lag (s. segmentation). The bearing is also calculated. These features are then summarised for each segment (mean, max, min, change rate, etc.).
 
*4. Unsupervised algorithm*
The K-means clustering algorithm is used to preliminarily label segments using the above-mentioned descriptive statistics and appropriate thresholds for the different mode patterns. Those clearly identified to belong to one transport mode are labelled, saved and removed. This reduces the size of the data set for further processing.
 
*5. Spatial Multi-Criteria Analysis* 
The data is then further classified using multiple criteria analysis including a comparison with public transport schedule data provided by the Swiss Federal Railways SBB. Clearly categorized segments with only one classification are again labelled, saved and removed.
 
*6. Supervised learning algorithms* 
The remaining data set is then labelled using the Random Forest (RF) supervised learning algorithm.
 
*7. Evaluation of improvement in transport mode detection*
The resulting data set with all labelled segments is then compared to ground truth data for one person in the sample to determine the accuracy of the assigned labels. This is also compared to the assigned labels by POSMO.
 
**Punctuality Evaluation of public transport**
 
*8. Assigning stations and calculation times*
Each public transportation segment is assigned a departure and arrival station as well as a calculated actual departure time and arrival time. 
 
*9. Join tracking segment with bus/train/tram*
Based on a predefined temporal window, each segment is assigned a connection with a mode of public transport including schedule arrival and departure time. This can then be compared to determine punctuality as defined by the Swiss federal railway. The accuracy of this analysis is again assessed using one ground truth data set.
 
## R concepts
<!-- Which R concepts, functions, packages will you mainly use. What additional spatial analysis methods will you be using? -->
All analysis will be done in R, using R-Studio.  
 
In addition to basic pre-processing, analysis, and visualization tools such as ggplot2, dplyr, tidyr and readr, we will use the following tools:  
1.	Moving window functions from the “zoo” package
2.	The data analysis tools in the “data.table” package
3.	Spatial analysis tools in the “sf” and “terra”package
4.	The map visualization tools in the “tmap” package
5.	The R-Tool for k-means clustering in the “kmeans” package
6.	The classification and regression algorisms in the “randomForest” package
 
## Risk analysis
<!-- What could be the biggest challenges/problems you might face? What is your plan B? -->
The biggest challenges for the project will be the time constraint to implement the analysis in R and carefully evaluate the results.  
Another risk is, that for many thresholds used in segmentation and TMD it is difficult and time consuming to find the perfect value that fits the whole sample the best to allow for realistic results. If the chosen thresholds are inadequate, this will significantly impact the results.  
With the evaluation of punctuality, it is also possible, that the data even with improved TMD is not precise and accurate enough to reliably evaluate punctuality.  
POSMO is a relatively new application for tracking the movement of people. The tracking is carried out with GPS, which is known for the variable precision. It may lead to wrong conclusion and the differentiation of public transport methods could be difficult to define.
 
## Questions? 
<!-- Which questions would you like to discuss at the coaching session? -->
1.	Given our data, is it more sensible to go with our methodological version for the second research question, rather than actually evaluating punctuality of public transport?  
2.	In your experience, is the task we give ourselves with these two research questions possible given time constraints and limited experience with these clustering tools.  
3.	What would be a useful tool in R to each measure the distance of a point (GPS-fix) to a railway network (vector, line)  
 
## Literature
Laube, P., & Purves, R. S. (2011). How fast is a cow? Cross-Scale Analysis of Movement Data. Transactions in GIS, 15(3), 401–418. https://doi.org/10.1111/j.1467-9671.2011.01256.x

Sadeghian, P., Zhao, X., Golshan, A., & Håkansson, J. (2022). A stepwise methodology for transport mode detection in GPS tracking data. Travel Behaviour and Society, 26, 159–167. https://doi.org/10.1016/j.tbs.2021.10.004

# Proposal for Semester Project

**Patterns & Trends in Environmental Data / Computational Movement
Analysis Geo 880**

| Semester:      | FS23                                     |
|:---------------|:---------------------------------------- |
| **Data:**      | Pooled POSMO tracking data               |
| **Title:**     | Transport Mode Detection & Weather       |
| **Student 1:** | Lukas Bieri (bieriluk)                   |
| **Student 2:** | Valentin Hett (hettval1)                 |

## Abstract 
<!-- (50-60 words) -->


## Research Questions  <!--(50-60 words)-->
1. Can Transport Mode Detection for the pooled POSMO tracking data be improved using (a) the stepwise procedure described in Sadeghian et al (2022) and with (b) public transport timetables?
2. Is it possible to accurately assess the punctuality of public transport using the data provided by POSMO?

## Results / products
<!-- What do you expect, anticipate? -->
Posmo is a relativly new application for tracking the movement of people. The tracking is carried out with GPS, which is known for the variable precision. It may lead to wrong conclusion and the differentiation of public transport methods could be difficult to define. In order to allow the time to capture the reliability and the correct punctuality, the maximum deviation must be defined. If the GPS data isn't varying to much, it should be possible to reconstruct the pathways of the individual type of movement.   


## Data
<!-- What data will you use? Will you require additional context data? Where do you get this data from? Do you already have all the data? -->
The data is provided by different students, which tracked their movement by POSMO. They have been pooled and anonymized so that an evaluation of the data cannot be influenced by individual students. The data will most likely originate throughout Switzerland. In order to verify the method, the system boundaries are initially set in the ZVV transport infrastructure in Wädenswil. With further evaluations, the system boundaries can be extended or even further limited. For this purpose, the departure and arrival times of public transport are also required. These are provided by the public transport companies. The times will differ from the performed times, therefore it should be possible to render the data comparable.

## Analytical concepts
<!-- Which analytical concepts will you use? What conceptual movement spaces and respective modelling approaches of trajectories will you be using? What additional spatial analysis methods will you be using? -->
As we are looking at all the collected movement data, we operate in an unconstrained movement space, however we make use of constrained movement spaces for detecting the mode of transport, since trains and busses are restricted to their respective routes. 
**Improved Transport Mode Detection**

*1. Noise reduction*  
The tracking data from the pool of POSMO app data is combined, cleaned, outliers are removed, and the data is resampled using linear interpolation to have a consistent time lag between points. The parameters for these steps are derived from repeated Explorative Data Analysis (EDA) by visualization and descriptive statistics.   
*2. Segmentation*  
The trajectories are cut into segments using the method as described in (Laube & Purves, 2011). This is done by detecting static fixes using a temporal moving window (v) to calculate the mean Euclidian distance between the points and comparing this to a threshold (d) for non-movement. Short segments are removed.  
*3. Features extraction*  
As the basis for the Transport Mode Detection features are calculated from the data such as: speed, acceleration, step length and time lag (s. Segmentation). The bearing is also calculated. These features are then summarised for each segment (mean, max, min, change rate).  
*4. Unsupervised algorithm*  
The K-means clustering algorithm is used to preliminarily label segments using the above-mentioned descriptive statistics and thresholds for the different mode patterns. The clearly identified to belong to one transport mode are labelled, saved, and removed. This reduces the size of the data set for further processing.  
*5. Spatial Multi-Criteria Analysis*   
The data is then further classified using multiple criteria including a comparison with public transport schedule data provided by the Swiss Federal Railways SBB.  
*6. Supervised learning algorithms*   
The remaining data set is then further labelled using the Random Forest (RF) supervised learning algorithm.  
*7. Evaluation of improvement in transport mode detection*  
The resulting data set with all labelled segments is the compared to ground truth data for one person in the sample to determine the accuracy of the assigned labels. This is also compared to the assigned labels by POSMO.

**Punctuality Evaluation of public transport**
*8. Assigning stations and calculation times*  
Each segment of public transportation is assigned a departure and arrival station as well as a calculated actual departure time and arrival time.  
*9. *

## R concepts
<!-- Which R concepts, functions, packages will you mainly use. What additional spatial analysis methods will you be using? -->
All analysis will be done in R, using R-Studio. 
In addition to basic pre-processing, analysis and visualization tools such as ggplot2, dplyr, tidyr and readr, we will use the following tools:
1.	Moving window functions from the “zoo” package will be used for resampling and feature extraction.

*2. Segmentation*

*3. Features extraction*
*4. Unsupervised algorithm*
*5. Spatial Multi-Criteria Decision Analysis (sMCDA)*
*6. Supervised learning algorithms* 

**Punctuality Evaluation of public transport**

## Risk analysis
<!-- What could be the biggest challenges/problems you might face? What is your plan B? -->
The biggest challenges for the project will be the time constraint to implement the analysis in R and carefully evaluate the results. 
Another risk is, that for many thresholds used in segmentation and Transport Mode Detection it is difficult and time consuming to find the perfect value that fits the whole sample the best to allow for realistic results. If the chosen thresholds are inadequate, this will significantly impact the results.
With the evaluation of punctuality, it is also possible, that the data even with improved Transport Mode detection is not precise and accurate enough to reliably evaluate punctuality.

## Questions? 
<!-- Which questions would you like to discuss at the coaching session? -->
1.	Given our data, is it more sensible to go with our methodological version for the second research question, rather than actually evaluating punctuality of public transport?
2.	What would be a useful tool in R to each measure the distance of a point (GPS-fix) to a railway network (vector, line)


## Literature

Sadeghian, P., Zhao, X., Golshan, A., & Håkansson, J. (2022). A stepwise methodology for transport mode detection in GPS tracking data. Travel Behaviour and Society, 26, 159–167. https://doi.org/10.1016/j.tbs.2021.10.004

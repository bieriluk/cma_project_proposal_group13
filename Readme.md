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
Posmo is a relativly new application for tracking the movement of people. The tracking is carried out with GPS, which is known for the variable precision. It may lead to wrong conclusion and the differentiation of public transport methods could be difficult to define. In order to allow the time to capture the reliability and the correct punctuality, the maximum deviation must be defined. 


## Data
<!-- What data will you use? Will you require additional context data? Where do you get this data from? Do you already have all the data? -->

## Analytical concepts
<!-- Which analytical concepts will you use? What conceptual movement spaces and respective modelling approaches of trajectories will you be using? What additional spatial analysis methods will you be using? -->

**Improved Transport Mode Detection**

*1. Noise reduction*
The tracking data from the pool of POSMO app data is combined, cleaned, outliers are removed and the data is resampled to have a consistent timelag between points. The parameters for these steps are derived from repeated Explorative Data Analysis by Visialization and descriptive statistics. 
*2. Segmentation*
*3. Features extraction*
*4. Unsupervised algorithm*
*5. spatial Multi-Criteria Decision Analysis (sMCDA)*
*6. Supervised learning algorithms* 

**Punctuality Evaluation of public transport**
*7. *

## R concepts
<!-- Which R concepts, functions, packages will you mainly use. What additional spatial analysis methods will you be using? -->

## Risk analysis
<!-- What could be the biggest challenges/problems you might face? What is your plan B? -->

## Questions? 
<!-- Which questions would you like to discuss at the coaching session? -->

## Literature

Sadeghian, P., Zhao, X., Golshan, A., & Håkansson, J. (2022). A stepwise methodology for transport mode detection in GPS tracking data. Travel Behaviour and Society, 26, 159–167. https://doi.org/10.1016/j.tbs.2021.10.004

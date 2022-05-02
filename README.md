# STAT 450 Project
## The Effects of Climate Variables on Average Stream Flow for Canadian Watersheds

***Contributors***: *Anjali Chauhan, Kelvin Li, Kohl Peterson, Vanessa Bayubaskoro*

### 1. Summary

This study aims to develop a model that predicts the annual average streamflow for Canadian watersheds
based on climate variables data. Streamflow predictions provide crucial information for water resource
management and help reduce the financial loss due to floods, droughts and dam mismanagement. Climate
variables such as precipitation, evaporation, temperature, potential evaporation, snow density and snow fall
are all important factors in predicting streamflow values based on Boruta and Forward Stepwise Regression
variable importance techniques. We find that these important climate variables have linear relationships with
the streamflow values.Our best performing model is an ensemble model with interaction terms with Root
Mean Square Error (RMSE) of 0.1878. This model stacks prediction models such as Linear Regression and
XGBoost and puts more weight on well performing models. These techniques can be applied in predicting
average annual streamflow across different watersheds throughout the planet without the spatial and temporal
input. Looking at streamflow values per location, we find that there are two watersheds with 3 extreme high
points.

### 2. Introduction

A watershed refers to an area of land that channels rainfall and snowmelt to a common outlet of rivers,lakes
and other bodies of water. Understanding watershed stream flow is important for water resource management
including irrigation, hydroelectric power and flood control. The study investigates the effect of climate
variables on the watershed’s streamflow.

The statistical analysis addresses the following questions:

- Can the data from one catchment be used to extrapolate stream flow in another catchment, given the
climate variables?
- Can we accurately detect unusual streamflow activities that result in severe adverse effects on the
nearby ecosystem and populated areas?

To answer the above questions, we will:
- Build an outlier detection system to detect the unusual streamflow activity (extreme values)
- Develop effective visualization to analyze the relation between average annual streamflow and the
climate variables
- Identify important climate variable(s) and determine the effect of said variable(s) on the streamflow
- Develop models to accurately predict the average streamflow

This report summarises the primary statistical modelling and analysis results. The body of the report is
organized as follows: Section 2 describes the data collection, provides measurements of the variables and
summarises the data. Section 3 presents the data preprocessing and statistical modelling techniques used
to answer the client’s research questions. Section 4 summarises and interprets the results of the statistical
analysis conducted. Section 5 describes the outlier detection performed on the predicted streamflow values.
Section 6 briefs the limitations and challenges of the analysis. Lastly, appendices are provided for further
exploratory data analysis and the code used for the statistical modeling.

### 3. Data

This section includes brief description of the given data variables and visualizations of the relationships
between each climate variables and streamflow.

#### 3.1. Description

There are observations from 23 medium-sized water catchment areas located around Canada. The data was
collected daily by satellites, and an aggregation of the data (annual averages) was provided for this analysis.
Table 1 provides a data dictionary and Table 2 has a list of summary statistics. The size of these watersheds
ranges from 50 km^2 to 10,000 km^2. The data of various climate variables was taken from the year 1980 to
2018. An additional dataset with the watershed location data (Longitude, Latitude) is also available by the
client for further analysis of the effect of spatial features on the streamflow.

#### 3.2. Exploratory Data Analysis

Fig. 1 shows that the relationships between each climate variables and streamflow are linear. All of the snow
related climate variables and precipitation have a positively correlated linear relationship with streamflow.
Evaporation and potential evaporation have a negatively correlated linear relationship with streamflow. Fig.
2 shows the distribution of the climate variables before scaling. Scaling climate variables is needed to avoid
issues during modelling.

There are a lot of evidence that suggests difficulty in extrapolating the results of one gridcode to another. By
analyzing our data at gridcode level, Fig. 3 shows that the number of observations varies per gridcode. There
are multiple watershed locations with 39 observations but there is also a watershed with only 20 observations.
Fig. 4 displays the various distribution of streamflow per gridcode. Streamflow differs significantly from
gridcode to gridcode.

A close look at various variables broken out by gridcode (see Fig. 5 as an example) finds some interesting
results. For many gridcode’s, there appears to be a much stronger linear relationship between climate
variables and the stream flow and these relationships appear to have different intercept and slope values.
This suggests that there may not be a one-size-fits-all approach to fitting a regression model based on annual
climate variables alone, and different slopes for different gridcode’s may need to be considered for further
analysis in the future.

### 4. Methods
[Please refer to: https://github.com/anjali-chauhan/Predicting-Stream-Flow/blob/main/Report-%20Stream%20Flow%20Prediction.pdf]

### 5. Model Results
[Please refer to: https://github.com/anjali-chauhan/Predicting-Stream-Flow/blob/main/Report-%20Stream%20Flow%20Prediction.pdf]

### 6. Outlier Detection
[Please refer to: https://github.com/anjali-chauhan/Predicting-Stream-Flow/blob/main/Report-%20Stream%20Flow%20Prediction.pdf]

### 7. Limitations

In this section, we discuss about our limitations of ouur study.

- After feature selection, there is some potential that the best features for each model type were not
selected. When selecting the features that would be included in the hyper-parameter tuning for the
models we used the results of both Boruta (random forest based selection method) and Forward
Stepwise Regression (regression based selection method). The selected features from each both agreed
with each other so they seemed to be reliable; however, we did not do an exhaustive search over all
variables for each of the models and there might be better combinations.
- Gridcode being selected as an important feature may lead to poor model performance due to lack of
data, especially when considering interactions. There are 23 separate gridcodes, so there are only 20-40
observations for each gridcode which is not very much (especially for tree based models). Having access
to more data could result in much higher performance.
- Each observation in the dataset is an aggregation of climate data collected over the year, i.e., they are
the average values collected over the year. This limits the forecasting power of the predictive models
that we have fit as we would need to use the forecasted explanatory variables to predict the stream
flow, which would most likely lower the performance of the model.

### 8. Conclusion

In this work, we wanted to visualize the relationships between each climate variables and streamflow, find
important climate variables in predicting the annual average streamflow, predict streamflow, and find outliers.
In order to achieve this, we created scatterplots to see that there are linear relationships between each climate
variables and streamflow, got rid of highly correlated climate variables and performed feature selection to
find the important climate variables. We have fitted multiple models to our training data and found that
an Ensemble model with interaction terms performed the best based on our cross validation set. We also
looked at the distribution of streamflow per gridcode to obtain outliers.

After all the model iterations and improvements, we have been able to achieve fairly good results with
the Ensemble Model taking into account the interaction effect between variables. These results have large implications when it comes to water resource management economically. We have conducted our primary analysis taking into account the spatial data (e.g. gridcodes) which serves as a good MVP to predict the streamflow.

As a side interest and to expand upon the idea of predicting the streamflow solely using climate variables
and not any spatial and temporal data, we conducted an analysis and trained models without this data and
the predictive performance dropped significantly. Although this addresses the client’s first research question
of whether one catchment can be used to extrapolate stream flow in another catchment, the limitation we
faced was lack of training data. To be able to model such a complex problem using climatic variables, we
need more data to train our model which can help improve the predictive performance of the model.

To address the second research question of whether or not we can detect the unusual streamflow activity
accurately, we built a proof of concept pipeline for the outlier detection system. It will take the features
from our prediction model as input and label the observations as either anomalous or regular depending
on the anomaly scores which are the measures of deviation from normal behavior. We will face the same
challenge here - lack of training data. This will lead to an increase in false positives and false negatives in the
outlier detection system which can have detrimental consequences. For example, not being able to detect a
subtle increase in the streamflow (false negatives) which could lead to irrigation problems and even floods,
or getting a huge pool of outlier values (false positives) that raises false alarms of anomalous behavior more
often than desired.

### 9. Future Research

Future research in two areas would help address the limitations in this study: further investigating outliers
and anomaly detection and training a model on a more granular time frame.

- The outlier detection that we have done is appropriate for identifying outliers in the current dataset
but does not have a real-world application. Training a classification model to predict extreme values
in streamflow and/or training an anomaly detection model to find unusual patterns in streamflow and
the climate variables. Both models could have more real-world application in flood/drought prevention
which is useful in fields such as agriculture.
- Additionally, including input data for the whole year for the model makes it impractical to accurately
predict streamflow values in the future as we would need to use forecasted values for the input variables.
Having the data in a more granular time frame would greatly benefit the analysis and real-world
predictive power of the model as we could train the predictive streamflow model only using past
variables. The resulting model would not rely on using forecasted input variables, which addresses a
critical limitation of this study

### 10. References

- Government of Canada / Gouvernement du Canada. (2021, November 25). Government of Canada /
gouvernement du Canada. Climate. Retrieved February 5, 2022, from https://climate.weather.gc.ca/
glossary_e.html
- US Department of Commerce, N. O. A. A. (2012, March 8). Snow measurement guidelines. Snow
Measurement Guidelines. Retrieved February 5, 2022, from https://www.weather.gov/gsp/snow
- Janssen, J., & Ameli, A. A. (2021). A Hydrologic Functional Approach for Improving Large‐Sample
Hydrology Performance in Poorly Gauged Regions. Water Resources Research, 57(9), e2021WR030263.
- Statistical interaction: More than the sum of its parts. Statistics Solutions. (2021, June 22). Retrieved
February 21, 2022, from https://www.statisticssolutions.com/statistical-interaction-more-than- thesum-of-its-parts/


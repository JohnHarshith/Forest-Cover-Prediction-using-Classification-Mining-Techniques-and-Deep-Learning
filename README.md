<h1 align="center"> Forest Cover Prediction using Classification Mining Techniques and Deep Learning </h1>

<p align="center">
  <a href="https://github.com/arjundas1/Forest-Cover-Prediction-using-Classification-Mining-Techniques-and-Deep-Learning">
    <img src="https://user-images.githubusercontent.com/83835729/132753758-d3334562-56e8-46b8-87ce-6dcc64ad65e8.png" width="350" height="250">
  </a>
</p>

<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#introduction">Introduction</a></li>
    <li><a href="#project-team">Project Team</a></li>
    <li><a href="#project-objective">Project Objective</a></li>
    <li><a href="#tools-used">Tools Used</a></li>
    <li><a href="#methodology">Methodology</a></li>
    <li><a href="#implementation">Implementation</a></li>
    <li><a href="#inference">Inference</a></li>
    <li><a href="#conclusion">Conclusion</a></li>
    <li><a href="#references">References</a></li>
    <!---
    <li><a href="#contact-us">Contact Us</a></li>
    --->
  </ol>
</details>

## Introduction

In recent years, there have been great advancements in the field of Machine Learning and Artificial Intelligence, where automation of lengthy, tedious, and manually implemented algorithms have been replaced with powerful and dynamic language libraries, that have logic programmed already with easy language syntax, thereby making implementations faster. Data Mining techniques have also seen notable improvements lately that enable people to get deeper understanding of various kinds of datasets, and hence infer better targeted prediction, bringing out several unknown or unobserved interpretations of the data.

Complex datasets that have considerably huge size and mediocre usability ratings might indicate towards a possible tendency of mediocrity in the prediction accuracies for the model created based on these datasets. However, it need not be a hard and fast rule and such generalised notions can be claimed incorrect with the use of latest advanced computing tools. The project deals with a dataset of a similar description and finds a variety of methods to create suitable prediction models using Classification Mining Techniques and Deep Learing concepts to yield a higher prediction accuracy than the base paper without overfitting the model for higher accuracy. 

## Project Team

Guidance Professor: Dr. Arup Ghosh, School of Computer Science and Engineering, VIT Vellore.

The group for our Data Mining project consists of -

|Sl.No. | Name  | ID Number |
|-| ------------- |:-------------:|
|1|     Arjun Das      | 20BDS0129     |
|2| Siddharth Pal      | 20BDS0409     |
|3| John Harshith      | 20BDS0411     |


## Project Objective

In 1999, Jock A. Blackard and Denis J. Dean implemented Artificial Neural Network and Discriminant Analysis to predict the forest cover from various areas of the Roosevelt National Forest in Colorado, USA.

However, we know from his paper that there is only 71.1% prediction accuracy in the model created by them using Artificial Neural Networks on various columns of data. Even though this method was better than previously implemented traditional Discriminant Analysis, our objective in this project is to find solutions to better the accuracy using the exact same dataset by creating various classification models.

This dataset includes information on tree type, shadow coverage, wilderness of the surrounding, distance to nearby landmarks (roads etc), soil type, local topography, etc. The dataset is very large having more than 0.5 million item sets. Its usability is 5.9 according to premiere data science websites.

The above dataset has been taken from the University of California Irvine Machine Learning Repository, and the source can be found [here](https://archive.ics.uci.edu/ml/datasets/Covertype), and the dataset is also present in the main branch of the repository as [covtype.csv](https://github.com/arjundas1/Forest-Cover-Prediction-using-Classification-Mining-Techniques-and-Deep-Learning/blob/main/covtype.csv). Finally the accuracy and overall prediction performance of the model is gauged for efficient use.

## Tools Used

To achieve the project objective we make use of the following tools -
* **Classification Mining Techniques**
  * Logistic Regression
  * Gaussian Naive Bayes'
  * K-Nearest Neighbors
  * Support-Vector Machine
  * Random Forest Classification

* **Python Language Libraries**
  * Seaborn
  * Matplotlib
  * Scikit-learn
  * Pandas
  * Keras
  * Tensorflow
 
* **R Language Libraries** 
  * Tidyverse
  * Skimr

## Methodology

1. Understanding the components of the dataset.
2. Creating visuals that will aid us with the understanding and enable us to find the proper combination of data columns for high accuracy.
3. Using various classification mining algorithms to create models that yield certain prediction accuracy for certain combination of data columns.
4. Fitting models appropriately and checking if any model has been overfitted or underfitted.
5. Iterating certain column combinations and algorithms for a large number of times to find the best train-test split and record that prediction percentage as well as the split content in a separate binary file for future use.
6. Using Deep Learning technique on the dataset and yield prediction accuracy.
7. Comaparing the performance of all the algorithms and concluding with the most recommended algorithm with this dataset.

## Implementation
<!---
A segment of the visualisation has used the R language and its libraries to help us understand the dataset better. The rest of the visualisation, classification and DL analysis has been implemented with the help of Python libraries.

### Understanding the Data

The 13 variables included in the dataset are:

- Cover_Type: One of seven types of tree cover found in the forest. In the data downloaded for the project, the observations are coded 1 through 7. We have renamed them for clarity. Observations are based on the primary cover type of 30m x 30m areas, as determined by the United States Forest Service. This is our response variable.
- Wilderness_Area: Of the six wilderness areas in the Roosevelt National Forest, four were used in this dataset. In the original dataset, these were one-hot encoded. We put them in long form for better visualisation and because most machine learning methods will automatically one-hot encode categorical variables for us.
- Soil_Type: 40 soil types were identified in the dataset and more detailed information regarding the types can be found at https://www.kaggle.com/uciml/forest-cover-type-dataset. Similar to Wilderness_Area, Soil_Type was originally one-hot encoded.
- Elevation: The elevation of the observation in meters above sea level.
- Aspect: The aspect of the observation in degrees azimuth.
- Slope: The slope at which the observation is observed in degrees.
- Hillshade_9am: The amount of hillshade for the observation at 09:00 on the summer solstice. This is a value between 0 and 225.
- Hillshade_Noon: The amount of hillshade for the observation at 12:00 on the summer solstice. This is a value between 0 and 225.
- Hillshade_3pm: The amount of hillshade for the observation at 15:00 on the summer solstice. This is a value between 0 and 225.
- Vertical_Distance_To_Hydrology: Vertical distance to nearest water source in meters. Negative numbers indicate distance below a water source.
- Horizontal_Distance_To_Hydrology: Horizontal distance to nearest water source in meters.
- Horizontal_Distance_To_Roadways: Horizontal distance to nearest roadway in meters.
- Horizontal_Distance_To_Fire_Points: Horizontal distance to nearest wildfire ignition point in meters.

```R
library(tidyverse)
library(skimr)

df <- read.csv("Forest Cover.csv")
```
```R
glimpse(df)
nrow(df) - nrow(distinct(df))
any(is.na(df))
skim(df)
```

### Visualising the data



#### Soil Type

The base paper included a vivid description 

```R
set.seed(1808)

dff <- (df %>%
         group_by(Cover_Type) %>%
         sample_n(size = 1000) %>%
         ungroup() %>%
         gather(Wilderness_Area, Wilderness_Value, 
                Wilderness_Area1:Wilderness_Area4) %>% 
         filter(Wilderness_Value >= 1) %>%
         select(-Wilderness_Value) %>%
         mutate(Wilderness_Area = str_extract(Wilderness_Area, '\\d+'),
                Wilderness_Area = str_replace_all(Wilderness_Area,
                                                  c(`1` = 'Rawah',
                                                    `2` = 'Neota',
                                                    `3` = 'Comanche Peak',
                                                    `4` = 'Cache la Poudre')),
                Wilderness_Area = as.factor(Wilderness_Area)) %>%
         gather(Soil_Type, Soil_Value, Soil_Type1:Soil_Type40) %>%
         filter(Soil_Value == 1) %>%
         select(-Soil_Value) %>% 
         mutate(Soil_Type = as.factor(str_extract(Soil_Type, '\\d+'))) %>%
         mutate(Cover_Type = str_replace_all(Cover_Type,
                                             c(`1` = 'Spruce/Fir',
                                               `2` = 'Lodgepole Pine',
                                               `3` = 'Ponderosa Pine',
                                               `4` = 'Cottonwood/Willow',
                                               `5` = 'Aspen',
                                               `6` = 'Douglas Fir',
                                               `7` = 'Krummholz')),
                Cover_Type = as.factor(Cover_Type)) %>%
         select(Cover_Type:Soil_Type, Elevation:Slope,
                Hillshade_9am:Hillshade_3pm, Vertical_Distance_To_Hydrology,
                Horizontal_Distance_To_Hydrology:Horizontal_Distance_To_Fire_Points))

glimpse(dff)
skim(dff)

palette <- c('sienna1', 'chartreuse', 'lightskyblue1', 
             'hotpink', 'mediumturquoise', 'indianred1', 'gold')
ggplot(dff, aes(x = Cover_Type, y = Elevation)) +
  geom_violin(aes(fill = Cover_Type)) + 
  geom_point(alpha = 0.01, size = 0.5) +
  stat_summary(fun = 'median', geom = 'point') +
  labs(x = 'Forest Cover') +
  scale_fill_manual(values = palette) +
  theme_minimal() +
  theme(legend.position = 'none',
        axis.text.x = element_text(angle = 45,
                                   hjust = 1),
        panel.grid.major.x = element_blank())
```

<p align="center">
  <a href="https://github.com/arjundas1/Forest-Cover-Prediction-using-Classification-Mining-Techniques-and-Deep-Learning">
    <img src="https://github.com/arjundas1/Forest-Cover-Prediction-using-Classification-Mining-Techniques-and-Deep-Learning/blob/main/Visualization/Cover%20based%20on%20soil.png" width="650" height="500">
  </a>
</p>

--->

### Classification Algorithm Determination

There exists various classification mining algorithms that can be used and implemented to form a model that yields very high prediction accuracy. A comparison of various feature selection with various supervised classification learning algorithms have been used and recorded. This tells us about the range of prediction percent one can get while using a particular algorithm (with or without ensemble) for a particular combination of features or data labels.

#### Gaussian Naive Bayes'



#### Logistic Regression



#### Support Vector Machines



#### K-Nearest Neighbors



#### Random Forest

A bagging ensemble technique for the Decision Tree Algorithm, Random Forest generates a constant prediction accuracy at a particular n (number of estimators that gets created) for a the column combinations. Therefore, there is no need to store the highest recorded accuracy and its corresponding test-train split in a pickle file. Random forest has also been one of the computationally cheapest techniques and resulted in one of the highest recorded prediction accuracies for many of the column combinations.

More information on the algorithm used:
- Number of estimators - 100
- Node splitting criteria taken - Gini index
- No explicit mention of the depth of the tree that is formed
- For best split, square root of the features was done instead of taking logarithm
- No random state included and no verbosity required

```python
x_train, x_test, y_train, y_test = train_test_split(x, y, test_size=0.2)
rf = RandomForestClassifier(n_estimators=100)
rf.fit(x_train, y_train)
pred = rf.predict(x_test)
print("Accuracy using Random Forest: ", round(rf.score(x_test,y_test) * 100, 3), "%", sep="")
```

## Inference



## Conclusion



## References

- [_Blackard, J. A., & Dean, D. J. (1999). Comparative accuracies of artificial neural networks and discriminant analysis in predicting forest cover types from cartographic variables. Computers and electronics in agriculture, 24(3), 131-151._](https://github.com/arjundas1/Forest-Cover-Prediction-using-Classification-Mining-Techniques-and-Deep-Learning/blob/main/References/Comparative%20accuracies%20of%20artificial%20neural%20networks%20and%20discriminant%20analysis%20in%20predicting%20forest%20cover%20types%20from%20cartographic%20variables.pdf)

<!---
## Contact Us

_You can contact us through our LinkedIn account -_

* [John Harshith](https://www.linkedin.com/in/john-harshith-5354371b7/)
* [Arjun Das](https://www.linkedin.com/in/arjundas1/)
* [Siddharth Pal](https://www.linkedin.com/in/siddharthpal20/)
--->

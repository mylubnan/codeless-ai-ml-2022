# Codeless-AI-ML-2022-Project

## Overview
Understanding the concept of the CRISP-DM model then clarifying which part of the project is in which part of the CRISP-DM model, and making 3 modeling of AI/ML using KNIME platform then comparing which model is most suitable to this data set (Titanic) by checking the which one got the most accurate. This repository will consist of
- KNIME_project_ai_titanic.knwf | For the KNIME workflow

## Tools
- KNIME

## Nodes being used in KNIME.
- CSV Reader
- Statistics
- Missing Value
- Number to String
- Domain Calculator
- Partitioning
- Rule Engine
- String Manipulation
- Column Filter
- Random Forest Learner
- Random Forest Predictor
- Naive Bayes Learner
- Naive Bayes Predictor
- Decision Tree Learner
- Decision Tree Predictor
- Scorer
- Column Rename
- Table View

## Business Understanding of CRISP-DM
The main objective of this project is to make the AI/ML prediction base on the titanic data set when the titanic disaster happen so that we know how much chance that people would survive and not survived. Moreover, it is to see which model of AI/ML is the most suitable compared with the accuracy of the prediction.

## Data Understanding of CRISP-DM 
Import data by CSV Reader node, then make it easier to see using the Statistics node.
<p float="left">
 <img src="Images/1.png" alt="image" width="25%"/> 
</p>

##  Data Preparation of CRISP-DM
Add the missing data of the columns because will need it for the condition to predict later on using the Missing Value node, then use the Number To String node for changing the numeric of data to string because to make predictions it is better to use string but not always necessary for this project it is needed so that in the Learner part it will not get any error. Next, due to the cause that adding the missing values, it needs to also add a Domain Calculator node for the Learner to work properly, and inside it change the Restrict number of possible values to 90-120. Next, use the Partitioning node to separate the data that use for learning and the data that use for checking the result of learning which is the prediction. Next, use the Random Forest Learner node to teach AI or ML for prediction. Then, the Random Forest Predictor node receives the data from the route of the Random Forest Learner node, and another one receives the data from the route of the Partitioning node. Lastly, use the Scorer node to show the result of all such as correct classified, wrong classified, accuracy, etc. Probably get the accuracy of prediction around 75%.

<p float="left">
 <img src="Images/2.1.png" alt="image" width="80%"/> 
</p>

Next, to increase the accuracy of data use the Rule Engine node put between the CSV Reader node and the Missing Value noded for the expression to define the age range use this
```
$Age$ < 3 => "Infant"
$Age$ < 12 => "Child"
$Age$ < 20  => "Teenager"
$Age$ < 55 => "Adult"
$Age$ < 90 => "Senior"
TRUE => "Other" 
```
Now probably get the accuracy of prediction around 78%.

<p float="left">
 <img src="Images/2.2.png" alt="image" width="80%"/> 
</p>

Again, to increase the accuracy of data use the string Manipulation node for the config to define the age range base of 4 first characters of the individual name, in expression put this

`
substr($Name$, indexOfChars($Name$, "," )+2 , 4 )
`

Then add the new Rule Engine node put after the string Manipulation but before the previous Rule Engine node in the expression put this
```
$First4Titles$ IN ("Mrs.","Mr. ", "Dr. ", "Don.", "Rev.", "Mme.", "Jonk", "the ", "Capt", "Mlle", "Col.", "Sir.", "Lady", "Majo", "Ms. ") => "Adult"
$First4Titles$ IN ("Miss","Mast") => "Child"
```

Then add another new Rule Engine node put before the Missing Value node, in the expression put this
```
MISSING $AgeBracket$ => $AgeBracket2$
TRUE => $AgeBracket$
```

<p float="left">
 <img src="Images/2.3.png" alt="image" width="80%"/> 
</p>

Now, you can you these nodes for preparation data to connect to the model such as the Random Forest node, the Naive Bayes node, and the Decision Tree node then we can see the result and so on.

<p float="left">
 <img src="Images/2.png" alt="image" width="80%"/> 
</p>

##  Modeling of CRISP-DM
Firstly we use the 3 Random Forest nodes to see that check that the improvement of the rule engine that we use is working so we only use the most one of these prepared data.

<p float="left">
 <img src="Images/3.1.png" alt="image" width="60%"/> 
</p>

Next, when we know which one is most prepared so use that one to another model which is the Naive Bayes node.

<p float="left">
 <img src="Images/3.2.png" alt="image" width="70%"/> 
</p>

Moreover, we use that one to another model which is the Decision Tree node.

<p float="left">
 <img src="Images/3.3.png" alt="image" width="70%"/> 
</p>

Then, we can see the result in the next part

<p float="left">
 <img src="Images/3.png" alt="image" width="60%"/> 
</p>

##  Evaluation of CRISP-DM
In the scorer, we can see the result of all such as correct classified, wrong classified, accuracy, etc. Then use the Column Appender node then connect all 3 nodes from the Random Forest nodes. After that use the Column Rename node to make the viewer not confused with the names of the columns. Then in first table view will show the comparison of the number of correct and wrong predictions of each model. However, in the second part, we put the rule engine to make the comparison of the model itself based on the accuracy of each model and then show in the table view which one is the best suitable.

<p float="left">
 <img src="Images/4.1.png" alt="image" width="70%"/> 
</p>

<p float="left">
 <img src="Images/5.1.png" alt="image" width="80%"/> 
</p>

<p float="left">
 <img src="Images/5.2.png" alt="image" width="80%"/> 
</p>

In the scorer, we can see the result of all such as correct classified, wrong classified, accuracy, etc. Then use the Column Appender node then connect all 3 nodes from the Random Forest nodes. After that use the Column Rename node to make the viewer not confused with the names of the columns. Then in first table view will show the comparison of the number of correct and wrong predictions of each model. However, in the second part, we put the rule engine to make the comparison of the model itself based on the accuracy of each model and then show in the table view which one is the best suitable model.

<p float="left">
 <img src="Images/4.2.png" alt="image" width="70%"/> 
</p>

<p float="left">
 <img src="Images/5.3.png" alt="image" width="80%"/> 
</p>

<p float="left">
 <img src="Images/5.4.png" alt="image" width="80%"/> 
</p>

<p float="left">
 <img src="Images/4.png" alt="image" width="70%"/> 
</p>

## Whole Process in KNIME
<p float="left">
 <img src="Images/final.png" alt="image" width="100%"/> 
</p>

# Author
- Lubnan Samae

# Project Resources
- https://towardsdatascience.com/a-beginners-guide-to-kaggle-s-titanic-problem-3193cb56f6ca // Explanation resource
- https://www.kaggle.com/competitions/titanic/ // Data-set resource
- https://www.youtube.com/watch?v=OOgRIwrwJQY // Tutorial resource

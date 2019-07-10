# The Naive Modeler
**Expectation:**  
It is sometimes suggested that machine learning models are so "intelligent" that you simply have to plug training data into a model to fit it and you should get pretty much as good a model as can be achieved. Perhaps some playing around with the very basic model parameters might be needed but that's all.

**Reality**  
Often, such naive model building does not yield very good models. There are many reasons why this might happen. For example:
* the presence of interaction effects
* the need for calculation of appropriate features from the raw data
* cleaning of the data would be needed and requires in-depth knowledge of the data
* ...

**This Project**  
The purpose of this project is simply to investigate how well common predictive regression model types can handle significant interaction between predictors. The code uses randomly generated data and builds regression models of the most common types, sometimes trying multiple simple variations. It assumes that the modeler is not attempting to understand the data very closely, is not going to calculate new features and will only attempt to try the most basic variations of the predictive regression model types.

**The Data**  
The data will contain box dimensions (length, width and height) generated randomly, each between 0 and 1.0. These are the predictors. The outcome is the box volume. There is no error term present so perfect predictions are possible. The code sets aside 10% of the data as the test data, leaving 90% as training data.

**The Models**  
Various regression model types are built. A model predicting the volume according to: 
predicted_volume = length x width x height 
would achieve 100% accuracy. However, most model types cannot predict using a relationship like this and so will be less than 100% accurate. Sinde the assumption is that the user is naive, the code does not calculate dimensions_product = length x width x height as a new feature which is what a modeler who understands the data and the abilities of various model types would do.

**Library Requirements**  
numpy, scikit-learn(sklearn) and (for the last models) tensorflow

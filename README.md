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

**Comparison Data**
For comparison, all the models can be run against an outcome feature (length of tape to go around box) which means there is no feature interaction. Uncomment the relevant section below.

**The Models**  
Various regression model types are built. A model predicting the volume according to: 
predicted_volume = length x width x height 
would achieve 100% accuracy. However, most model types cannot predict using a relationship like this and so will be less than 100% accurate. Sinde the assumption is that the user is naive, the code does not calculate dimensions_product = length x width x height as a new feature which is what a modeler who understands the data and the abilities of various model types would do.

**Library Requirements**  
numpy, scikit-learn(sklearn) and (for the last models) tensorflow

**Results**  
_*Comparison data - no interaction*_  
As expected, many models gave perfect or very good predictions. Models worth commenting on:
* Support Vector Regression did very well except if the kernel was sigmoid
* Decision tree did well but required a depth of 7, with 128 leaves, to achieve better than 5% error
* sklearn's MLPRegressor did well no matter what activation was used
* Tensorflow NN with only input and output layer did well except when the activation function was sigmoid, tanh or softmax (in which cases it performed spectacularly badly)
* Tensorflow NN with 3 hidden layers performed very similarly to the Tensorflow NN with no hidden layers.

_*Box volumes - exhibiting feature interaction*_  
Mostly models performed quite badly, usually having a %error greater than 50%.  Models worth commenting on:
* Decision tree got %error own to 10% once enough depth was allowed. This is not surprising since the tree breaks the data down into many numeric ranges and then the interaction effects within these small ranges are minimised.
* Random forest regressor achieved 5% error - one of the best performances.
* sklearn's MLPRegressor managed %error rates below 12% for tanh and relu.
* Tensorflow NN with only input and output layer hardly got below 30% no matter which activation function was used. Earlier experiments showed that if an optimizer other than RMSprop was used the results would be very very poor.
* Tensorflow NN with 3 hidden layers did quite well, achieviung below 7% errors except with linear and softmax activation functions. Earlier experiments showed that if an optimizer other than RMSprop was used the results would be very very poor.

**Conclusions**  
A naive modeler, not knowing the data well and not recognising the presence of very significant feature interaction, might be surprised at how badly the first model attepts are performing. Probably the only models that would work at all well would be some form of random forest with a large enough depth of a neural network with several hidden layers and even then the modeler would have to try activation functions (and optimizers) until one that works is picked. If the modeler recognised that the outcome correlated with the product of the 3 predictive features then caclulating this product would mean that the results should be near perfect for most model types.
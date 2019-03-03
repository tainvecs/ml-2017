## Environment 
* Ubuntu 18.04
* Python 3.6.8
* numpy 1.16.0, pandas 0.24.0, matplotlib 3.0.2


## Maintainer Info
* Chin-Ho, Lin
* tainvecs@gmail.com
* [Github](https://github.com/tainvecs/ml-2017)


## Overview
Before deep learning models, we may start from regression models. A Regression model can be viewed as a swallow neural network model with single hidden layer. In the first homework of ml-2017, we are asked to implement a linear regression model and solve a regression problem.


## Dataset

The dataset consist of 18 different air pollution sources collected at Fengyuan air pollution observatory in Taiwan. 

* **Training Data**
	- /data/train.csv
	- The training data contains the first 20 days data in each month of an year.
	- Given the 24 hours data of 18 different air pollution sources, we have to extract training features and train our linear regression model.

* **Test Data**
	- /data/test.csv
	- Test data is extracted from the last 10 days data in each month of an year.
	- Given data of 9 continuous hours, we have to predict the value of air pollution source PM2.5 in next hour.
	

## Linear Regression Model


* **--train** (str)
	- path of training data
	- If specified, new model will be trained and output.
* **--test** (str)
	- path of test data
	- If specified, prediction will be output to **--out_predict**.
* **--validate** (float or int)
	- float 0~1: the proportions of validation set split from training dataset 
	- int > 1: number of validation data slice from training dataset
	- validation data should not be more than 30\% of training dataset
* **--in_model** (str)
	- path of the model to load
* **--random_seed** (int)
	- random seed for splitting training and validation data
* **--iter_n** (int)
	- number of training iteration
* **--batch_size** (int)
	- sgd batch size
* **--eta** (float)
	- learning rate
* **--l2_lambda** (float)
	- l2 norm lambda value
* **--optimizer** (str)
	- option: **\"adam\"**, **\"ada\"**
		* adam optimizer
		* ada gradient
* **--beta_m** (float)
	- bata value of momentum
	- The value should be specified if the optimizer is \"adam\".
* **--beta_v** (float)
	- bata value of velocity
	- The value should be specified if the optimizer is \"adam\".
* **--epsilon** (float)
	- The small value for avoiding divide by zero error while calculating gradient.
* **--early_stop** (bool)
	- early stopping based on validation value
* **--out_log** (str)
	- path to output log file
* **--out_model** (str)
	- path to output model
* **--out_predict** (str)
	- path to output test prediction file
* **--debug** (bool)
	- printing debug message


## Model

* a 163-dimensional numpy array
* the first 162 dimension is the training feature weight **w**
* the last dimension is the bias term **b**


## Parameters

* **Adam Optimizer**
	- **eta**: 10, **l2_lambda**: 0.01, **iter_n**: 10000
	- **beta_m**: 0.9, **beta_v**: 0.999
	- **batch_size**: 10, 50, 100, 500, 1000

![](https://github.com/tainvecs/ml-2017/blob/master/hw1/png/adam-batch_size-eta_10_l2_lambda_0.01.png?raw=true)

* Adam optimizer with small batch size and large learning rate results in considerable increase on RMSE.


* **Adam Optimizer**
	- **eta**: 0.01, **l2_lambda**: 0.01, **iter_n**: 10000
	- **beta_m**: 0.9, **beta_v**: 0.999
	- **batch_size**: 10, 50, 100, 500, 1000 

![](https://github.com/tainvecs/ml-2017/blob/master/hw1/png/adam-batch_size-eta_0.01_l2_lambda_0.01.png?raw=true)

* On the contrary, a smaller learning rate shows more stable performance on RMSE.


* **Ada Gradient**
	- **batch_size**: 50, **l2_lambda**: 0.01, **iter_n**: 10000
	- **eta**: 1e-4, 1e-3, 1e-2, 1e-1, 1, 10

![](https://github.com/tainvecs/ml-2017/blob/master/hw1/png/ada-eta-batch_size_50_l2_lambda_0.01.png?raw=true)

* In contrast, a too small learning rate using ada gradient leads to great RMSE increase.


* **Adam Optimizer**
	- **eta**: 0.01, **batch_size**: 50, **iter_n**: 10000
	- **beta_m**: 0.9, **beta_v**: 0.999
	- **l2_lambda**: 1e-4, 1e-3, 1e-2, 1e-1, 1

![](https://github.com/tainvecs/ml-2017/blob/master/hw1/png/adam-l2_lambda-eta_0.01_batch_size_50.png)

* **Ada Gradient**
	- **eta**: 0.01, **batch_size**: 50, **iter_n**: 10000
	- **l2_lambda**: 1e-4, 1e-3, 1e-2, 1e-1, 1

![](https://github.com/tainvecs/ml-2017/blob/master/hw1/png/ada-l2_lambda-eta_0.01_batch_size_50.png)

* The L2 regularization lambda does not shows significant influence on RMSE validation value in this task, no matter with adam optimizer or ada gradient.
# Heart-rate-prediction
## Description:
This project is the implementation of code related to Article "Real-Time System Prediction for Heart Rate Using Deep
Learning and Stream Processing Platforms".
The article was about heart rate prediction.
I got 3 minutes as input in this code and predict 5 minutes as output. We have the heart rate for every 0.5 seconds in the data set. So for getting 3 minutes as input, our input shape will be like this: 60(60 seconds per minute) * 3(minutes) * 2(for 1 second) = 360,  and for output shape(predict 5 minutes), it will be : 60 * 5 * 2 = 600.

Before starting to work with our data, we have to check if our data is stationary or not.
For this part, I checked it in three ways: 
  1. Histogram plot to check if we have normal distribution data or not.
  2. calculate mean and variance in parts of data to understand whether our mean or variance in our data is alike or not.
  3. Dickey-Fuller test

  If our data wasn't stationary, we had to make it stationary (It was stationary.)

After that, we have to scale our data between [-1,1] 
* There are some functions that I will describe here:
  *   to_supervised : 
     this function will take our dataset, make windows and predictions, and make an array containing two columns (3 minutes input, 5minutes output).
And the next window and prediction will be in the next row.
  *   split_dataset: It will take our dataset, supervise data via the to_supervised function, and split it to train and test.

These parts of code were about preparing data for building a model.

The next step is about building a model.  
  (first, I made my model without Keras tuner. and then I used Keras tuner )
  * Functions: 
    * build_model: it takes one argument name hp and prepares a model to tune model parameters. number of neurons is in the range (10, 500), and the dropout value is in the range (0.1, 0.9)

    * tune: it defines parameters(train, test,  model name, and directory address, where our result will save). It will find the best parameters and build a model with the parameters.

The next part is about evaluation.we used rmse for evaluation mertric.
  * Functions:
    * rmse: it calculates rmse score.
    * evaluate_model: first, it runs the build_model function, then tune parameters and build model,  and at last calculates rmse score.

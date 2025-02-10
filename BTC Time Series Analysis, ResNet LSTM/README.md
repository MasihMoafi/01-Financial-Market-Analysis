# Time-series Analysis by using LSTM in Conjunction with ResNet for Efficiency

## Data Preparation

Note: The dataset is uploaded in this repository. You can use any other dataset you want as well, the model generalizes quite well.

The first step involves loading and preparing the data. The Bitcoin price data is loaded from a CSV file and any missing data is removed. A visualization of the closing prices is generated to provide an overview of the data. 

## Sequence Creation and Normalization

To train the LSTM model, sequences of input features and corresponding target values are created. The price and volume data are normalized using MinMaxScaler. The data is then divided into the training, validation, and test sets.

## LSTM Model Architecture

The LSTM model consists of two LSTM layers with dropout regularization. The second LSTM layer returns sequences, and a TimeDistributed Dense layer is applied to each time step. The Residual Network (ResNet) concept is utilized by wrapping the LSTM model with a custom ResidualWrapper class.

## Model Training and Evaluation

The model is compiled with an Adam optimizer and mean squared error (MSE) loss function. It is trained on the training data with validation on the validation set. The training and validation loss curves are plotted to assess the model's performance.

Evaluation metrics such as mean absolute error (MAE), mean squared error (MSE), and root mean squared error (RMSE) are calculated on the test set to quantify the model's accuracy.

(MAE): 0.015
(MSE): 0.0005
(RMSE): 0.023

## Swing Trading Simulation

In addition to the time-series analysis, a swing trading simulation is performed using a simple strategy. Based on a moving average indicator (SMA_30), buy and sell signals are generated. The simulation tracks the portfolio value and trade types (buy/sell) throughout the last two months.

Note: We cutoff the last two months' data from our training so that our predictions be accurate.

Since our swing trading wasn't profitable, we developed a new strategy that is indeed profitable, the details of this strategy are explored in the project.

## Results

The initial portfolio value and the final portfolio value after the swing trading simulation are displayed. 

---

Note: The model is predicting price changes rather than absolute prices, this is a common strategy used in financial markets to make the model more robust.

A more detailed explanation to gain better intuition as to what the model is doing: 
    The model was trained to predict the change in price and volume for the next 6 days based on the last 6 days of data.
    Then, the predicted change is added to the last known price to get the predicted price.
    The trading strategy involves buying when the predicted price is higher than the current price (and the difference is above a certain threshold). It means that the model is predicting an upward trend in price.
    If the price actually goes up, the strategy will make a profit. If it goes down, it will make a loss.

So even though the model is predicting price changes rather than absolute prices, it's still capable of identifying trends in the price data, which is what this trading strategy is based on. This is why the strategy could be profitable.

Note: Several different architectures where tested and compared, the best results were made by the resNet LSTM model. We tried CNN-transformers, LSTM, regression, added ConvNets and Dense layers to our model etc.

## Summary

This project showcases the utilization of ResNet LSTM model for efficient time-series analysis of Bitcoin price data. By combining these techniques, the model's accuracy and speed increases significantly.

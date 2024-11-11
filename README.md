### Developed by: SHARAN MJ
### Reg no: 212222240097
### Date:
# Ex.No: 08     MOVINTG AVERAGE MODEL AND EXPONENTIAL SMOOTHING
 


### AIM:
To implement Moving Average Model and Exponential smoothing Using Python on Onion Price data.
.
### ALGORITHM:
1. Import necessary libraries
2. Read the electricity time series data from a CSV file,Display the shape and the first 20 rows of
the dataset
3. Set the figure size for plots
4. Suppress warnings
5. Plot the first 50 values of the 'Value' column
6. Perform rolling average transformation with a window size of 5
7. Display the first 10 values of the rolling mean
8. Perform rolling average transformation with a window size of 10
9. Create a new figure for plotting,Plot the original data and fitted value
10. Show the plot
11. Also perform exponential smoothing and plot the graph
### PROGRAM:
```python
# Import necessary libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import warnings
from statsmodels.tsa.holtwinters import ExponentialSmoothing

# Suppress warnings
warnings.filterwarnings('ignore')

# Read the dataset (adjust the path accordingly)
data = pd.read_csv('/content/OnionTimeSeries - Sheet1.csv')

# Convert 'Date' to datetime format and set it as the index
data['Date'] = pd.to_datetime(data['Date'], format='%m/%d/%Y')  # Changed format to '%m/%d/%Y'
data.set_index('Date', inplace=True) # Changed to 'Date' instead of 'date'

# Focus on the 'Adj Close' column
adj_close_data = data[['']]

# Display the shape and the first 5 rows of the dataset
print("Shape of the dataset:", adj_close_data.shape)
print("First 5 rows of the dataset:")
print(adj_close_data.head())

# Plot Original Dataset (Adj Close Data)
plt.figure(figsize=(12, 6))
plt.plot(adj_close_data['Min'][:100], label='Original Onion Price Data', color='blue')
plt.title('Annual Change in Onion Price (First 100 Data Points)')
plt.xlabel('Date')
plt.ylabel('Price of Onion')
plt.legend()
plt.grid(True)
plt.show()

# Moving Average
# Perform rolling average transformation with a window size of 10
rolling_mean_3 = data['Min'].rolling(window=3).mean()

# Plot Moving Average
plt.figure(figsize=(12, 6))
plt.plot(data['Min'][:100], label='Original Price', color='blue')  
plt.plot(rolling_mean_3, label='Moving Average (window=3)', color='orange')
plt.title('Moving Average of Price')
plt.xlabel('Date')
plt.ylabel('Price of Onion')
plt.legend()
plt.grid()
plt.show()

# Exponential Smoothing
model = ExponentialSmoothing(data['Min'], trend='add', seasonal=None)
model_fit = model.fit()


future_steps = 5
predictions = model_fit.predict(start=len(data), end=len(data) + future_steps - 1)

future_dates = pd.date_range(start=data.index[-1] + pd.Timedelta(days=1), periods=future_steps)

# Plot the original data and Exponential Smoothing predictions
plt.figure(figsize=(12, 6))
plt.plot(data['Min'], label='Original Price', color='blue')
plt.plot(future_dates, predictions, label='Exponential Smoothing Forecast', color='orange')
plt.title('Exponential Smoothing Predictions for Price')
plt.xlabel('Date')
plt.ylabel('Price of Onion')
plt.legend()
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()
```

### OUTPUT:

![Screenshot 2024-11-11 114355](https://github.com/user-attachments/assets/b0387cf3-5bc1-4f90-a58a-10a7c401cee6)


#### Plot Transform Dataset

![Screenshot 2024-11-11 114401](https://github.com/user-attachments/assets/b9330873-5bf8-48c8-bf23-a4da7cc97f9b)


#### Moving Average

![Screenshot 2024-11-11 114409](https://github.com/user-attachments/assets/c9527b0c-c766-419a-b0a5-582f4affd1dd)


#### Exponential Smoothing


![Screenshot 2024-11-11 114615](https://github.com/user-attachments/assets/edbc589f-d411-4677-8e3c-a3318a2ae699)

### RESULT:
Thus , successful implemention of the Moving Average Model and Exponential smoothing using python is done.

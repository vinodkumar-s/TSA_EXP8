## DEVELOPED BY: VINOD KUMAR S
## REGISTER NO: 212222240116
## DATE:

# Ex.No: 08     MOVING AVERAGE MODEL AND EXPONENTIAL SMOOTHING
 
## AIM:
To implement Moving Average Model and Exponential smoothing Using Python.
## ALGORITHM:
1. Import necessary libraries
2. Read the coffee Sales time series data from a CSV file,Display the shape and the first 20 rows of
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
## PROGRAM:
```python
# Import necessary libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import warnings
from statsmodels.tsa.holtwinters import ExponentialSmoothing

# Suppress warnings
warnings.filterwarnings('ignore')

# Read the dataset from the uploaded CSV file
file_path = 'coffeesales.csv'  # Path to the uploaded dataset
data = pd.read_csv(file_path)

# Display the shape and the first few rows of the dataset
print("Shape of the dataset:", data.shape)
print("First 20 rows of the dataset:")
print(data.head(20))

# Ensure the 'datetime' column is in datetime format and set it as index
data['datetime'] = pd.to_datetime(data['datetime'])
data.set_index('datetime', inplace=True)

# Plot Original Sales Data (money)
plt.figure(figsize=(12, 6))
plt.plot(data['money'], label='Original Sales', color='blue')
plt.title('Original Sales Data (Money)')
plt.xlabel('Date')
plt.ylabel('Sales (Money)')
plt.legend()
plt.grid()
plt.show()

# Moving Average
# Perform rolling average transformation with a window size of 3 (adjust as needed)
rolling_mean_3 = data['money'].rolling(window=3).mean()

# Plot Moving Average
plt.figure(figsize=(12, 6))
plt.plot(data['money'], label='Original Sales', color='blue')
plt.plot(rolling_mean_3, label='Moving Average (window=3)', color='orange')
plt.title('Moving Average of Sales (Money)')
plt.xlabel('Date')
plt.ylabel('Sales (Money)')
plt.legend()
plt.grid()
plt.show()

# Exponential Smoothing
model = ExponentialSmoothing(data['money'], trend='add', seasonal=None)
model_fit = model.fit()

# Make predictions for the next 5 periods (adjust as needed)
future_steps = 5
predictions = model_fit.predict(start=len(data), end=len(data) + future_steps - 1)

# Create a future index for the predicted dates
future_dates = pd.date_range(start=data.index[-1] + pd.Timedelta(days=1), periods=future_steps)

# Plot the original data and Exponential Smoothing predictions
plt.figure(figsize=(12, 6))
plt.plot(data['money'], label='Original Sales', color='blue')
plt.plot(future_dates, predictions, label='Exponential Smoothing Forecast', color='orange')
plt.title('Exponential Smoothing Predictions for Sales (Money)')
plt.xlabel('Date')
plt.ylabel('Sales (Money)')
plt.legend()
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()

```

## OUTPUT:
### GIVEN DATA
![image](https://github.com/user-attachments/assets/56b1ac47-6fde-4c3b-9ca4-0f58cfdf598d)


### Moving Average

![image](https://github.com/user-attachments/assets/e651f48e-5edc-4327-b2f5-9d483824f500)

### Plot Transform Dataset

![image](https://github.com/user-attachments/assets/708bf9e3-b700-49b8-b5f2-99fa889f4b61)


### Exponential Smoothing

![image](https://github.com/user-attachments/assets/2ad4008a-9c52-41a7-8358-2ede3fe0231f)




## RESULT:
Thus, the program to implement the Moving Average Model and Exponential smoothing using python is executed successfully.

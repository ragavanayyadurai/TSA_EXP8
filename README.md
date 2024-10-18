## DEVELOPED BY: Ragavendran A
## REGISTER NO: 212222230114
## DATE:

# Ex.No: 08 MOVING AVERAGE MODEL AND EXPONENTIAL SMOOTHING
 
## AIM:
To implement Moving Average Model and Exponential smoothing Using Python.
## ALGORITHM:
1. Import necessary libraries
2. Read the House Sales time series data from a CSV file,Display the shape and the first 20 rows of
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
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import warnings
from statsmodels.tsa.holtwinters import ExponentialSmoothing

warnings.filterwarnings('ignore')

# Load dataset
file_path = '/content/Summer_olympic_Medals.csv'
data = pd.read_csv(file_path)

print("Shape of the dataset:", data.shape)
print("First 20 rows of the dataset:")
print(data.head(20))

# Filter data for a specific country, e.g., 'USA'
country = 'United States'
country_data = data[data['Country_Name'] == country]

# Aggregate the total number of medals per year
country_data['Total_Medals'] = country_data['Gold'] + country_data['Silver'] + country_data['Bronze']
country_data = country_data[['Year', 'Total_Medals']].dropna()

# Set the 'Year' as the index and sort by year
country_data['Year'] = pd.to_datetime(country_data['Year'], format='%Y')
country_data.set_index('Year', inplace=True)

# Plot original medal data
plt.figure(figsize=(12, 6))
plt.plot(country_data['Total_Medals'], label='Total Medals', color='blue')
plt.title(f'Total Medals Over Time for {country}')
plt.xlabel('Year')
plt.ylabel('Number of Medals')
plt.legend()
plt.grid()
plt.show()

# Moving average calculation (window=3)
rolling_mean_3 = country_data['Total_Medals'].rolling(window=3).mean()

# Plot moving average along with original data
plt.figure(figsize=(12, 6))
plt.plot(country_data['Total_Medals'], label='Total Medals', color='blue')
plt.plot(rolling_mean_3, label='Moving Average (window=3)', color='orange')
plt.title(f'Moving Average of Medals for {country}')
plt.xlabel('Year')
plt.ylabel('Number of Medals')
plt.legend()
plt.grid()
plt.show()

# Apply Exponential Smoothing
model = ExponentialSmoothing(country_data['Total_Medals'], trend='add', seasonal=None)
model_fit = model.fit()

# Forecast future steps
future_steps = 5
predictions = model_fit.predict(start=len(country_data), end=len(country_data) + future_steps - 1)

# Create future dates for forecasting
future_dates = pd.date_range(start=country_data.index[-1] + pd.Timedelta(days=365), periods=future_steps, freq='Y')

# Plot forecast
plt.figure(figsize=(12, 6))
plt.plot(country_data['Total_Medals'], label='Total Medals', color='blue')
plt.plot(future_dates, predictions, label='Exponential Smoothing Forecast', color='orange')
plt.title(f'Exponential Smoothing Predictions for {country}')
plt.xlabel('Year')
plt.ylabel('Number of Medals')
plt.legend()
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()

```

## OUTPUT:
### GIVEN DATA
![image](https://github.com/user-attachments/assets/bb0c1ee9-4ce9-48f3-8658-0a0c4ba382f7)

### Moving Average
![image](https://github.com/user-attachments/assets/30fe18b7-1c4a-4bc7-96e9-62ec5849fcef)

### Plot Transform Dataset
![image](https://github.com/user-attachments/assets/a14ec36c-97dc-425f-afe3-be782d724e61)

### Exponential Smoothing
![image](https://github.com/user-attachments/assets/39fefd27-3782-489c-8f9d-e4b1943ea0c9)


## RESULT:
Thus, the program to implement the Moving Average Model and Exponential smoothing using python is executed successfully.

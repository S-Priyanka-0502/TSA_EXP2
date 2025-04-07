# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION

### AIM:
To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:
Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program
### PROGRAM:

import pandas as pd

import numpy as np

import matplotlib.pyplot as plt

data=pd.read_csv('/content/AirPassengers.csv',parse_dates=['Month'],index_col='Month')

data.head()

resampled_data = data['#Passengers'].resample('Y').sum().to_frame()

resampled_data.head()

resampled_data.index = resampled_data.index.year

resampled_data.reset_index(inplace=True)

resampled_data.rename(columns={'Month': 'Year'}, inplace=True)

resampled_data.head()

years = resampled_data['Year'].tolist()

passengers = resampled_data['#Passengers'].tolist()

A - LINEAR TREND ESTIMATION

X = [i - years[len(years) // 2] for i in years]

x2 = [i ** 2 for i in X]

xy = [i * j for i, j in zip(X, passengers)]

n = len(years)

b = (n * sum(xy) - sum(passengers) * sum(X)) / (n * sum(x2) - (sum(X) ** 2))

a = (sum(passengers) - b * sum(X)) / n

linear_trend = [a + b * X[i] for i in range(n)]

B- POLYNOMIAL TREND ESTIMATION

x3 = [i ** 3 for i in X]

x4 = [i ** 4 for i in X]

x2y = [i * j for i, j in zip(x2, passengers)]

coeff = [[len(X), sum(X), sum(x2)],

[sum(X), sum(x2), sum(x3)],

[sum(x2), sum(x3), sum(x4)]]

Y = [sum(passengers), sum(xy), sum(x2y)]

A = np.array(coeff)

B = np.array(Y)

solution = np.linalg.solve(A, B)

a_poly, b_poly, c_poly = solution

poly_trend = [a_poly + b_poly * X[i] + c_poly * (X[i] ** 2) for i in range(n)]

VISULASING RESULT

print(f"Linear Trend: y={a:.2f} + {b:.2f}x")

print(f"\nPolynomial Trend: y={a_poly:.2f} + {b_poly:.2f}x + {c_poly:.2f}x²")

resampled_data['Linear Trend'] = linear_trend

resampled_data['Polynomial Trend'] = poly_trend

resampled_data.set_index('Year',inplace=True)

resampled_data['#Passengers'].plot(kind='line',color='blue',marker='o') #alpha=0.3 makes

resampled_data['Linear Trend'].plot(kind='line',color='black',linestyle='--')

resampled_data['#Passengers'].plot(kind='line',color='blue',marker='o')

resampled_data['Polynomial Trend'].plot(kind='line',color='black',marker='o')

### OUTPUT
A - LINEAR TREND ESTIMATION

![Screenshot 2025-04-07 183215](https://github.com/user-attachments/assets/bb53fbe7-8723-46e0-b6bd-7fccbf57c825)


B- POLYNOMIAL TREND ESTIMATION

![Screenshot 2025-04-07 183242](https://github.com/user-attachments/assets/756c00ad-31ef-4c55-b28e-83cc5d1975c5)


### RESULT:
Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.

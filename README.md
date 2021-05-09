# sql-pro

Data challenge 2021 Shopify



1.)

3145.13 is the mean of the entire 4th column (“order_amount”). I calculated the average of that entire column on excel and got the exact same number. Also when I imported pandas in python, I was able to get a diverse range of data to better understand the set. Looking at the data set using the eye test, you can see the outliers with some amounts totaling up to 704000.

Python input

Input:


import numpy as np 
import pandas as pd # CSV file
import os
df = pd.read_csv('sheet1.csv')
df.head()



max      704000.000000

I can find this value using the describe function which shows it to be $272 and standard deviation to be 132.06
df.order_amount.describe()


len(df['shop_id'].unique())#looking for the complete IQR average

df['order_amount'].hist()

print('median: ', np.median(df['order_amount']))

#filtering dataset to only include middle 50% of values
newdf = df[(df['order_id'] > 163) & (df['order_id'] < 390)]

print(np.median(newdf['order_id']))

Output

count    4738.000000
mean      283.814268
std       132.061996
min        90.000000
25%       161.000000
50%       272.000000
75%       362.000000
max       624.000000

This way eliminates the idea of having any outliers as it causes the average order value to look out of sorts.Using a method that is less prone to outliers can give us a better understanding of the AOV than  Filtering the outliers and using the range of the middle 50%.

b) I would find the average of the middle 50% of the data which does not include outliers that are vary large or very low.

c) 272


2)
a.)
Use Speedy express to count the number of entries


SELECT COUNT(*) AS NumberOfOrders
FROM [Orders]
JOIN [Shippers]
    ON [Shippers].ShipperID = [Orders].ShipperID
WHERE [Shippers].ShipperName = 'Speedy Express'
54 is the number of orders


b.)
SELECT LastName, MAX(OrdersTaken)

FROM

(SELECT LastName, COUNT(*) AS OrdersTaken

FROM (Orders

INNER JOIN Employees ON Orders.EmployeeID = Employees.EmployeeID)

GROUP BY Employees.EmployeeID);

Peacock had the most orders at 40
c.)

Product ID is 40 and total ordered quantity is 160. Now find the name of the most ordered product.

SELECT ProductName,SUM(Quantity) AS "TotalOrdered"
FROM [Orders]
JOIN [Customers]
    ON [Customers].CustomerID = [Orders].CustomerID
JOIN [OrderDetails]
    ON [OrderDetails].OrderID = [Orders].OrderID
JOIN [Products]
    ON [Products].ProductID = [OrderDetails].ProductID
WHERE Country = 'Germany'
GROUP BY [OrderDetails].ProductID

The output shows that the Boston Crab Meat has the greatest amount of orders at 160.

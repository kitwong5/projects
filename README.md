# Slope One and Weighted Slope One Recommender System
Slope One predictor is one of the widely-used method in recommendation systems. It is an rating-based collaborative filtering recommendation algorithm introduced in a paper by Lemire and Maclachlan in 2005.  Lemire and Maclachlan introduced sever CF algorithms like PER USER AVERAGE, The SLOPE ONE Scheme, the weighted SLOPE ONE Scheme, and The BI-POLAR SLOPE ONE Scheme. This code will put the focused in SLOPE ONE and the weighted SLOPE ONE Scheme.

SLOPE ONE Scheme is a model-based collaborative filtering. It used a simple linear regression model, the f(x) = x + b for prediction. x is representing the rating value and b is refer to the average difference between the ratings of one item of another. 

![image](https://github.com/kitwong5/weighted_slope_one.github.io/assets/142315009/1530c516-9fc9-447a-ae8b-e7bb44c5f569)

For example,  to make a prediction for user B on Item J, then the model will lookup other rated users rating (let say User A). It take the difference between Item J to another item i to calculate the deviation.  Then it take the average of deviation and use it to make prediction for User B on item J with just adding the deviation on top on item I’s rating value.

Base on this concept, let’s look at the prediction formula:
![image](https://github.com/kitwong5/weighted_slope_one.github.io/assets/142315009/883d7f39-061a-4edf-a4f8-d4c341386a58)

It calculates the average deviation of ratings between the target item j and other items i and then makes the rating prediction for item J.  The upper part of the formula is the summation of the deviation of item i with respect to item j plus the given rating value then it derived by the lower part, the number of rated items

Further drill down to the deviation part. It is just a straight forward formula that it just take the summation of rating different between the target item j vs other items i, then derived it by the number of rated items 


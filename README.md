# Slope One Recommender System
Slope One predictor is one of the widely used methods in recommendation systems. It is a rating-based collaborative filtering recommendation algorithm introduced in a paper by Lemire and Maclachlan in 2005.  Lemire and Maclachlan introduced several CF algorithms like PER USER AVERAGE, The SLOPE ONE Scheme, the weighted SLOPE ONE Scheme, and The BI-POLAR SLOPE ONE Scheme. This code will put the focus on SLOPE ONE and the weighted SLOPE ONE Scheme.

SLOPE ONE Scheme is a model-based collaborative filtering. It used a simple linear regression model, the f(x) = x + b for prediction. x represents the rating value and b refers to the average difference between the ratings of one item of another.

![image](https://github.com/kitwong5/weighted_slope_one.github.io/assets/142315009/9f3c7097-7464-4cb0-970a-95af4f1f9571)

For example,  to make a prediction for user B on Item j, the model will lookup other rated users rating (e.g. User A). It takes the difference between Item j to another item i to calculate the deviation.  Then it takes the average deviation and uses it to predict User B on item j by just adding the deviation on top of item I’s rating value.

Base on this concept, let’s look at the prediction formula:
![image](https://github.com/kitwong5/weighted_slope_one.github.io/assets/142315009/883d7f39-061a-4edf-a4f8-d4c341386a58)

- card(Rj) is the set of all relevant items
- devj,I is the average deviation of item i with respect to item j
- devj,i + ui is a prediction for uj given ui

It calculates the average deviation of ratings between the target item j and other items i and then makes the rating prediction for item j.  The upper part of the formula is the summation of the deviation of item i for item j plus the given rating value then it is derived by the lower part, the number of rated items.  Further drill down the deviation part, it is just a straightforward formula that it takes the summation of rating different between the target item j vs other items i, then derived it by the number of rated items 

# Weighted Slope One Scheme
However, there is a drawback to the Slope One formula that the number of ratings observed is not taken into account.  For example, the deviation average comes from 20 users vs 2000 users means different representatives, and this is not reflected in the slope one formula.

![image](https://github.com/kitwong5/weighted_slope_one.github.io/assets/142315009/615b0270-444e-48f2-a3ea-7cee11cc542a)

The weighted slope one formula has addressed this drawback by adding the part that I highlighted in red to the formula, the Cj,i variable, that is the number of users that have rated both items j and item i.  This Cj,i variable kind of represents the weight value for the item's deviation. With this weighted variable added, it can help improve the slope One formula’s prediction accuracy. 

# Personalized weighted Slope One method with with neighborhood concept
To further enhance the slope one method, personalized weighted can be added to the formula to improve the Slope One algorithm with considering the effects of both items and users.  To be specific, what got enhanced is the deviation calculation part from the prediction formula. 

![image](https://github.com/kitwong5/weighted_slope_one.github.io/assets/142315009/d32e2e83-de46-417c-9f8b-5251196ec840)

The deviation calculation now has 2 parts, the front part is from the original slop one formula and the second part is a newly added formula that multiplies the item’s deviation with the exponential form of similarities across the active user vs other users.  In this way, the slop one formulate can provide personalized recommendations with the associated of active user’s neighborhood information while computing the deviation between items.  Last but not least, the new formula also introduced a λ parameter to help control the deviation calculation of how much weight should come from the front part (that is the item rating deviation) 
or form the newly added part (that is the item rating deviation with user sim similarities weight added)

How does the parameter λ affects the prediction performance ? 

![image](https://github.com/kitwong5/weighted_slope_one.github.io/assets/142315009/02f45a44-941d-4950-8341-c472d49d4627)

I have performed testing with 0.2, 0.5 and 0.8 λ values on the personalized weighted Slope One model and found the higher the λ value, resulting in lower in prediction accuracy.  What it means is in the item deviation calculation part of the prediction formula, if more weight is assigned to the part with personalized weighed, it will result in better prediction accuracy.  It proved that the personalized weighed parts that we just added were able to help improve the weighted Slope One prediction accuracy.

Next, I have tried to add more neighborhood concepts to the Personalized weighted Slope One formula.  The Slope One formula uses all users’ rating data in the prediction
which means if someone has opposite preferences/opposite similarities compared to the active users, their data still will be used in the prediction formula.  To clean up these kinds of noise, I have introduced a parameter, KNN λ, to control the model to filter the user dataset according to the user's similarities value.

![image](https://github.com/kitwong5/weighted_slope_one.github.io/assets/142315009/78a16e01-2a11-4078-b1c8-af3a6aa00322)

I first performed the prediction by using the full user list, then I ran another test that only included the positive similarities users. At last, I ran the third round of tests using users' similarities values up to 0.5. The result showed if the model does not use all users for prediction, but only includes the positive similarities users for prediction, the prediction accuracy will increase. The other finding is if the user dataset with higher user similarities, the prediction accuracy will be increased.

# Conclusion

with a series of experiments, it concluded 
- the weight slop one formula that includes the number of rating elements as the weight value to the Slope One formula, can enhance the prediction accuracy
- adding user similarity as a weight to the rating deviation calculation can enhance Slope One prediction accuracy
- adding a threshold to control to use positive similarities users for the prediction can enhance Slope One prediction accuracy

# Reference
- Wikipedia Contributors (2010). Slope One. [online] Wikipedia. Available at: https://en.wikipedia.org/wiki/Slope_One
- Lemire D., Maclachlan A.: Slope One Predictors for Online Rating-Based Collaborative Filtering (2008)
- Shaw R., Patra B.: Slope One Meets Neighourhood: Revisiting Slop One Predictor in Collaborative Filtering (2020)  Available at: Slope One Meets Neighbourhood: Revisiting Slope One Predictor in Collaborative Filtering | SpringerLink
- Tian S., Ou L.: An Improved Slope One Algorithm Combining KNN Method Weighted by User Similarity (2016)  Available at: An Improved Slope One Algorithm Combining KNN Method Weighted by User Similarity | SpringerLink!




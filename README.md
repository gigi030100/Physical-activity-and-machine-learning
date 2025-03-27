# Physical Activity and Machine Learning

<img width="439" alt="Screenshot 2025-02-03 at 10 18 10" src="https://github.com/user-attachments/assets/d4f894e6-9c4b-40bd-ba85-9c092a710f23" />

## Research aim
This report aims to develop a reliable system which helps to predict the amount, and type of physical exercise a person completes using machine learning techniques. 

To achieve this goal, my report does the following:
1. Data cleaning and exploratory data analysis.
2. Investigated the relationship between heart rate and the type of physical activity performed.
3. Developed and tested a machine learning model to predict the amount and the type of exercise completed.

## Methodology

### Dataset
This report incorporates the PAMAP2 (Physical Activity Monitoring) dataset containing information regarding the physical exercises undertaken by participants. Data on the exercises undertaken include the timestamp, activity type, heart rate and the movement of hands, chest, and ankles using inertial measurement units (IMU). A total of 9 participants (8 males and 1 female) were sampled for the dataset. All subjects were asked to perform 12 different activities. Although they were given the option to complete other optional activities, this report will be mainly focusing on the activities described in the DataCollectionProtocol file.

Before performing exploratory data analysis, splitting the dataset into training and testing set is essential to avoid overfitting models. It's also helpful in avoiding biases that arise from preconceptions gained from looking at the data itself. The decision to split the dataset is applicable in this report due to the large sample size it constitutes. The data split ratio used for this report is 50:50. 

### Data pre-processing and Exploratory data analysis
As the original format of the data was merged into one file per subject, I've combined these separate files into one whole dataset to make data analysis more efficient.
Transient activities from the dataset was removed as these were irrelevant activities that were being performed in between exercises, e.g., moving from one location to another location for another task. This was done to reduce unnecessary noise from our dataset.
To overcome this, I interpolated data, using the interpolate() function, to replace missing points with predicted values according to its surrounding data points. As a result, a total of 1,942,868 rows of clean dataset were left to be analysed.

![Screenshot 2025-03-27 at 18 26 39](https://github.com/user-attachments/assets/9df15d94-62ef-4aff-82d1-6902f4abce00)

Regarding the investigation between two attributes, heart rate was chosen as one of the variables of interest which indicates the overall intensity of an exercise. According to our descriptive statistics, heart rate ranges from 52 seconds to 202 seconds, along with an average heart rate of 107.5 seconds. Data distribution of heart rate is outlined in figure 1 where we can also see outliers beyond 180 beats per minute.


![Screenshot 2025-03-27 at 18 29 17](https://github.com/user-attachments/assets/39d75cc1-3f3b-498b-9d27-2a09f0fa02c4)

In Figure 2, the data distribution of heartrate shows to be positively skewed meaning the mean heartrate is higher than the median value heart rate. Thus, due to outliers and non-symmetric distribution of heart rate values, heart rate will need to be standardised during hypothesis testing.


![Screenshot 2025-03-27 at 18 30 52](https://github.com/user-attachments/assets/7fb64306-2abb-4107-bf3e-1abb9f1a19f6)


In figure 3, I've also created another boxplot which displays the heart rate data distribution according to activity type. We can see that activity 24 (rope jumping) followed by activity 5 (running) are the top two most intense exercise according to our dataset. Meanwhile, activities 1-3 (lying, sitting, and standing) had the lowest heart rates.

## Hypothesis Testing
Activity 5 (running) and 24 (rope jumping) both have a common feature of being a locomotor movement. Locomotor movements refers to the movement of the body to one or many directions as a typical definition from the web. Does this mean activities incorporating locomotor movement will be associated with higher heartrate? To investigate this, I've divided the activity type into two categories (Locomotor exercises and non-locomotor exercises). The mean heart rate of these two categories will be compared. I've distinguished these activities according to whether it falls within the general definition of a locomotor movement.

#### Locomotor exercises
- Walking
- Running
- Cycling
- Nordic Walking
- Ascending & Descending the stairs
- Vacuuming
- Ironing
- Rope Jumping

#### Non-locomotor exercises
- Lying
- Sitting
- Standing

## Results of hypothesis testing
A Z-test was chosen as the sample size of locomotor (687,724) and non-locomotor activities (283,709) both exceed the threshold sample size of 30. Firstly, the mean, standard deviation, and the sample size of heart rate in both locomotor and non-locomotor activities were obtained. The difference in mean heart rate of both types of activities were calculated which resulted into 36.91 beats per minute (2 decimal places). Mean heart rate difference was then converted into a standardised normal distribution value of 0.03 (two decimal places). For hypothesis testing, significance level of 0.05 was specifically chosen as this level is the standard level to distinguish between significant and non-significant results (Di Leo & Sardanelli, 2020). Following the Z-test under the assumption of my null hypothesis, a p-value of 0.0 was obtained. As our p-value was below our significance level of 0.05, we can reject the null hypothesis and accept the alternative hypothesis whereby heart rate is associated with locomotor exercises. Moreover, having a p-value of 0.0 means there's approximately 0% chance that results occurred randomly.

## Multiple Linear Regression to predict amount of participant activity
Multiple linear regression was used to predict the amount of exercises undertaken by participants. The amount of activity completed was operationalised using heart rate since a person's heart rate tends to increase the more exercises they do, thus reflecting the amount of physical activity done. Feature selection for this linear model was implemented by determining attributes of the dataset that moderately correlated with heart rate. A threshold of 0.4 Pearson's correlation coefficient was chosen which is indicative of a moderate correlation (theBMJ, 2020). Heart rate was correlated against all other attributes within the data, resulting in 4 features being selected for having a correlation coefficient of above 0.4: timestamp (0.78), chestacc16_3 (0.41), chestMag2(0.40), and chestMag3(0.45) Once the linear regression model was fitted onto the training dataset, this was used to make heart rate predictions in the testing dataset. These heart rate predictions were then compared to the actual heart rate predictions in the testing dataset. To examine the goodness of fit model derived from the training dataset, the root mean squared error (RMSE) was calculated. Resultingly, the average difference between predicted and real values in the testing dataset is 16.36.

## Logistics Regression to predict the type of physical activity performed (locomotor vs non-locomotor movements)
A Logistics regression model was used as this model operates on the dependent variable having binary outputs or being a categorical variable. Since I'm interested in determining the type of activity performed, the dependent variable will be categorical. Therefore, a new attribute was created in the dataset whereby activity was converted into dummy variables: non-locomotor (0) and locomotor exercises (1). As timestamp, chestacc16_3, chestMag2, and chestMag3 were moderately correlated with heart rate, these features were chosen for logistics regression model. Heart rate was also chosen as there was a significant difference in mean heart rate between locomotor and non-locomotor exercises. Numerical variables such as timestamp, heartrate, chestacc16_3, chestMag2, and chestMag3 were normalised to ensure these features are comparable on the same scale. This helps avoid larger scales from certain feature(s) affecting the rest of the model. Next, the logistics model was derived from the training dataset and was used to predict the activity type in the testing dataset.

To evaluate the overall fit of this model, the precision, recall, and f1 score metrics were calculated. Resultingly, a precision value of 1.0 for non-locomotor exercises indicates that out of all the exercises that the model predicted to be a non-locomotor exercise, 100% were correctly predicted to be a non-locomotor movement. Meanwhile, a precision value of 0.91 indicates that out of all the locomotor exercises predicted by the model, 91% of them were predicted correctly.

Regarding f1-score, values of 0.86 and 0.95 for non-locomotor and locomotor exercises respectively indicates that the model developed has good predictive performance as it's close to 1.

## 6. Summary

In summary, this report aimed to develop a hypothesis and test the relationship between heart rate and locomotor exercises. Based on exploratory data analysis, I predicted that locomotor exercises will have a significantly higher heart rate than non-locomotor exercises due to its high intensity. This hypothesis was tested by calculating the mean heart rate difference between locomotor and non-locomotor exercises. Results of this test confirmed that locomotor exercises were indeed associated with increased heart rate. However, cautious should be taken from this as heart rate can affected by other factors external from exercising, e.g., nervousness or even anxiety. To control for these extraneous variables, further data collection which implements participant screening can be done to control for a participant's mental state.

This report also aimed to develop a reliable system which helps to predict the amount of exercise (using heart rate) and type of physical exercise a person completes (locomotor vs non-locomotor exercises). Here, a logistics regression model was developed with the goal of predicting whether the exercise performed was locomotor or non-locomotor using heart rate, duration, chest acceleration, and chest magnetometer data. The performance of this model was also evaluated which resulted in good levels of accuracy. However, the uneven sample of male and female participants means our model may be good at predicting the amount and type of exercises performed by males as opposed to both males and females. Hence, further data collection should incorporate more female participants to be able to reliably predict the amount, and type of exercises performed by males and females.



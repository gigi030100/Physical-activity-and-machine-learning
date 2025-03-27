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
This report incorporates the PAMAP2 (Physical Activity Monitoring) dataset containing information regarding the physical exercises undertaken by participants. Data on the exercises undertaken include the timestamp, activity type, heart rate and the movement of hands, chest, and ankles using inertial measurement units (IMU). A total of 9 participants (8 males and 1 female) were sampled for the dataset. All subjects were asked to perform 12 different activities. 

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


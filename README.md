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

### Data pre-processing and Exploratory data analysis
As the original format of the data was merged into one file per subject, I've combined these separate files into one whole dataset to make data analysis more efficient.
Transient activities from the dataset was removed as these were irrelevant activities that were being performed in between exercises, e.g., moving from one location to another location for another task. This was done to reduce unnecessary noise from our dataset.
To overcome this, I interpolated data, using the interpolate() function, to replace missing points with predicted values according to its surrounding data points. As a result, a total of 1,942,868 rows of clean dataset were left to be analysed.

#### Data splitting
Before performing exploratory data analysis, splitting the dataset into training and testing set is essential to avoid overfitting models. It's also helpful in avoiding biases that arise from preconceptions gained from looking at the data itself. The decision to split the dataset is applicable in this report due to the large sample size it constitutes. The data split ratio used for this report is 50:50. 


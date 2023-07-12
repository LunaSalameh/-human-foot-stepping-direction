# -human-foot-stepping-direction
This project aim to accurately identifying the direction of human foot movements. it start by implementing an IMU-based wearable electronic device. 
Then, different algorithms are designed and compared to recognize five distinct foot motions: jump, step left, step right, step forward, and step backward.

# Description
# Firt Step: Data acquisition
First, an IMU sensor was attached on leg in order to record the foot motion.
Second, A Data Set was built with the help of 9 individuals, each performing the five movements (jump, forward, backward, left, right) three times. This resulted in a total of 135
experiments. Each experiment was recorded over a time window of 2 seconds with a sampling rate of 180 Hz, resulting in 360 time samples for each experiment.
Each time sample consists of a set of measurements, including 3-axis accelerometer data and 3-axis gyroscope data, totaling 12 measurements.

The measurement units allow the user to choose the appropriate sensitivity factor for both the gyroscope and the accelerometer, depending on the application. In our application,
the appropriate measurement ranges for the data were selected as follows: the gyroscope measurement range is ±250 (deg/sec) with a scaling factor of 131, and the accelerometer
measurement range is ±2g (m/s^2) with a scaling factor of 16384. These parameters were chosen to match the expected human movements performed by the individuals, ensuring that they
fall within the specified measurement ranges. Consequently, the data was scaled using the aforementioned factors.

The data was divided into three separate files as follows: The first file contains data from the first sensor (located on the leg), the second file contains data from the second
sensor (located on the foot). The purpose of this division is to train the algorithms on individual sensor data and compare the results to find the best placement.
The third file is a file specific to the final column that determines the type of movement (labels), which are as follows: 
1≡forward,
2≡backward,
3≡left,
4≡right,
5≡jump

# Motion Detection
In an attempt to improve the previous results, the number of experiments was increased to 257 trials. Unwanted signals were eliminated from each time sample by applying a simple
motion detection method.

# Resize
Resegmentation was performed to standardize the length of all time windows after the motion detection process. Each experiment was resampled to have 64 time samples.
Oversampling was applied to the sequences with fewer than 64 samples, while undersampling was applied to the sequences with more than 64 samples.

# Feature Extraction
The following features were extracted from each sequence and for each measurement of the accelerometer and gyroscope:
'mean', 'min', 'max', 'std', 'skew', 'kurtosis', 'entropy', 'max_to_min', 'mean_abs_change', 'mean_change_of_abs_change', 'abs_max', 'abs_min' 'L1-norm'

# Classification
the data was divided into training data and testing data using a 10-fold cross-validation method. The following models were trained:
KNN, SVM, logistic regression, RF, XG_boost

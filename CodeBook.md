**THE MAIN CODES CAN BE FOUND in R-Codes File**

## step 1
Since we need "data.table" and "dplyr" packages, these packages were called.

## step 2
Dataset downloaded and unzipped in "UCI HAR Dataset" folder

## step 3
Readin Data. Since the data is in .txt format, I used read.table.
**features <- features.txt** ( The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals tAcc-XYZ and tGyro-XYZ.)
**activities** ( List of activities )
**subjectTest**  ( test data of 9/30 volunteer's observation)
**xtest** (features test data)
**ytest** (test data of activities' code labels)
**subjectTraint** (train data of 21/30 volunteer's observation)
**xtrain** (features train data)
**ytrain** (train data of activities’code labels)

## step 4
Merging the train and test data sets to create one complete data set
 **X**  (by merging x_train and x_test) (Although there are many ways, but this assignment,rbind() was used)
 **Y**  (by merging y_train and y_test) (rbind() function)
 **Subject** (by merging subject_train and subject_test)  (rbind() function)
 **Merged_Table** (by merging Subject, Y and X) (cbind() function)
 
## step 4
Extracts only the measurements on the mean and standard deviation for each measurement
**TidyTable** (by subsetting Merged_Table, selecting only columns: subject, code and the measurements on the mean and standard deviation (std) for each measurement)

## step 4
Uses descriptive activity names to name the activities in the data set
All code column's numbers of the TidyTable replaced with corresponding activity taken from second column of the  activities variable

## step 5
relabellinf the data set with descriptive variable names

code column in TidyData renamed into Activity

All start with character t in column’s name replaced by Time

All Acc in column’s name replaced by Accelerometer

All Gyro in column’s name replaced by Gyroscope

All start with character f in column’s name replaced by Frequency

All .mean. in column’s name replaced by _Mean_

All .std. in column’s name replaced by _StDeviation_

All Mag in column’s name replaced by Magnitude

All start with character a in column’s name replaced by A

All tBody in column’s name replaced by TimeBody

## step 5
From the data set in previous step, creates a second, independent tidy data set with the average of each variable for each activity and each subject

FinalTable is created by sumarising TidyTable taking the means of each variable for each activity and each subject, after groupped by subject and activity.

Export FinalTable into **FinalTable.txt** file.

Changing to Date Frame

Export FinalTable into **FinalTable.CSV**file.

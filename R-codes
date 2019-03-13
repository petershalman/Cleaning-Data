library(data.table)
library(dplyr)

# Downloading file from the source
fileUrl = 'https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip'
if (!file.exists('./UCI HAR Dataset.zip')){
  download.file(fileUrl,'./UCI HAR Dataset.zip', mode = 'wb')
  unzip("UCI HAR Dataset.zip", exdir = getwd())
}

#READING DATA 
features <- read.table("UCI HAR Dataset/features.txt", col.names = c("n","func"))
activities <- read.table("UCI HAR Dataset/activity_labels.txt", col.names = c("code", "activity"))
subjectTest <- read.table("UCI HAR Dataset/test/subject_test.txt", col.names = "subject")
xtest <- read.table("UCI HAR Dataset/test/X_test.txt", col.names = features$func)
ytest <- read.table("UCI HAR Dataset/test/y_test.txt", col.names = "code")
subjectTrain <- read.table("UCI HAR Dataset/train/subject_train.txt", col.names = "subject")
xtrain <- read.table("UCI HAR Dataset/train/X_train.txt", col.names = features$func)
yrain <- read.table("UCI HAR Dataset/train/y_train.txt", col.names = "code")

#CREATING ONE DATA SET BY MERGING ALL THE DATA.
Y <- rbind(ytrain, ytest)
X <- rbind(xtrain, xtest)
Subject <- rbind(subjectTrain, subjectTest)
Merged_Table <- cbind(Subject, Y, X)

#Extracts only the measurements on the mean and standard deviation for each measurement.
TidyTable <- Merged_Table %>% select(subject, code, contains("mean"), contains("std"))

#Uses descriptive activity names to name the activities in the data set. 
#Since I have not use the type of TidyData$code to Character for doing this section I use the following syntax:
TidyTable$code <- activities[TidyTable$code, 2]
# typeof(TidyTable$code):"integer"

#Appropriately labels the data set with descriptive variable names.
names(TidyTable)[2] = "Activity"
names(TidyTable) <- gsub("^t", "Time", names(TidyTable))
names(TidyTable)<-gsub("Acc", "Accelerometer", names(TidyTable))
names(TidyTable)<-gsub("Gyro", "Gyroscope", names(TidyTable))
names(TidyTable)<-gsub("^f", "Frequency", names(TidyTable))
names(TidyTable) <- gsub(".mean.", "_Mean_", names(TidyTable))
names(TidyTable) <- gsub(".std.", "_StDeviation_", names(TidyTable))
names(TidyTable) <- gsub("Mag", "Magnitude", names(TidyTable))
names(TidyTable) <- gsub("^a", "A", names(TidyTable))
names(TidyTable) <- gsub("tBody", "TimeBody", names(TidyTable))



FinalTable <- TidyTable %>%
    group_by(subject, Activity) %>%
    summarise_all(funs(mean))
   
write.table(FinalTable, "FinalTable.txt", row.name=FALSE)

#save "FinalTable" in CSV format
mac<-as.data.frame(TidyTable)
write.csv(mac, "FinalTable.csv", row.names = FALSE)



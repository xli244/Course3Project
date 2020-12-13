This CodeBook will provide details on how all the variables and summaries calculated, along with units, and any other relevant information.
# Download the raw data
- The raw data is downloaded with this [link](https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip). 
- The folder that contains raw data is called "UCI HAR Dataset". 
# Load the data into RStudio 
- features: "features.txt". Columns are renamed to "serial_n" and "features". There are 561 obs of 2 variables. 
- activity: "activity_labels.txt". Columns are renamed to "code" and "activity". There are 6 obs of 2 variables. 
- subjecttest: "subject_test.txt". The column name is "subject". There are 2947 obs of 1 variable. 
- xtest: "X_test.txt". The column are renamed to indicate the features listed in the "features.txt". There are 2947 obs of 561 variables. 
- ytest:"y_test.txt". The column is named as "code". It is the same code used in the data "activity.txt" to indicate activity type. There are 2947 obs of 1 variable.
- subjecttrain:"subject_train.txt". The column name is "subject". There are 7352 obs of 1 variable. 
- xtrain:"X_train.txt". The column are renamed to indicate the features listed in the "features.txt". There are 7352 obs of 561 variables. 
- ytrain:"y_train.txt".The column is named as "code". It is the same code used in the data "activity.txt" to indicate activity type. There are 7352 obs of 1 variable.
# Merge data 
- Rows of xtest and xtrain are merged in the same dataset called "X". 
- The same method applies to the merged datasets "Y" and "subject". 
- Then, all columns of datasets "X", "Y",and "subject" are merged into data table called "mergedata". The first column is the "subject", the second column shows "Y" value, and the rest of the columns are from "X".  
# Extracts only the measurements on the mean and standard deviation 
- In the data table "mergedata", only columns that contains "mean" and "std" are selected. 
- Note:Because the R function `select` also selects columns that contain "meanFreq" and "angle...mean", and these columns are not the measurements required. The `select` function is used again to exclude "meanFreq" and "angle".
- There are 10299 obs of 68 variables in the "mergedata". 
# Uses descriptive activity names 
- The second column "code" of "mergedata" is matched with the first column "code" of "activity" dataset, and each code is replaced by the corresponding descriptive name. 
# Appropriately labels the data set with descriptive variable names
- In the "mergedata" data table:
- The first column is renamed from "subject" to "Subject", and the second column is renamed from "code" to "Activity_type".
- "t" and "f" that appears in the beginning of the labels are replaced with "Time" and "Frequency",respectively. 
- "Acc" and "Gyro" are replaced with "Accelerometer" and "Gyroscope", respectively.
- "-mean()" and "-std()" are replaced with "Mean" and "STD", respectively.
- Finally, use the `names` function to check all the column names are decriptive and appropriately labeled.  
# Create a tidy data set with the average of each variable for each activity and each subject
- Group "mergedata" by activity and subject, and use `summarise_all` to apply the `mean` to both. 
- The new data is called "todydata".
- There are 30 subjects and 6 types of activities with 66 variables/features. We can confirm this as "tidydata" has 180 rows and 68 columns. 
- The "tidydata" is exported to the "UCI HAR Dataset" as "tidydata.txt". 

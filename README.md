# PROJECT
----------

*The data for this project is collected from  [http://google.com](Human Activity Recognition database) built from the recordings of 30 subjects performing 6 activities of daily living.
In this project we clean this data using R codes.*

#Activites of different exercises are recorded#



```r
activities <- read.table("UCI_HAR_Dataset/activity_labels.txt",sep="",header=FALSE)
colnames(activities) = c("code","name")
print(activities)
```

```
##   code               name
## 1    1            WALKING
## 2    2   WALKING_UPSTAIRS
## 3    3 WALKING_DOWNSTAIRS
## 4    4            SITTING
## 5    5           STANDING
## 6    6             LAYING
```

#features are column names of various measurements


```r
features <- read.table("UCI_HAR_Dataset/features.txt.",sep=" ",header=FALSE)
colnames(features) =c("code","name")
head(features)
```

```
##   code              name
## 1    1 tBodyAcc-mean()-X
## 2    2 tBodyAcc-mean()-Y
## 3    3 tBodyAcc-mean()-Z
## 4    4  tBodyAcc-std()-X
## 5    5  tBodyAcc-std()-Y
## 6    6  tBodyAcc-std()-Z
```

##PREPARING TEST DATA
###subject_test file contains activity ids performed on each person
###x_test contains several columns data of various features
###y_test contains activity ids performed on each person
### Above three files contains same no.of records. First 2 files contains same data

##*subjects*


```r
subjects <- read.table("UCI_HAR_Dataset/test/subject_test.txt",sep=" ",header=FALSE)
colnames(subjects)=c("sub_id")
head(subjects)
```

```
##   sub_id
## 1      2
## 2      2
## 3      2
## 4      2
## 5      2
## 6      2
```


```r
tail(subjects)
```

```
##      sub_id
## 2942     24
## 2943     24
## 2944     24
## 2945     24
## 2946     24
## 2947     24
```

##*act_columns*


```r
activity_columns <- read.table("UCI_HAR_Dataset/test/y_test.txt",sep=" ",header=FALSE)
colnames(activity_columns)=c("act_id")
head(activity_columns)
```

```
##   act_id
## 1      5
## 2      5
## 3      5
## 4      5
## 5      5
## 6      5
```


```r
tail(activity_columns)
```

```
##      act_id
## 2942      2
## 2943      2
## 2944      2
## 2945      2
## 2946      2
## 2947      2
```

##*features_col*


```r
features_columns <- read.table("UCI_HAR_Dataset/test/x_test.txt",sep="",header=FALSE)
colnames(features_columns)=features$name

library(dplyr)
xtest = select( features_columns, contains("std"), contains("Mean"))
```

```
## Error in eval(expr, envir, enclos): found duplicated column name: fBodyAcc-bandsEnergy()-1,8, fBodyAcc-bandsEnergy()-9,16, fBodyAcc-bandsEnergy()-17,24, fBodyAcc-bandsEnergy()-25,32, fBodyAcc-bandsEnergy()-33,40, fBodyAcc-bandsEnergy()-41,48, fBodyAcc-bandsEnergy()-49,56, fBodyAcc-bandsEnergy()-57,64, fBodyAcc-bandsEnergy()-1,16, fBodyAcc-bandsEnergy()-17,32, fBodyAcc-bandsEnergy()-33,48, fBodyAcc-bandsEnergy()-49,64, fBodyAcc-bandsEnergy()-1,24, fBodyAcc-bandsEnergy()-25,48, fBodyAcc-bandsEnergy()-1,8, fBodyAcc-bandsEnergy()-9,16, fBodyAcc-bandsEnergy()-17,24, fBodyAcc-bandsEnergy()-25,32, fBodyAcc-bandsEnergy()-33,40, fBodyAcc-bandsEnergy()-41,48, fBodyAcc-bandsEnergy()-49,56, fBodyAcc-bandsEnergy()-57,64, fBodyAcc-bandsEnergy()-1,16, fBodyAcc-bandsEnergy()-17,32, fBodyAcc-bandsEnergy()-33,48, fBodyAcc-bandsEnergy()-49,64, fBodyAcc-bandsEnergy()-1,24, fBodyAcc-bandsEnergy()-25,48, fBodyAccJerk-bandsEnergy()-1,8, fBodyAccJerk-bandsEnergy()-9,16, fBodyAccJerk-bandsEnergy()-17,24, fBodyAccJerk-bandsEnergy()-25,32, fBodyAccJerk-bandsEnergy()-33,40, fBodyAccJerk-bandsEnergy()-41,48, fBodyAccJerk-bandsEnergy()-49,56, fBodyAccJerk-bandsEnergy()-57,64, fBodyAccJerk-bandsEnergy()-1,16, fBodyAccJerk-bandsEnergy()-17,32, fBodyAccJerk-bandsEnergy()-33,48, fBodyAccJerk-bandsEnergy()-49,64, fBodyAccJerk-bandsEnergy()-1,24, fBodyAccJerk-bandsEnergy()-25,48, fBodyAccJerk-bandsEnergy()-1,8, fBodyAccJerk-bandsEnergy()-9,16, fBodyAccJerk-bandsEnergy()-17,24, fBodyAccJerk-bandsEnergy()-25,32, fBodyAccJerk-bandsEnergy()-33,40, fBodyAccJerk-bandsEnergy()-41,48, fBodyAccJerk-bandsEnergy()-49,56, fBodyAccJerk-bandsEnergy()-57,64, fBodyAccJerk-bandsEnergy()-1,16, fBodyAccJerk-bandsEnergy()-17,32, fBodyAccJerk-bandsEnergy()-33,48, fBodyAccJerk-bandsEnergy()-49,64, fBodyAccJerk-bandsEnergy()-1,24, fBodyAccJerk-bandsEnergy()-25,48, fBodyGyro-bandsEnergy()-1,8, fBodyGyro-bandsEnergy()-9,16, fBodyGyro-bandsEnergy()-17,24, fBodyGyro-bandsEnergy()-25,32, fBodyGyro-bandsEnergy()-33,40, fBodyGyro-bandsEnergy()-41,48, fBodyGyro-bandsEnergy()-49,56, fBodyGyro-bandsEnergy()-57,64, fBodyGyro-bandsEnergy()-1,16, fBodyGyro-bandsEnergy()-17,32, fBodyGyro-bandsEnergy()-33,48, fBodyGyro-bandsEnergy()-49,64, fBodyGyro-bandsEnergy()-1,24, fBodyGyro-bandsEnergy()-25,48, fBodyGyro-bandsEnergy()-1,8, fBodyGyro-bandsEnergy()-9,16, fBodyGyro-bandsEnergy()-17,24, fBodyGyro-bandsEnergy()-25,32, fBodyGyro-bandsEnergy()-33,40, fBodyGyro-bandsEnergy()-41,48, fBodyGyro-bandsEnergy()-49,56, fBodyGyro-bandsEnergy()-57,64, fBodyGyro-bandsEnergy()-1,16, fBodyGyro-bandsEnergy()-17,32, fBodyGyro-bandsEnergy()-33,48, fBodyGyro-bandsEnergy()-49,64, fBodyGyro-bandsEnergy()-1,24, fBodyGyro-bandsEnergy()-25,48
```

```r
head(xtest,1)
```

```
## Error in head(xtest, 1): object 'xtest' not found
```

## Before I start R Program, I obtain these databases and organize in my file

http://archive.ics.uci.edu/ml/machine-learning-databases/00240/UCI%20HAR%20Dataset.zip

## The first thing I do is to obtain all unassembled datasets (y_test.txt, X_test.txt, subject_test.txt, y_train.txt, X_train.txt, and subject_train.txt). 


paste(getwd(), "/Desktop/Assignment4/train/subject_train.txt", sep = "") -> a

paste(getwd(), "/Desktop/Assignment4/train/y_train.txt", sep = "") -> b

paste(getwd(), "/Desktop/Assignment4/train/X_train.txt", sep = "") -> c

read.table(a) -> a

read.table(b) -> b

read.table(c) -> c

paste(getwd(), "/Desktop/Assignment4/test/subject_test.txt", sep = "") -> x

paste(getwd(), "/Desktop/Assignment4/test/y_test.txt", sep = "") -> y

paste(getwd(), "/Desktop/Assignment4/test/X_test.txt", sep = "") -> z

read.table(x) -> x

read.table(y) -> y

read.table(z) -> z


## The next thing I do is to rename y_test.txt, y_train.txt, subject_test.txt, and subject_train.txt from "V1" to "Activities" and "Subject" before I can assemble them because each column must have unique names. Otherwise, the assembled dataset would have double or three times "V1", which is undesired.


library(dplyr)

rename(a, Subject = "V1") -> a

rename(b, Activities = "V1") -> b

rename(x, Subject = "V1") -> x

rename(y, Activities = "V1") -> y


## Then all datasets assemble together into messy dataset


cbind(a, b) -> a

cbind(x, y) -> x

rbind(a, x) -> a

rbind(c, z) -> c

cbind(a, c) -> messy


## The next thing I do is to extract certain columns contained with statistics of either mean or standard derviation.


select(messy, Subject, Activities, c(V1:V6), c(V41:V46), 
       c(V81:V86), c(V121:V126), c(V161:V166), 
       c(V201, V202, V214, V215, V227, V228, V240, V241, V253, V254), 
       c(V266:V271), c(V345:350), c(V424:429), 
       c(V503, V504, V516, V517, V529, V530, V542, V543)) -> cleaner


## The gsub applies to replace 1,2,3,4, & 56 by walking, walking upstairs, walking downstairs, sitting, standing, & laying. Then, each word is unquoted.


gsub(1, "walking", cleaner$Activities) -> cleaner$Activities

gsub(2, "walking upstairs", cleaner$Activities) -> cleaner$Activities

gsub(3, "walking downstairs", cleaner$Activities) -> cleaner$Activities

gsub(4, "sitting", cleaner$Activities) -> cleaner$Activities

gsub(5, "standing", cleaner$Activities) -> cleaner$Activities

gsub(6, "laying", cleaner$Activities) -> cleaner$Activities

gsub('"', '', cleaner$Activities) -> cleaner$Activities


## The next painstaking part is to make each column header descriptive, like over 60 column headers.


rename(cleaner, tBodyAcc_mean.X = "V1") -> cleaner

rename(cleaner, tBodyAcc_mean.Y = "V2") -> cleaner

rename(cleaner, tBodyAcc_mean.Z = "V3") -> cleaner

rename(cleaner, tBodyAcc_std.X = "V4") -> cleaner

rename(cleaner, tBodyAcc_std.Y = "V5") -> cleaner

rename(cleaner, tBodyAcc_std.Z = "V6") -> cleaner

rename(cleaner, tGravityAcc_mean.X = "V41") -> cleaner

rename(cleaner, tGravityAcc_mean.Y = "V42") -> cleaner

rename(cleaner, tGravityAcc_mean.Z = "V43") -> cleaner

rename(cleaner, tGravityAcc_std.X = "V44") -> cleaner

rename(cleaner, tGravityAcc_std.Y = "V45") -> cleaner

rename(cleaner, tGravityAcc_std.Z = "V46") -> cleaner

rename(cleaner, tBodyAccJerk_mean.X = "V81") -> cleaner

rename(cleaner, tBodyAccJerk_mean.Y = "V82") -> cleaner

rename(cleaner, tBodyAccJerk_mean.Z = "V83") -> cleaner

rename(cleaner, tBodyAccJerk_std.X = "V84") -> cleaner

rename(cleaner, tBodyAccJerk_std.Y = "V85") -> cleaner

rename(cleaner, tBodyAccJerk_std.Z = "V86") -> cleaner

rename(cleaner, tBodyGyro_mean.X = "V121") -> cleaner

rename(cleaner, tBodyGyro_mean.Y = "V122") -> cleaner

rename(cleaner, tBodyGyro_mean.Z = "V123") -> cleaner

rename(cleaner, tBodyGyro_std.X = "V124") -> cleaner

rename(cleaner, tBodyGyro_std.Y = "V125") -> cleaner

rename(cleaner, tBodyGyro_std.Z = "V126") -> cleaner

rename(cleaner, tBodyGyroJerk_mean.X = "V161") -> cleaner

rename(cleaner, tBodyGyroJerk_mean.Y = "V162") -> cleaner

rename(cleaner, tBodyGyroJerk_mean.Z = "V163") -> cleaner

rename(cleaner, tBodyGyroJerk_std.X = "V164") -> cleaner

rename(cleaner, tBodyGyroJerk_std.Y = "V165") -> cleaner

rename(cleaner, tBodyGyroJerk_std.Z = "V166") -> cleaner

rename(cleaner, tBodyAccMag_mean = "V201") -> cleaner

rename(cleaner, tBodyAccMag_std = "V202") -> cleaner

rename(cleaner, tGravityAccMag_mean = "V214") -> cleaner

rename(cleaner, tGravityAccMag_std = "V215") -> cleaner

rename(cleaner, tBodyAccJerkMag_mean = "V227") -> cleaner

rename(cleaner, tBodyAccJerkMag_std = "V228") -> cleaner

rename(cleaner, tBodyGyroMag_mean = "V240") -> cleaner

rename(cleaner, tBodyGyroMag_std = "V241") -> cleaner

rename(cleaner, tBodyGyroJerkMag_mean = "V253") -> cleaner

rename(cleaner, tBodyGyroJerkMag_std = "V254") -> cleaner

rename(cleaner, fBodyAcc_mean.X = "V266") -> cleaner

rename(cleaner, fBodyAcc_mean.Y = "V267") -> cleaner

rename(cleaner, fBodyAcc_mean.Z = "V268") -> cleaner

rename(cleaner, fBodyAcc_std.X = "V269") -> cleaner

rename(cleaner, fBodyAcc_std.Y = "V270") -> cleaner

rename(cleaner, fBodyAcc_std.Z = "V271") -> cleaner

rename(cleaner, fBodyAccJerk_mean.X = "V345") -> cleaner

rename(cleaner, fBodyAccJerk_mean.Y = "V346") -> cleaner

rename(cleaner, fBodyAccJerk_mean.Z = "V347") -> cleaner

rename(cleaner, fBodyAccJerk_std.X = "V348") -> cleaner

rename(cleaner, fBodyGyro_mean.X = "V424") -> cleaner

rename(cleaner, fBodyGyro_mean.Y = "V425") -> cleaner

rename(cleaner, fBodyGyro_mean.Z = "V426") -> cleaner

rename(cleaner, fBodyGyro_std.X = "V427") -> cleaner

rename(cleaner, fBodyAccMag_mean = "V503") -> cleaner

rename(cleaner, fBodyAccMag_std = "V504") -> cleaner

rename(cleaner, fBodyBodyAccJerkMag_mean = "V516") -> cleaner

rename(cleaner, fBodyBodyAccJerkMag_std = "V517") -> cleaner

rename(cleaner, fBodyBodyGyroMag_mean = "V529") -> cleaner

rename(cleaner, fBodyBodyGyroMag_std = "V530") -> cleaner

rename(cleaner, fBodyBodyGyroJerkMag_mean = "V542") -> cleaner

rename(cleaner, fBodyBodyGyroJerkMag_std = "V543") -> TidyData



## Finally, I use dplyr summary with mean and write them into cleaned read.table dataset.



CleanData <- TidyData %>%

+     group_by(Subject, Activities) %>%

+     summarise_all(funs(mean))

write.table(CleanData, "CleanData.txt", row.name=FALSE)



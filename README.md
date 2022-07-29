# Getting-and-Cleaning-Data-Course-Project

# The steps (and corresponding code lines) are as follow:  

## 1.Read the data files
df_train <- read.table("train/X_train.txt")
df_test <- read.table("test/X_test.txt")
col_names <- read.table("features.txt")[["V2"]]
df_train_subject_id <- read.table("train/subject_train.txt", 
                                  col.names=c("id_subject"))
df_test_subject_id <- read.table("test/subject_test.txt", 
                                 col.names=c("id_subject"))
df_activity_labels <- read.table("activity_labels.txt", 
                                 col.names=c("id_activity", "activity"))
df_train_activity_id <- read.table("train/y_train.txt", 
                                   col.names=c("id_activity"))
df_test_activity_id <- read.table("test/y_test.txt", col.names=c("id_activity"))


## 2.Merge the training and the test sets to create one data set
df_merged <- rbind(df_train, df_test)


## 3.Appropriately label the data set with descriptive variable names
colnames(df_merged) <- col_names


## 4.Extract only the measurements on the mean and standard deviation for each 
## measurement
col_names_with_mean_or_std <- grep("mean|std", col_names, 
                                   ignore.case=TRUE, value=TRUE)
df_merged_extracted <- df_merged[col_names_with_mean_or_std]


## 5.Insert a column of subjects into the data set to provide information on
## which subject corresponds to which data 
df_merged <- cbind(rbind(df_train_subject_id, df_test_subject_id), df_merged)


## 6.Use descriptive activity names to name the activities in the data set
# 6.1.Insert a column of activity ids into the data set to provide information
# on which activity corresponds to which data
df_merged <- cbind(rbind(df_train_activity_id, df_test_activity_id), df_merged)
# 6.2.Insert a column of corresponding activity names by using merge function
df_merged <- merge(df_activity_labels, df_merged, by="id_activity")


## 7.From the data set, create a second, independent tidy data set
## with the average of each variable for each activity and each subject
# 7.1.Load the library "dplyr"
library(dplyr)
# 7.2.Order the rows by the subject ids; group the obtained table; calculate
# the average values; remove the column of activity ids
average_data_set <- arrange(df_merged, id_subject) %>% 
  group_by(id_subject, activity) %>% 
  summarise_all(mean) %>% select(-id_activity)


## 8.Save the obtained data set
write.csv(average_data_set, "Final_data_set.csv")
write.table(average_data_set, "Final_data_set.txt", sep = " ", row.names=FALSE)

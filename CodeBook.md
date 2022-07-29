Getting-and-Cleaning-Data-Course-Project

The following steps are taken to achieve getting and cleaning data:  

1.Read the data files (more information on the data files can be found in "INFO.txt"):
1.1. "train/X_train.txt";
1.2. "test/X_test.txt";
1.3. "features.txt";
1.4. "train/subject_train.txt";
1.5. "test/subject_test.txt";
1.6. "activity_labels.txt";
1.7. "train/y_train.txt";
1.8. "test/y_test.txt".

2.Merge the training and the test sets to create one data set: df_merged.

3.Appropriately label the data set with descriptive variable names found in "features.txt".

4.Extract only the measurements on the mean and standard deviation for each measurement by finding those columns the names of which contain either "mean" or "std" patterns. The extracted data is assigned as df_merged_extracted.    

5.Insert a column of subjects ids into the data set to provide information on
which subject corresponds to which data.

6.Use descriptive activity names to name the activities in the data set:
6.1.Insert a column of activity ids into the data set to provide information
on which activity corresponds to which data;
6.2.Insert a column of corresponding activity names by using merge function.

7.From the obtained data set, create a second, independent tidy data set
with the average of each variable for each activity and each subject:
7.1.Load the library "dplyr";
7.2.Order the rows by the subject ids; group the obtained table; calculate the average values; remove the column of activity ids. These operations yield the final data set: average_data_set.

8.Save average_data_set as "Final_data_set.csv" and "Final_data_set.txt"

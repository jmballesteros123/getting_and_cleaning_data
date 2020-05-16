# Code Book
generated 2020-05-16 

## Actions performed on data:
* create data dir `./data`
* downloading zip file: [https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip](https://d396qusza40orc.cloudfront.net/getdata%2Fprojectfiles%2FUCI%20HAR%20Dataset.zip) to `./data`
* extracting zip file: `./data/data.zip` to `./data/UCI HAR Dataset`
* merging all *_test.txt and *_train.txt files into one dataset: `mergedData`
* `mergedData` loaded in memory, dimensions: 10299 x 563
* subsetted `mergedData` into `subSetMergedData` keeping only the key columns and features containing `std` or `mean`, dimensions : 10299 x 68
* merged `./data/UCI HAR Dataset/activity_labels.txt` contents with correct `activity_num` column, effectivly appending `activity_name` to `subSetMergedData`, dimensions : 10299 x 69
* melt `subSetMergedData` into `reshapedData`, based on key columns, dimensions : 679734 x 5
* split feature column `variable` into 7 seperate colums (for each sub feature), and added it to `reshapedData`, dimensions : 679734 x 12
* renamed `reshapedData` to **`resultData`**
* cast `resultData` into **`tidyData`** with the average of each variable for each activity and each subject dimensions :180 x 68
* write `tidyData` to file  `./data/tidy_data.txt`

## `resultData` variable

### key columns

Variable name       | Description
--------------------|------------
`subject`           | ID of subject, int (1-30)
`activity_num`      | ID of activity, int (1-6)
`activity_name`     | Label of activity, Factor w/ 6 levels
### non-key columns

Variable name       | Description
--------------------|------------
`variable`          | comlete name of the feature, Factor w/ 66 levels (eg. tBodyAcc-mean()-X) 
`value`             | the actual value, num (range: -1:1)
`dimension`         | dimension of measurement, Factor w/ 2 levels: `t` (Time) or `f` (Frequency)
`source`            | source of measurement, Factor w/ 3 levels: `Body`,`BodyBody` or `Gravity`
`type`              | type of measurement, Factor w/ 2 levels: `Acc` (accelerometer) or `Gyro` (gyroscope)
`jerk`              | is 'Jerk' signal , Factor w/ 2 levels:  `Jerk` or `` (non Jerk)
`magnitude`         | is 'Magnitude' value , Factor w/ 2 levels:  `Mag` or `` (non Mag)
`method`            | result from method , Factor w/ 2 levels:  `mean` (average) or `std` (standard deviation)
`axis`              | FFT exrapolated to axis , Factor w/ 2 levels:  `` (no FFT-axis) or `X`, `Y` or `Z`

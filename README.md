#run_analysis.R
##colnames
a vector of chars that is the name of features in test and train files.<br/><br/>
###calculation:<br/>
```colnames <- c("subject","y",read.table("features.txt",stringsAsFactors=F)[,2])```<br/><br/>
###steps:<br/>
* extract the second column of feature.txt as a vector of characters: ```read.table("features.txt",stringsAsFactors=F)[,2]```<br/>
* append the vector to "subject" and "y": ```c("subject","y",...)```<br/>
* assign the names vector to colnames<br/>

##test
a variable of type data.frame that consists of X(sensor inputs), y(activity code) and the subject(phone wearer) for the test data.<br/><br/>
###calculation:<br/>
```test <- cbind(read.table("test/subject_test.txt"),read.table("test/y_test.txt"),read.table("test/X_test.txt"))```<br/><br/>
###steps:<br/>
* read the subject identifier for each test case: ```read.table("test/subject_test.txt")```<br/>
* read the activity code for each test case: ```read.table("test/y_test.txt")```<br/>
* read the sensor data for each test case: ```read.table("test/X_test.txt")```<br/>
* bind them all and assign them to variable "test": ```cbind(subject,y,X)```

##train
a variable of type data.frame that consists of X(sensor inputs), y(activity code) and the subject(phone wearer) for the train data.<br/><br/>
###calculation:<br/>
```train <- cbind(read.table("train/subject_train.txt"),read.table("train/y_train.txt"),read.table("train/X_train.txt"))```<br/><br/>
###steps:<br/>
* read the subject identifier for each train case: ```read.table("train/subject_train.txt")```<br/>
* read the activity code for each train case: ```read.table("train/y_train.txt")```<br/>
* read the sensor data for each train case: ```read.table("train/X_train.txt")```<br/>
* bind them all and assign them to variable "train": ```cbind(subject,y,X)```

##merged
a variable of type data.frame that consists of all the data from "test" data.frame appended to "train" data.frame.<br/><br/>
###calculation:<br/>
```merged <- rbind.data.frame(train,test);
names(merged) <- colnames```<br/><br/>
###steps:<br/>
* append test rows to train dataset: ```merged <- rbind.data.frame(train,test)```<br/>
* set appropriate names for the dataset: ```names(merged) <- colnames```

##feature_type
a vector of chars that consists of the function name in feature name.
The assumption is that the function, used on the data(e.g. mean()) is seperated from the rest of the test by "-" and is always the 2nd part of the string. which is the case on our data.<br/><br/>
###calculation:<br/>
```feature_type <- sapply(strsplit(colnames,split="-"),function(x){x[2]})```<br/><br/>
###steps:<br/>
* create a function that extracts the 2nd element of a list: ```function(x){x[2]}```<br/>
* split each element on the colnames using the seperator "-": ```strsplit(colnames,split="-")```<br/>
* apply the created functin to the list that we just created and assign the resulting vector to "feature_type": ```feature_type <- sapply(SplitedNames,ExtractionFunction)```
 
##std_mean_elements
a variable of type data.frame that consists of all the data from which have -mean() or -std() in their column name.<br/><br/>
###calculation:<br/>
```std_mean_elements <- merged[,c(1:2,which(feature_type == "mean()" |feature_type == "std()"))]```<br/><br/>
###steps:<br/>
* create a vector of boolean that has a true elements for each column name that contains mean() or std(): ```feature_type == "mean()" |feature_type == "std()"```<br/>
* create a numeric vector that contains the index for each true element: ```which(std_mean_features)```<br/>
* extract the subject, activity and selected columns from "merged" dataset into "std_mean_elements": ```std_mean_elements <- merged[,c(1:2,selected_elements)]```

##activity
a variable of type data.frame that consists of activity labels and their corresponding values.<br/><br/>
###calculation:<br/>
```activity <- read.table("activity_labels.txt",stringsAsFactors=T);
names(activity)<-c("ActivityValue","ActivityLabel")```<br/><br/>
###steps:<br/>
* read "activity_labels.txt" into "activity" dataset: ```activity <- read.table("activity_labels.txt",stringsAsFactors=T)```<br/>
* set appropriate names for the dataset: ```names(activity)<-c("ActivityValue","ActivityLabel")```

##aggregated_data
a mean aggregation of std_mean_elements by subject and activity over all columns.<br/><br/>
###calculation:<br/>
```aggregated_data <- aggregate.data.frame(std_mean_elements,by=list(std_mean_elements$subject,std_mean_elements$y),FUN=mean)```

##cleanData
a data.frame that has activities of type factor instead of integer which is then written to a file.<br/><br/>
###calculation:<br/>
```cleanData <- merge(activity,aggregated_data,by.x="ActivityValue",by.y="y")[,c(-1,-3,-4)];
write.table(cleanData,file="cleanData.txt")```<br/><br/>
###steps:<br/>
* join aggregated_data with activity on activity value: ```merge(activity,aggregated_data,by.x="ActivityValue",by.y="y")```<br/>
* remove the activity value column and the ones created by aggeregation and assign it to "cleanData" dataset: ```cleanData <- merged_aggregated_data[,c(-1,-3,-4)]```<br/>
* write cleanData to the output: ```write.table(cleanData,file="cleanData.txt")```
* 

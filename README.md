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
###steps:<br/>
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
 


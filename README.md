#run_analysis.R
##colnames
a vector of chars that is the name of features in test and train files.<br/><br/>
calculation:<br/>```colnames <- c("subject","y",read.table("features.txt",stringsAsFactors=F)[,2])```<br/><br/>
steps:<ol>
<li>extract the second column of feature.txt as a vector of characters: read.table("features.txt",stringsAsFactors=F)[,2]
<li>append the vector to "subject" and "y": c("subject","y",...)
<li>assign the names vector to colnames
</ol>
##test
a variable of type data.frame that consists of X(sensor inputs), y(activity code) and the subject(phone wearer) for the test data.<br/><br/>
calculation:<br/>```test <- cbind(read.table("test/subject_test.txt"),read.table("test/y_test.txt"),read.table("test/X_test.txt"))```<br/><br/>
steps:<ol>
<li>read the subject identifier for each test case: read.table("test/subject_test.txt")
<li>read the activity code for each test case: read.table("test/y_test.txt")
<li>read the sensor data for each test case: read.table("test/X_test.txt")
<li>bind them all and assign them to variable "test": cbind(subject,y,X)
</ol>
##train
a variable of type data.frame that consists of X(sensor inputs), y(activity code) and the subject(phone wearer) for the train data.<br/><br/>
calculation:<br/>```train <- cbind(read.table("train/subject_train.txt"),read.table("train/y_train.txt"),read.table("train/X_train.txt"))```<br/><br/>
steps:<ol>
<li>read the subject identifier for each train case: read.table("train/subject_train.txt")
<li>read the activity code for each train case: read.table("train/y_train.txt")
<li>read the sensor data for each train case: read.table("train/X_train.txt")
<li>bind them all and assign them to variable "train": cbind(subject,y,X)
</ol>

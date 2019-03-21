
# datasets 
# sim_Gail_Random sim_Gail_signal sim_Gail_signal_add_NA imputed1

#1 sim_Gail_Random
# ada
# Model-free analysis, classification
library("crossval")
library("ada")
require(crossval)
require(ada)
#set up adaboosting prediction function

# Define a new classification result-reporting function
my.ada <- function (train.x, train.y, test.x, test.y, negative, formula){
  ada.fit <- ada(train.x, train.y)
  predict.y <- predict(ada.fit, test.x)
  #count TP, FP, TN, FN, Accuracy, etc.
  out <- confusionMatrix(test.y, predict.y, negative = negative)
  # negative  is the label of a negative "null" sample (default: "control").
  return (out)
  return (predict.y)
}

# remove unrelated variables ! 
#sim_Gail_Random$BrCa <- ifelse(sim_Gail_Random$Case_Random==0,0,1) 
colnames(sim_Gail_Random)
input <- sim_Gail_Random[ ,-which(names(sim_Gail_Random) %in% c("Case_Random","ID","T2"))]
output <- as.factor(sim_Gail_Random$Case_Random)
c(dim(input), dim(output))

# using sim_Gail_Random data:
X <- as.data.frame(input); Y <- output
neg <- "1"   # "Control" == "1"

# Side note: There is a function name collision for "crossval", the same method is present in 
# the "mlr" (machine Learning in R) package and in the "crossval" package.  
# To specify a function call from a specific package do:  packagename::functionname()

set.seed(115) 

cv.out <- crossval::crossval(my.ada, X, Y, K = 5, B = 2, negative = neg)
# the label of a negative "null" sample (default: "control")

out <- diagnosticErrors(cv.out$stat) 
print(cv.out$stat)
#FP    TP    TN    FN 
#58.1 59.1 62.5 60.3 
print(out)
##acc      sens      spec       ppv       npv       lor 
##0.50666667 0.49497487 0.51824212 0.50426621 0.50895765 0.05289971  




# Logistic 
X =as.matrix(input)    # Predictor variables
Y =as.matrix(output) 
lm.logit <- glm(as.numeric(Y) ~ ., data = as.data.frame(X), family = "binomial")
ynew <- predict(lm.logit, as.data.frame(X)); #plot(ynew)
ynew2 <- ifelse(exp(ynew)<median(exp(ynew)), 0, 1); # plot(ynew2)

predfun.logit = function(train.x, train.y, test.x, test.y, neg)
{   lm.logit <- glm(train.y ~ ., data = train.x, family = "binomial")
ynew = predict(lm.logit, test.x )
# compute TP, FP, TN, FN
ynew2 <- ifelse(exp(ynew)<median(exp(ynew)), 0, 1)
out = confusionMatrix(test.y, ynew2, negative=neg)  # Binary outcome, we can use confusionMatrix
return( out )
}

cv.out.logit = crossval::crossval(predfun.logit, as.data.frame(X), as.numeric(Y), K=5, B=2, neg="1")
cv.out.logit$stat.cv
print(cv.out.logit$stat)
#FP    TP    TN    FN 
#58.7  61.3   61.9 58.1 
diagnosticErrors(cv.out.logit$stat)
#acc      sens      spec       ppv       npv       lor 
#0.5133333 0.5134003 0.5132670 0.5108333 0.5158333 0.1066946


#KNN qda lda

library("class")

X <- as.data.frame(input); Y <- output
predfun.knn =function(train.x, train.y, test.x, test.y, neg)
{
  require("class")
  knn.fit =knn(train.x, test.x, cl =train.y, prob=T)  # knn is already a prediction function!!!
  # ynew = predict(knn.fit, test.x)$class           # no need of another prediction, in this case
  out.knn =confusionMatrix(test.y, knn.fit, negative=neg)
  return( out.knn )
}   

predfun.qda = function(train.x, train.y, test.x, test.y, negative)
{
  require("MASS") # for lda function
  qda.fit = qda(train.x, grouping=train.y)
  ynew = predict(qda.fit,test.x)$class
  out.qda = confusionMatrix(test.y, ynew, negative=negative)
  return( out.qda )
}  


predfun.lda = function(train.x, train.y, test.x, test.y, neg)
{
  require("MASS")
  lda.fit = lda(train.x, grouping=train.y)
  ynew = predict(lda.fit, test.x)$class
  out.lda = confusionMatrix(test.y, ynew, negative=neg)
  return( out.lda )
}


predfun.logit = function(train.x, train.y, test.x, test.y, neg)
{   lm.logit <- glm(train.y ~ ., data = train.x, family = "binomial")
ynew = predict(lm.logit, test.x )
# compute TP, FP, TN, FN
ynew2 <- ifelse(exp(ynew)<median(exp(ynew)), 0, 1)
out = confusionMatrix(test.y, ynew2, negative=neg)  # Binary outcome, we can use confusionMatrix
return( out )
}

predfun.lm =function(train.x, train.y, test.x, test.y)
{     lm.fit =lm(train.y ~. , data=train.x)
ynew =predict(lm.fit, test.x )
# compute squared error risk (MSE)

out =mean( (ynew -test.y)^2)
# note that, in general, when fitting linear model to continuous outcome variable (Y),
# we cant use the out<-confusionMatrix(test.y, ynew, negative=negative), as it requires a binary outcome
# this is why we use the MSE as an estimate of the discrepancy between observed & predicted values
return(out)
}



cv.out.lm =crossval::crossval(predfun.lm, as.data.frame(X), as.numeric(Y), K=5, B=20) #c(cv.out.lm$stat, cv.out.lm$stat.se) 
cv.out.knn =crossval::crossval(predfun.knn, X, Y, K=5, B=2, neg="1")
cv.out.qda = crossval::crossval(predfun.qda, as.data.frame(X), as.factor(Y), K=5, B=2, neg="1")
cv.out.lda = crossval::crossval(predfun.lda, X, Y, K=5, B=2, neg="1")


cv.out.lm
#$stat
#0.2514864
#$stat.se
#0.0003619022
actuals_preds <- data.frame(cbind(actuals=sim_Gail_Random$Case_Random, predicteds=ynew))
correlation_accuracy.lm <- cor(actuals_preds)
#COR
#22.45

print(cv.out.qda$stat)
#  FP   TP   TN   FN 
#33.4 36.0 87.2 83.4 

print(cv.out.knn$stat)
#  FP   TP   TN   FN 
#58.3 59.0 62.3 60.4 

print(cv.out.lda$stat)
#  FP   TP   TN   FN 
#55.0 50.6 65.6 68.8 

diagnosticErrors(cv.out.lm$stat)
#   acc   sens   spec    ppv    npv    lor 
#0.5025 1.0000 0.0000 0.5025    NaN    NaN 

diagnosticErrors(cv.out.lda$stat)
#       acc       sens       spec        ppv        npv        lor 
# 0.4841667  0.4237856  0.5439469  0.4791667  0.4880952 -0.1310097
diagnosticErrors(cv.out.qda$stat)
#      acc      sens      spec       ppv       npv       lor 
#0.5133333 0.3015075 0.7230514 0.5187320 0.5111372 0.1195191 
diagnosticErrors(cv.out.knn$stat)
#       acc       sens       spec        ppv        npv        lor 
#0.50541667 0.49413735 0.51658375 0.50298380 0.50774246 0.04290767

# random forest
library(randomForest)
require(randomForest)
library(caret)

rf_randoms<-sim_Gail_Random
rf_randoms$Case_Random <- as.factor(rf_randoms$Case_Random)
rf.mdl <- randomForest(rf_randoms[,1:9], rf_randoms[,"Case_Random"], ntree=501)
rf.cv <- rfcv( rf_randoms[,1:9], rf_randoms[,"Case_Random"], cv.fold = 3)
#with(rf.cv, plot(n.var, error.cv, type="b", col="red"))
#rf.cv$error.cv
#confussion.rf<-confusionMatrix(rf.cv$predicted, rf_randoms$Case_Random)
#confussion.rf
rf_random_AUC <- rf.mdl$confusion # (256+346)/1200


#2 sim_Gail_signal
# Define a new classification result-reporting function
detach("package:caret", unload=TRUE)
# remove unrelated variables ! 
#sim_Gail_signal$BrCa <- ifelse(sim_Gail_signal$Case_signalYN==0,0,1) 
colnames(sim_Gail_signal)
input <- sim_Gail_signal[ ,-which(names(sim_Gail_signal) %in% c("Case_signalYN","ID","T2"))]
output <- as.factor(sim_Gail_signal$Case_signalYN)
c(dim(input), dim(output))

# using sim_Gail_signal data:
X <- as.data.frame(input); Y <- output
neg <- "1"   # "Control" == "1"

# Side note: There is a function name collision for "crossval", the same method is present in 
# the "mlr" (machine Learning in R) package and in the "crossval" package.  
# To specify a function call from a specific package do:  packagename::functionname()

set.seed(115) 

cv.out <- crossval::crossval(my.ada, X, Y, K = 5, B = 2, negative = neg)
# the label of a negative "null" sample (default: "control")

out <- diagnosticErrors(cv.out$stat) 
print(cv.out$stat)
#FP    TP    TN    FN 
#59.0 113.2 109.8   8.0 
print(out)
##acc      sens      spec       ppv       npv       lor 
##0.9291667 0.9339934 0.9242424 0.9263502 0.9320883 5.1511506  




# Logistic 
X =as.matrix(input)    # Predictor variables
Y =as.matrix(output) 
lm.logit <- glm(as.numeric(Y) ~ ., data = as.data.frame(X), family = "binomial")
ynew <- predict(lm.logit, as.data.frame(X)); #plot(ynew)
ynew2 <- ifelse(exp(ynew)<median(exp(ynew)), 0, 1); # plot(ynew2)

predfun.logit = function(train.x, train.y, test.x, test.y, neg)
{   lm.logit <- glm(train.y ~ ., data = train.x, family = "binomial")
ynew = predict(lm.logit, test.x )
# compute TP, FP, TN, FN
ynew2 <- ifelse(exp(ynew)<median(exp(ynew)), 0, 1)
out = confusionMatrix(test.y, ynew2, negative=neg)  # Binary outcome, we can use confusionMatrix
return( out )
}

cv.out.logit = crossval::crossval(predfun.logit, as.data.frame(X), as.numeric(Y), K=5, B=2, neg="1")
cv.out.logit$stat.cv
print(cv.out.logit$stat)
#FP    TP    TN    FN 
#6.4 113.6 112.4   7.6 
diagnosticErrors(cv.out.logit$stat)
#acc      sens      spec       ppv       npv       lor 
#0.9416667 0.9372937 0.9461279 0.9466667 0.9366667 5.5703012


#KNN qda lda

library("class")

X <- as.data.frame(input); Y <- output
predfun.knn =function(train.x, train.y, test.x, test.y, neg)
{
  require("class")
  knn.fit =knn(train.x, test.x, cl =train.y, prob=T)  # knn is already a prediction function!!!
  # ynew = predict(knn.fit, test.x)$class           # no need of another prediction, in this case
  out.knn =confusionMatrix(test.y, knn.fit, negative=neg)
  return( out.knn )
}   

predfun.qda = function(train.x, train.y, test.x, test.y, negative)
{
  require("MASS") # for lda function
  qda.fit = qda(train.x, grouping=train.y)
  ynew = predict(qda.fit,test.x)$class
  out.qda = confusionMatrix(test.y, ynew, negative=negative)
  return( out.qda )
}  


predfun.lda = function(train.x, train.y, test.x, test.y, neg)
{
  require("MASS")
  lda.fit = lda(train.x, grouping=train.y)
  ynew = predict(lda.fit, test.x)$class
  out.lda = confusionMatrix(test.y, ynew, negative=neg)
  return( out.lda )
}


predfun.lm =function(train.x, train.y, test.x, test.y)
{     lm.fit =lm(train.y ~. , data=train.x)
ynew =predict(lm.fit, test.x )
# compute squared error risk (MSE)
out =mean( (ynew -test.y)^2)

#out.lda = confusionMatrix(test.y, ynew, negative=neg)
#out =mean( (ynew -test.y)^2)  out = confusionMatrix(test.y, ynew, negative=neg)
# note that, in general, when fitting linear model to continuous outcome variable (Y),
# we can???t use the out<-confusionMatrix(test.y, ynew, negative=negative), as it requires a binary outcome
# this is why we use the MSE as an estimate of the discrepancy between observed & predicted values
return(out)
}



cv.out.lm =crossval::crossval(predfun.lm, as.data.frame(X), as.numeric(Y), K=5, B=20) #c(cv.out.lm$stat, cv.out.lm$stat.se) 
cv.out.lm
#$stat
#0.09686989
#$stat.se
#0.0006307684

actuals_preds <- data.frame(cbind(actuals=sim_Gail_signal$Case_signalYN, predicteds=ynew))
correlation_accuracy.lm <- cor(actuals_preds)

cv.out.knn =crossval::crossval(predfun.knn, X, Y, K=5, B=2, neg="1")
cv.out.qda = crossval::crossval(predfun.qda, as.data.frame(X), as.factor(Y), K=5, B=2, neg="1")
cv.out.lda = crossval::crossval(predfun.lda, X, Y, K=5, B=2, neg="1")





print(cv.out.qda$stat)
#  FP   TP   TN   FN 
#8.7 110.4 110.1  10.8 

print(cv.out.knn$stat)
#  FP   TP   TN   FN 
#10.4 110.6 108.4  10.6 

print(cv.out.lda$stat)
#  FP   TP   TN   FN 
#6.5 111.2 112.3  10.0  


diagnosticErrors(cv.out.lda$stat)
#       acc       sens       spec        ppv        npv        lor 
# 0.9312500 0.9174917 0.9452862 0.9447749 0.9182339 5.2581170
diagnosticErrors(cv.out.qda$stat)
#      acc      sens      spec       ppv       npv       lor 
#0.9187500 0.9108911 0.9267677 0.9269521 0.9106700 4.8626300  
diagnosticErrors(cv.out.knn$stat)
#       acc       sens       spec        ppv        npv        lor 
#0.9125000 0.9125413 0.9124579 0.9140496 0.9109244 4.6890884

# random forest
library(randomForest)
require(randomForest)
library(caret)

rf_randoms<-sim_Gail_signal
rf_randoms$Case_signalYN <- as.factor(rf_randoms$Case_signalYN)
rf.mdl <- randomForest(rf_randoms[,1:9], rf_randoms[,"Case_signalYN"], ntree=501)
rf.cv <- rfcv( rf_randoms[,1:9], rf_randoms[,"Case_signalYN"], cv.fold = 3)
#with(rf.cv, plot(n.var, error.cv, type="b", col="red"))
#rf.cv$error.cv
#confussion.rf<-confusionMatrix(rf.cv$predicted, rf_randoms$Case_signalYN)
#confussion.rf
rf_random_AUC <- rf.mdl$confusion # (256+346)/1200

#3 sim_Gail_signal_add_NA
```{r cars}
detach("package:caret", unload=TRUE)
# Define a new classification result-reporting function

# remove unrelated variables ! 
#sim_Gail_signal_add_NA$BrCa <- ifelse(sim_Gail_signal_add_NA$Case_signalYN==0,0,1) 
colnames(sim_Gail_signal_add_NA)
input <- sim_Gail_signal_add_NA[ ,-which(names(sim_Gail_signal_add_NA) %in% c("Case_signalYN","ID","T2"))]
output <- as.factor(sim_Gail_signal_add_NA$Case_signalYN)
c(dim(input), dim(output))

# using sim_Gail_signal_add_NA data:
X <- as.data.frame(input); Y <- output
neg <- "1"   # "Control" == "1"

# Side note: There is a function name collision for "crossval", the same method is present in 
# the "mlr" (machine Learning in R) package and in the "crossval" package.  
# To specify a function call from a specific package do:  packagename::functionname()

set.seed(115) 

cv.out <- crossval::crossval(my.ada, X, Y, K = 5, B = 2, negative = neg)
# the label of a negative "null" sample (default: "control")

out <- diagnosticErrors(cv.out$stat) 
print(cv.out$stat)
#FP    TP    TN    FN 
#9.1 112.5 109.7   8.7 
print(out)
##acc      sens      spec       ppv       npv       lor 
##0.9258333 0.9282178 0.9234007 0.9251645 0.9265203 5.0491051 




# Logistic 
X =as.matrix(input)    # Predictor variables
Y =as.matrix(output) 
lm.logit <- glm(as.numeric(Y) ~ ., data = as.data.frame(X), family = "binomial")
ynew <- predict(lm.logit, as.data.frame(X)); #plot(ynew)
ynew2 <- ifelse(exp(ynew)<median(exp(ynew)), 0, 1); # plot(ynew2)

predfun.logit = function(train.x, train.y, test.x, test.y, neg)
{   lm.logit <- glm(train.y ~ ., data = train.x, family = "binomial")
ynew = predict(lm.logit, test.x )
# compute TP, FP, TN, FN
ynew2 <- ifelse(exp(ynew)<median(exp(ynew)), 0, 1)
out = confusionMatrix(test.y, ynew2, negative=neg)  # Binary outcome, we can use confusionMatrix
return( out )
}

cv.out.logit = crossval::crossval(predfun.logit, as.data.frame(X), as.numeric(Y), K=5, B=2, neg="1")
cv.out.logit$stat.cv
print(cv.out.logit$stat)
#FP    TP    TN    FN 
#8.8 111.2 110.0  10.0
diagnosticErrors(cv.out.logit$stat)
#acc      sens      spec       ppv       npv       lor 
#0.9216667 0.9174917 0.9259259 0.9266667 0.9166667 4.9344739 


#KNN qda lda

library("class")

X <- as.data.frame(input); Y <- output
predfun.knn =function(train.x, train.y, test.x, test.y, neg)
{
  require("class")
  knn.fit =knn(train.x, test.x, cl =train.y, prob=T)  # knn is already a prediction function!!!
  # ynew = predict(knn.fit, test.x)$class           # no need of another prediction, in this case
  out.knn =confusionMatrix(test.y, knn.fit, negative=neg)
  return( out.knn )
}   

predfun.qda = function(train.x, train.y, test.x, test.y, negative)
{
  require("MASS") # for lda function
  qda.fit = qda(train.x, grouping=train.y)
  ynew = predict(qda.fit,test.x)$class
  out.qda = confusionMatrix(test.y, ynew, negative=negative)
  return( out.qda )
}  


predfun.lda = function(train.x, train.y, test.x, test.y, neg)
{
  require("MASS")
  lda.fit = lda(train.x, grouping=train.y)
  ynew = predict(lda.fit, test.x)$class
  out.lda = confusionMatrix(test.y, ynew, negative=neg)
  return( out.lda )
}


predfun.lm =function(train.x, train.y, test.x, test.y)
{     lm.fit =lm(train.y ~. , data=train.x)
ynew =predict(lm.fit, test.x )
# compute squared error risk (MSE)
out =mean( (ynew -test.y)^2)

#out.lda = confusionMatrix(test.y, ynew, negative=neg)
#out =mean( (ynew -test.y)^2)  out = confusionMatrix(test.y, ynew, negative=neg)
# note that, in general, when fitting linear model to continuous outcome variable (Y),
# we can???t use the out<-confusionMatrix(test.y, ynew, negative=negative), as it requires a binary outcome
# this is why we use the MSE as an estimate of the discrepancy between observed & predicted values
return(out)
}



cv.out.lm =crossval::crossval(predfun.lm, as.data.frame(X), as.numeric(Y), K=5, B=20) #c(cv.out.lm$stat, cv.out.lm$stat.se) 
cv.out.lm
#$stat
#0.09894719
#$stat.se
#0.0006247335

actuals_preds <- data.frame(cbind(actuals=sim_Gail_signal_add_NA$Case_signalYN, predicteds=ynew))
correlation_accuracy.lm <- cor(actuals_preds) # 0.7807

cv.out.knn =crossval::crossval(predfun.knn, X, Y, K=5, B=2, neg="1")
cv.out.qda = crossval::crossval(predfun.qda, as.data.frame(X), as.factor(Y), K=5, B=2, neg="1")
cv.out.lda = crossval::crossval(predfun.lda, X, Y, K=5, B=2, neg="1")





print(cv.out.qda$stat)
#  FP   TP   TN   FN 
#11.0 110.7 107.8  10.5  

print(cv.out.knn$stat)
#  FP   TP   TN   FN 
# 12.0 109.5 106.8  11.7

print(cv.out.lda$stat)
#  FP   TP   TN   FN 
#7.4 109.7 111.4  11.5 


diagnosticErrors(cv.out.lda$stat)
#       acc       sens       spec        ppv        npv        lor 
# 0.9212500 0.9051155 0.9377104 0.9368061 0.9064280 4.9670497 
diagnosticErrors(cv.out.qda$stat)
#      acc      sens      spec       ppv       npv       lor 
#0.9104167 0.9133663 0.9074074 0.9096138 0.9112426 4.6378310 
diagnosticErrors(cv.out.knn$stat)
#       acc       sens       spec        ppv        npv        lor 
#0.9012500 0.9034653 0.8989899 0.9012346 0.9012658 4.4223870

# random forest
library(randomForest)
require(randomForest)
library(caret)

rf_randoms<-sim_Gail_signal_add_NA
rf_randoms$Case_signalYN <- as.factor(rf_randoms$Case_signalYN)
rf.mdl <- randomForest(rf_randoms[,1:9], rf_randoms[,"Case_signalYN"], ntree=501)
rf.cv <- rfcv( rf_randoms[,1:9], rf_randoms[,"Case_signalYN"], cv.fold = 3)
#with(rf.cv, plot(n.var, error.cv, type="b", col="red"))
#rf.cv$error.cv
#confussion.rf<-confusionMatrix(rf.cv$predicted, rf_randoms$Case_signalYN)
#confussion.rf
rf_random_AUC <- rf.mdl$confusion # (570+543)/1200=0.9275

#imputed1
```{r cars}

# Define a new classification result-reporting function
detach("package:caret", unload=TRUE)
# remove unrelated variables ! 
#imputed1$BrCa <- ifelse(imputed1$Case_signalYN==0,0,1) 
colnames(imputed1)
input <- imputed1[ ,-which(names(imputed1) %in% c("Case_signalYN","ID","T2"))]
output <- as.factor(imputed1$Case_signalYN)
c(dim(input), dim(output))

# using imputed1 data:
X <- as.data.frame(input); Y <- output
neg <- "1"   # "Control" == "1"

# Side note: There is a function name collision for "crossval", the same method is present in 
# the "mlr" (machine Learning in R) package and in the "crossval" package.  
# To specify a function call from a specific package do:  packagename::functionname()


set.seed(115) 

cv.out <- crossval::crossval(my.ada, X, Y, K = 5, B = 2, negative = neg)
# the label of a negative "null" sample (default: "control")

out <- diagnosticErrors(cv.out$stat) 
print(cv.out$stat)
#FP    TP    TN    FN 
#10.1 112.4 108.7   8.8 
print(out)
##acc      sens      spec       ppv       npv       lor 
##0.9212500 0.9273927 0.9149832 0.9175510 0.9251064 4.9233686 




# Logistic 
X =as.matrix(input)    # Predictor variables
Y =as.matrix(output) 
lm.logit <- glm(as.numeric(Y) ~ ., data = as.data.frame(X), family = "binomial")
ynew <- predict(lm.logit, as.data.frame(X)); #plot(ynew)
ynew2 <- ifelse(exp(ynew)<median(exp(ynew)), 0, 1); # plot(ynew2)

predfun.logit = function(train.x, train.y, test.x, test.y, neg)
{   lm.logit <- glm(train.y ~ ., data = train.x, family = "binomial")
ynew = predict(lm.logit, test.x )
# compute TP, FP, TN, FN
ynew2 <- ifelse(exp(ynew)<median(exp(ynew)), 0, 1)
out = confusionMatrix(test.y, ynew2, negative=neg)  # Binary outcome, we can use confusionMatrix
return( out )
}

cv.out.logit = crossval::crossval(predfun.logit, as.data.frame(X), as.numeric(Y), K=5, B=2, neg="1")
cv.out.logit$stat.cv
print(cv.out.logit$stat)
#FP    TP    TN    FN 
#7.8 112.2 111.0   9.0
diagnosticErrors(cv.out.logit$stat)
#acc      sens      spec       ppv       npv       lor 
#0.9300000 0.9257426 0.9343434 0.9350000 0.9250000 5.1784649  


#KNN qda lda

library("class")

X <- as.data.frame(input); Y <- output
predfun.knn =function(train.x, train.y, test.x, test.y, neg)
{
  require("class")
  knn.fit =knn(train.x, test.x, cl =train.y, prob=T)  # knn is already a prediction function!!!
  # ynew = predict(knn.fit, test.x)$class           # no need of another prediction, in this case
  out.knn =confusionMatrix(test.y, knn.fit, negative=neg)
  return( out.knn )
}   

predfun.qda = function(train.x, train.y, test.x, test.y, negative)
{
  require("MASS") # for lda function
  qda.fit = qda(train.x, grouping=train.y)
  ynew = predict(qda.fit,test.x)$class
  out.qda = confusionMatrix(test.y, ynew, negative=negative)
  return( out.qda )
}  


predfun.lda = function(train.x, train.y, test.x, test.y, neg)
{
  require("MASS")
  lda.fit = lda(train.x, grouping=train.y)
  ynew = predict(lda.fit, test.x)$class
  out.lda = confusionMatrix(test.y, ynew, negative=neg)
  return( out.lda )
}


predfun.lm =function(train.x, train.y, test.x, test.y)
{     lm.fit =lm(train.y ~. , data=train.x)
ynew =predict(lm.fit, test.x )
# compute squared error risk (MSE)
out =mean( (ynew -test.y)^2)

#out.lda = confusionMatrix(test.y, ynew, negative=neg)
#out =mean( (ynew -test.y)^2)  out = confusionMatrix(test.y, ynew, negative=neg)
# note that, in general, when fitting linear model to continuous outcome variable (Y),
# we can???t use the out<-confusionMatrix(test.y, ynew, negative=negative), as it requires a binary outcome
# this is why we use the MSE as an estimate of the discrepancy between observed & predicted values
return(out)
}



cv.out.lm =crossval::crossval(predfun.lm, as.data.frame(X), as.numeric(Y), K=5, B=20) #c(cv.out.lm$stat, cv.out.lm$stat.se) 
cv.out.lm
#$stat
#0.09838956
#$stat.se
#0.0006133364

actuals_preds <- data.frame(cbind(actuals=imputed1$Case_signalYN, predicteds=ynew))
correlation_accuracy.lm <- cor(actuals_preds) # 0.7823658

cv.out.knn =crossval::crossval(predfun.knn, X, Y, K=10, B=20, neg="1")
cv.out.qda = crossval::crossval(predfun.qda, as.data.frame(X), as.factor(Y), K=10, B=20, neg="1")
cv.out.lda = crossval::crossval(predfun.lda, X, Y, K=10, B=20, neg="1")





print(cv.out.qda$stat)
#  FP   TP   TN   FN 
#10.8 110.9 108.0  10.3   

print(cv.out.knn$stat)
#  FP   TP   TN   FN 
# 11.9 110.5 106.9  10.7

print(cv.out.lda$stat)
#  FP   TP   TN   FN 
#7.6 111.4 111.2   9.8 


diagnosticErrors(cv.out.lda$stat)
diagnosticErrors(cv.out.lda$stat.se)
#       acc       sens       spec        ppv        npv        lor 
# 0.9275000 0.9191419 0.9360269 0.9361345 0.9190083 5.1139271 
diagnosticErrors(cv.out.qda$stat)
#      acc      sens      spec       ppv       npv       lor 
#0.9120833 0.9150165 0.9090909 0.9112572 0.9129332 4.6790701  
diagnosticErrors(cv.out.knn$stat)
#       acc       sens       spec        ppv        npv        lor 
#0.9058333 0.9117162 0.8998316 0.9027778 0.9090136 4.5301272 

# random forest
library(randomForest)
require(randomForest)
library(caret)

rf_randoms<-imputed1
rf_randoms$Case_signalYN <- as.factor(rf_randoms$Case_signalYN)
rf.mdl <- randomForest(rf_randoms[,1:9], rf_randoms[,"Case_signalYN"], ntree=501)
rf.cv <- rfcv( rf_randoms[,1:9], rf_randoms[,"Case_signalYN"], cv.fold = 3)
#with(rf.cv, plot(n.var, error.cv, type="b", col="red"))
#rf.cv$error.cv
#confussion.rf<-confusionMatrix(rf.cv$predicted, rf_randoms$Case_signalYN)
#confussion.rf
rf_random_AUC <- rf.mdl$confusion # (563+537)/1200=0.9166667


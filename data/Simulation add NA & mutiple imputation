# add random missing in Simulated data with signal
library(missForest)
sim_Gail_signal_add_NA<-sim_Gail_signal
colnames(sim_Gail_signal_add_NA)
addna<-prodNA(sim_Gail_signal_add_NA[ , c(4:8)], noNA = 0.2)
sim_Gail_signal_add_NA<-cbind(sim_Gail_signal_add_NA[ , c(1:3)],addna,sim_Gail_signal_add_NA[ , c(9:10)])
sim_Gail_signal_add_NA$N_Biop[is.na(sim_Gail_signal_add_NA$N_Biop)] <- 0
sim_Gail_signal_add_NA$HypPlas[is.na(sim_Gail_signal_add_NA$HypPlas)] <- 99
sim_Gail_signal_add_NA$AgeMen[is.na(sim_Gail_signal_add_NA$AgeMen)] <- 99
sim_Gail_signal_add_NA$Age1st[is.na(sim_Gail_signal_add_NA$Age1st)] <- 99
sim_Gail_signal_add_NA$N_Rels[is.na(sim_Gail_signal_add_NA$N_Rels)] <- 99
sim_Gail_signal_add_NA$HypPlas<-ifelse(sim_Gail_signal_add_NA$N_Biop==0,99,sim_Gail_signal_add_NA$HypPlas)
sim_Gail_signal_add_NA$HypPlas<-ifelse(sim_Gail_signal_add_NA$N_Biop==99,99,sim_Gail_signal_add_NA$HypPlas)
str(sim_Gail_signal_add_NA)
table(sim_Gail_signal_add_NA$HypPlas)

#Multiple imputation

library(glmnet)
library(mi)
set.seed(1104)
sim_Gail_signal_imputed<-sim_Gail_signal_add_NA
sim_Gail_signal_imputed$N_Biop[sim_Gail_signal_imputed$N_Biop==99] <- NA
sim_Gail_signal_imputed$AgeMen[sim_Gail_signal_imputed$AgeMen==99] <- NA
sim_Gail_signal_imputed$Age1st[sim_Gail_signal_imputed$Age1st==99] <- NA
sim_Gail_signal_imputed$N_Rels[sim_Gail_signal_imputed$N_Rels==99] <- NA
str(sim_Gail_signal_imputed)



## Impute missing with 4 imputed data sets

mdf <- missing_data.frame(sim_Gail_signal_imputed)
str(sim_Gail_signal_imputed)
raw.im <- mi(mdf, n.iter=6, n.chains=4, seed=13423)
raw.complete <- complete(raw.im)
raw.complete$`chain:1`
imputed1<-raw.complete$`chain:1`[1:10]
imputed2<-raw.complete$`chain:2`[1:10]
imputed3<-raw.complete$`chain:3`[1:10]
imputed4<-raw.complete$`chain:4`[1:10]
str(imputed1)

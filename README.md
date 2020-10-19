# CDS490-Project

dataset :  https://www.kaggle.com/currie32/crimes-in-chicago?select=Chicago_Crimes_2012_to_2017.csv



## CODE FOR PROJECT : still working on editing a few things to my code as its not fully complete
# there are also things i need to add as I am trying to debug and add new modifications to my code 
library(dplyr)
library(readr)
library(ggplot2)
library(knitr)
library(tidyr)

# Reading Data
dataraw <- read.csv("Chicago_Crimes_2012_to_2017.csv", stringsAsFactors = FALSE)
summary(dataraw)
str(dataraw)


# data mining & analysis 
# omitting data we dont need
data <- na.omit(dataraw)
data$Primary.Type <- as.factor(data$Primary.Type)
data$Description <- as.factor(data$Description) 
data$Location.Description <- as.factor(data$Location.Description) 
data$IUCR <- as.factor(data$IUCR) 

data$Arrest[which(data$Arrest == "True")] <- 1
data$Arrest[which(data$Arrest == "False")] <- 0

data$Domestic[which(data$Domestic == "True")] <- 1
data$Domestic[which(data$Domestic == "False")] <- 0

head(data)

# Plotting the data  focusing on primary type first
dataprimary <- ggplot(data,aes(Primary.Type))
dataprimary + geom_histogram(stat = "count") + coord_flip()

# plotting arrest 
dataarrest <- ggplot(data,aes(Arrest))
dataarrest + geom_histogram(stat = "count") + coord_flip()

# plotting year 
datayear<- ggplot(data,aes(Year))
datayear + geom_histogram(stat = "count") + coord_flip()

# plotting decsription # this has a lot 
dataDes<- ggplot(data,aes(Location.Description))
dataDes + geom_histogram(stat = "count") + coord_flip()

# plotting bar plots to see if i can interpret results better
barplot(table(data$Year))
barplot(table(data$Primary.Type))
barplot(table(data$Location.Description))
barplot(table(data$Arrest))

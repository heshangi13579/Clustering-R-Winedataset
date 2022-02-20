# Clustering-R-Winedataset

//importing the libraries
library(janitor)
library(dplyr)

//reading the data in to the R
WineData = read_excel("C:/Users/Dell/Desktop/Wine.xlsx")
View(WineData)

//cleaning the data set
clean<-clean_names(WineData)
clean_x<-clean %>% remove_empty(whic=c("rows"))
clean_x<-clean %>% remove_empty(whic=c("cols"))
unique(clean)

//removing the column Class
WineDataWithoutClass = WineData
WineDataWithoutClass$Class <- NULL
View(WineDataWithoutClass)

//Normalize around Standard deviation the data set. Because the data in different columns are in different ranges.
WineDataStandadized <- scale(WineDataWithoutClass[-1])
View(WineDataStandadized)

//clustering
//using the kmeans to predetermine the number of clusters
//we need 3 clusters because we have 1,2 and 3 as classes.

results <- kmeans(WineDataStandadized,3)
results

attributes(results)

//centers of each attribute
results$centers

//now these clusters are compared with original table groups (1,2,3 classes)
table(WineData$Class, results$cluster)

plot(results$cluster)

plot(WineData$Class, results$cluster)

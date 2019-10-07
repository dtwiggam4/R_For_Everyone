#Install Packages
install.packages("devtools")
install.packages("useful")
install.packages("usethis")
install.packages("ggplot2")
install.packages("coefplot")
install.packages("dplyr")
install.packages("plyr")
install.packages("stringr")
install.packages("reshape2")
install.packages("xml2")
install.packages("rvest")

#Load Pakages
library("devtools")
library("useful", "usethis", "ggplot2", "coefplot", "dplyr", "plyr", "stringr", "reshape2")
library("useful")
library("usethis")
library("ggplot2")
library("coefplot")
library("dplyr")
library("plyr")
library("stringr")
library("reshape2")
library("xml2")
library("rvest")

#Install ffanalytics package
devtools::install_github("FantasyFootballAnalytics/ffanalytics")

#Scrape fantasy leaders from fantasypros.com
require(rvest)
d = read_html("https://www.fantasypros.com/nfl/reports/leaders/")

#Extract HTML code for data table on webpage
#Helpful web resource outlining instructions: https://rafalab.github.io/dsbook/web-scraping.html 
#Resource Guide: https://rafalab.github.io/dsbook/tidyverse.html
tab = d %>% html_nodes("table")

#Verify data pull
tab 

#Extract specific table of interest
tab <- tab[[1]] %>% html_table

#Check object type
class(tab)

#Reformat data frame with appropriate headers
tab <- tab %>% setNames(c("Rank", "Player", "Team", "Position", "Points", "Games", "Avg"))
tab
head(tab)

#Export to CSV file
write.csv(tab, "Fantasy Football Leaders.csv", row.names = F)

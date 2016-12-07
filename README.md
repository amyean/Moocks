# Moocks
獎學金

rm(list=ls(all.names=TRUE))
library(XML)
library(bitops)
library(RCurl)
library(httr)
Sys.setlocale(category = "LC_ALL", locale = "cht")
urlPath <- "http://love.ntu.edu.tw/CustomerSet/207_NTUactive/u_active_v1.asp?id={6744E5C6-790F-420F-A4B8-07F425A5C771}"
temp    <- getURL(urlPath, encoding = "big5")
xmldoc  <- htmlParse(temp)
res <- GET(urlPath)
res  <- htmlParse(res)
title   <- xpathSApply(xmldoc, "//td[@align=\"left\"]", xmlValue)
title   <- gsub("\n", "", title)
title   <- gsub("\t", "", title)
write.table(title,file="title.csv")

matrix  <-t(matrix(title,4,10))
colnames(matrix)<-c("類別名稱","申請日期","獎學金名稱","申請對象")

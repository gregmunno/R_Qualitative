# R_Qualitative
Creating a corpus in R

## Installing R 
Download and install R at https://cran.case.edu/

Download and install RStudio https://www.rstudio.com/products/rstudio/download/ . Not to make sure you install R first, then R Studio 

## What is R?
R is a programing language that specializes in statistical analysis and the plotting of data. Written mostly in C and in R itself, it first appeared in 1993. It is free and open source, and is a top choice for data scientists and academic researchers, and also popular in newsrooms. Developers have created a rich repository of "packages" for R, which create new funtionality and even a different vocabulary for writing code than Base R. These packages have expanded R's usability to include things like data scrapping, textual analysis, and interactive graphics. 

## What is RStudio?
RStudio is an interactive development environment for R. 

## RStudio -- A closer look
In RStudio you generally have four panes -- one to write your scripts (Source), one where your scripts are excuted (Console), one where your data is stored (Environment) and one to navigate to files, visualize data, etc.) You can customize the layout and appearance under "Tools > Global Settings"

Useful keyboard shortcuts can be found at https://support.rstudio.com/hc/en-us/articles/200711853-Keyboard-Shortcuts . Three that get used a lot are:

RUN Code - Ctrl+Enter
Insert PIPE opperator (%) - Ctrl+Shift+M

Insert ASSIGNMENT operator (<-) -	Alt+- (Windows)	Option+- (Mac) 

Clear Console - CTRL+L

At its base, R works like a calculator. So you can type 2+2 in the console and hit return and get 4, or you type 2-2 in scripting pane, click run (or control click), and the result will again appear in the console. 

You can assign values to a variable and then have R priont that value 
```
x <- 2
x 
```
And you can assign a series of values to a variable to create a vector 
```
y <- c(1,2,3,4)
y 
```
## Text files
Download and store in an easy to access location like your desktop or documents folder. 

Obama inauguration text https://drive.google.com/open?id=1hKBMFDVVrb681mPp6LYDcBbpsuo4C7Ih
Trump inauguration text https://drive.google.com/open?id=1bBVFvRVVeaK_aFBIA_uSw2EQTO3i6k7E

## Install Packages
```
install.packages("tm")  # for text mining
install.packages("SnowballC") # for text stemming
install.packages("wordcloud") # word-cloud generator
install.packages("RColorBrewer") # color palettes
```
## Load
```
library("tm")
library("SnowballC")
library("wordcloud")
library("RColorBrewer")
```
```
text <- readLines(file.choose())
```
```
docs <- Corpus(VectorSource(text))
```
```
inspect(docs)

toSpace <- content_transformer(function (x , pattern ) gsub(pattern, " ", x))
docs <- tm_map(docs, toSpace, "/")
docs <- tm_map(docs, toSpace, "@")
docs <- tm_map(docs, toSpace, "\\|")
```

## Remove punctuations
```
docs <- tm_map
```

## Convert the text to lower case
```
docs <- tm_map(docs, content_transformer(tolower))

inspect(docs)

dtm <- TermDocumentMatrix(docs)
m <- as.matrix(dtm)
v <- sort(rowSums(m),decreasing=TRUE)
d <- data.frame(word = names(v),freq=v)
head(d, 10)

set.seed(1234)
wordcloud(words = d$word, freq = d$freq, min.freq = 1,
          max.words=200, random.order=FALSE, rot.per=0.35,
          colors=brewer.pal(8, "Paired"))
```

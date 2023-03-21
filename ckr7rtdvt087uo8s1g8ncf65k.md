---
title: "6- Working directories and paths in R programming"
datePublished: Sat Jul 17 2021 12:53:08 GMT+0000 (Coordinated Universal Time)
cuid: ckr7rtdvt087uo8s1g8ncf65k
slug: 6-working-directories-and-paths-in-r-programming
tags: tutorial, programming-blogs, r, research, programming-languages

---

#### Set a default working directory in RStudio

Go to Tools &gt; Global Options &gt; General &gt; Default working directory (when not in a project) &gt; Browse &gt; Choose your directory &gt; Apply &gt; OK.

![Default_working_directory.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626525125418/DRApsLpqW.png align="left")

![Default_working_directory2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626525141549/-xQXqNS0o.png align="left")

#### Get current directory

```r
getwd() # stands for "get working directory"
```

#### Change working directory

```r
setwd("D:/R4Researchers")# setwd() function stands for “set working directory”
setwd('C:/Users/Azad/Downloads') # Change working directory to download folder
getwd()
```

#### Choose directory from RStudio

Use either `ctrl+shift+H` or go to Session &gt; Set Working directories &gt; Choose Directory.

#### List functions

```r
ls() # ls() function shows defined data sets and functions
```

![ls().png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626525991705/WUkBvQ-yuY.png align="left")

To remove everything in the working environment (only apply it when necessary):

```r
rm(list=ls())
```

#### Select path:

```r
file.path('D:', 'Natural_Resources', 'Soil')
file.path('D:', 'R4Researchers', 'India_China_LAI_and_LST.csv')
```

#### Use path for set directory

```r
setwd(file.path('D:', 'Natural_Resources', 'Soil'))
getwd()
```

#### An absolute path

```r
dt<- read.csv('D:/R4Researchers/data_ziped/data_ziped.csv')
dt
```

#### Relative path

```r
dt1<- read.csv('./data_ziped/data_ziped.csv')
```

#### Create folder and files

Create a folder inside the working directory:

```r
dir.create('data')
dir.create('data/test')
```

Create an empty file inside the directory:

```r
file.create("test_text_file.txt")
file.create("test_word_file.docx")
file.create("test_csv_file.csv")
```

Create 10 empty CSV files inside the directory using sapply function:

```r
sapply(paste0("test", 1:10, ".csv"), file.create)
```

#### Delete file

```r
unlink('test_word_file.docx')
file.remove('test_text_file.txt')
```

Delete 5 files with sapply function

```r
sapply(paste0('test', 1:5, '.csv'), unlink)
```

#### Copy file

```r
# file.copy("name_file.csv", "destination_folder")
file.copy("test5.csv", "D:/R4Researchers/data/test")
```

#### List files in the directory

```r
list.files("D:/R4Researchers/", full.names = TRUE, recursive = TRUE)
# list all CSV files non-recursively
list.files(pattern = ".csv")

# list all CSV files recursively through each sub-folder
list.files(pattern = ".csv", recursive = TRUE)
```

#### Check if a file or directory exists

```r
file.exists("D:/R4Researchers/data/test")
# TRUE
file.exists("D:/R4Researchers/data/test.csv")
# FALSE
file.exists('D:/R4Researchers/data')
# TRUE 
dir.exists('D:/R4Researchers')
# TRUE
dir.exists('D:/R4Researchers/new_data')
# FALSE
```

If you enjoy the content, please consider subscribing to my [YouTube channel](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) for future updates.

To access video tutorials and receive a certificate, enroll in my [Udemy course](https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A).
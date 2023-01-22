# 6- Working directories and paths in R programming

#### Set a default working directory in RStudio
Tools> Global Options> General> Default working directory (when not in a project)> Browse> Choose your directory> Apply> OK

![Default_working_directory.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626525125418/DRApsLpqW.png)

![Default_working_directory2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626525141549/-xQXqNS0o.png)

#### Get current directory
```
getwd() # stands for "get working directory"
```
#### Change working directory
```
setwd("D:/R4Researchers")# setwd() function stands for “set working directory”
setwd('C:/Users/Azad/Downloads') # Change working directory to download folder
getwd()
```
#### Choose directory from RStudio:
ctrl+shift+H
or: Session> Set Working directories> Choose Directory


#### List functions
```
ls() # ls() function shows defined data sets and functions
```
![ls().png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626525991705/WUkBvQ-yuY.png)

To remove everything in the working environment (only apply it when it is necessary):
```
rm(list=ls())
```

#### Select path:
```
file.path('D:', 'Natural_Resources', 'Soil')
file.path('D:', 'R4Researchers', 'India_China_LAI_and_LST.csv')
```
#### Use path for set directory
```
setwd(file.path('D:', 'Natural_Resources', 'Soil'))
getwd()
```

#### An absolute path
```
dt<- read.csv('D:/R4Researchers/data_ziped/data_ziped.csv')
dt
```
#### Relative path
```
dt1<- read.csv('./data_ziped/data_ziped.csv')
```
#### Create folder and files
Create a folder inside the working directory:
```
dir.create('data')
dir.create('data/test')
```

Create an empty file inside the directory:

```
file.create("test_text_file.txt")
file.create("test_word_file.docx")
file.create("test_csv_file.csv")
```
Create 10 empty csv file inside directory using sapply function
```
sapply(paste0("test", 1:10, ".csv"), file.create)
```
#### Delete file
```
unlink('test_word_file.docx')
file.remove('test_text_file.txt')
```
Delete 5 files with sapply function
```
sapply(paste0('test', 1:5, '.csv'), unlink)
```
#### Copy file

```
# file.copy("name_file.csv", "destination_folder")
file.copy("test5.csv", "D:/R4Researchers/data/test")
```
#### List files in the directory
```
list.files("D:/R4Researchers/", full.names = TRUE, recursive = TRUE)
# list all CSV files non-recursively
list.files(pattern = ".csv")

# list all CSV files recursively through each sub-folder
list.files(pattern = ".csv", recursive = TRUE)
```
  
#### Check if a file or directory exists
```
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
<p>If you like the content, please <a target="_blank" href="https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1">SUBSCRIBE</a> to my channel for the future content</p>

To get full video tutorial and certificate, please, enroll in the course through this link:
https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A
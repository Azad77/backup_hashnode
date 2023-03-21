---
title: "13- Create a report from data in R programming"
datePublished: Wed Jul 21 2021 12:26:45 GMT+0000 (Coordinated Universal Time)
cuid: ckrdgmunz0c33a2s1fad57rwt
slug: 13-create-a-report-from-data-in-r-programming
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1626870311450/_JavdQRqT.png
tags: tutorial, r, research, coding, programming-languages

---

#### Install and load packages (DataExplorer, datasets, ggplot2):

```r
#install.packages("DataExplorer")
# Load library
library(DataExplorer) # load DataExplorer
library(datasets)
library(ggplot2)
```

Download the data files [**LAI\_factors.csv**](https://github.com/Azad77/py4researchers/blob/main/data/LAI_factors.csv) and [**Countries\_LAI\_and\_LST.csv**](https://github.com/Azad77/py4researchers/blob/main/data/Countries_LAI_and_LST.csv).

#### Read in datasets:

```r
dt1<-read.csv(file.path('D:', 'R4Researchers', 'Countries_LAI_and_LST.csv'))
dt2<-read.csv(file.path('D:', 'R4Researchers', 'LAI_factors.csv'))
```

```r
introduce(airquality) # to describe basic information
introduce(dt1)

plot_bar(mtcars)
plot_boxplot(iris, by = "Species", ncol = 2L)
plot_correlation(iris)
plot_histogram(iris, ncol = 2L)
plot_prcomp(na.omit(airquality), nrow = 2L, ncol = 2L) # Visualize principal component analysis
plot_qq(iris) # plot quantile-quantile for each continuous feature
plot_scatterplot(iris, by = "Species") # create scatterplot for all features
plot_str(iris) # visualize data structure
```

#### Create a report

```r
create_report(iris)
create_report(airquality, y = "Ozone")

create_report(dt1)
plot_histogram(dt1)

create_report(dt2)
plot_histogram(dt2)
```

#### Create customized report

```r
create_report(
  data = dt2,
  output_format = html_document(toc = TRUE, toc_depth = 6, theme = "flatly"),
  output_file = "report_LAI_factors.html",
  output_dir = getwd(),
  y = "Year",
  config = configure_report(
    add_plot_prcomp = TRUE,
    plot_qq_args = list("by" = "Year", sampled_rows = 1000L),
    plot_bar_args = list("with" = "LAI_India"),
    plot_correlation_args = list("cor_args" = list("use" = "pairwise.complete.obs")),
    plot_boxplot_args = list("by" = "LST_India"),
    global_ggtheme = quote(theme_light())
  )
)
```

The output will be saved in the specified directory as an HTML file.

![report.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1626874201972/ycg4tkWBq.png align="left")

If you enjoy the content, please consider subscribing to my [YouTube channel](https://www.youtube.com/channel/UCpbWlHEqBSnJb6i4UemXQpA?sub_confirmation=1) for future updates.

To access video tutorials and receive a certificate, enroll in my [Udemy course](https://www.udemy.com/course/r-for-research/?referralCode=B6DCFDE343F0592EA61A).
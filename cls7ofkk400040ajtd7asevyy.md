---
title: "16- Analyzing Annual Weather Data with R"
datePublished: Sun Feb 04 2024 15:47:31 GMT+0000 (Coordinated Universal Time)
cuid: cls7ofkk400040ajtd7asevyy
slug: 16-analyzing-annual-weather-data-with-r
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1707061640833/1ac8a7c0-7e7e-4cd4-8e14-2476cf233abf.jpeg
tags: functions, r, weather

---

In this blog post, we'll explore how to import and analyze annual weather data using R programming. The focus will be on a specific weather station with the code "406210-99999" in Kirkuk. We'll calculate annual means (or sums eg. precipitation) for various weather variables and visualize the results. Let's dive into the code step by step.

## Load Necessary Packages

```R
# Load necessary packages
library(worldmet)  # Package for importing NOAA weather data
library(dplyr)      # Package for data manipulation
library(lubridate)  # For handling dates
```

## **Define the Import and Analysis Function**

```r
# Function to import NOAA data and calculate annual means (or sums)
import_and_calculate_means <- function(year) {
  # Import weather data for a specific station and a given year
  data <- importNOAA(code = "406210-99999", year = year)

  # Convert the date column to a Date type if it's not already in that format
  data$date <- as.Date(data$date)

  # Extract year from the date column using lubridate package
  data$year <- year(data$date)

  # Select only numeric columns for summarization
  numeric_data <- data %>% select_if(is.numeric)

  # Group by year and calculate annual means (or sums( for each numeric variable
  annual_data <- numeric_data %>%
    group_by(year) %>%
    #summarize(across(everything(), sum, na.rm = TRUE))
    summarzie(across(everything(), mean, na.rm = TRUE))

  # Show the resulting annual aggregated data
  print(annual_data)

  # Write the data to a CSV file with a filename indicating the station code and the year
  #write.csv(annual_data, paste("Kirkuk_Weather_data_annual_sum_", year, ".csv", sep = ""), row.names = TRUE)
  write.csv(annual_data, paste("Kirkuk_Weather_data_annual_average_", year, ".csv", sep = ""), row.names = TRUE)
}
```

## **Loop Through the Years and Execute the Function**

```r
# Loop through the years 2014 to 2023 and apply the import_and_calculate_means function
for (year in 2014:2023) {
  import_and_calculate_means(year)
  #import_and_calculate_sums(year)
}
```

Feel free to run this code in your R environment, and don't forget to share your findings and visualizations based on the annual weather data. Happy coding!

# Here's the entire R code

```r
# Load necessary packages
library(worldmet)  # Package for importing NOAA weather data
library(dplyr)      # Package for data manipulation
library(lubridate)  # For handling dates

# Function to import NOAA data and calculate annual means
import_and_calculate_means <- function(year) {
  # Import weather data for a specific station and a given year
  data <- importNOAA(code = "406210-99999", year = year)

  # Convert the date column to a Date type if it's not already in that format
  data$date <- as.Date(data$date)

  # Extract year from the date column using lubridate package
  data$year <- year(data$date)

  # Select only numeric columns for summarization
  numeric_data <- data %>% select_if(is.numeric)

  # Group by year and calculate annual means for each numeric variable
  annual_data <- numeric_data %>%
    group_by(year) %>%
    summarize(across(everything(), mean, na.rm = TRUE))

  # Show the resulting annual aggregated data
  print(annual_data)

  # Write the data to a CSV file with a filename indicating the station code and the year
  write.csv(annual_data, paste("Kirkuk_Weather_data_annual_sum_", year, ".csv", sep = ""), row.names = TRUE)
}

# Loop through the years 2014 to 2023 and apply the import_and_calculate_means function
for (year in 2014:2023) {
  import_and_calculate_means(year)
}
```
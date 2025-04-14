Introductory Training Materials for R and RStudio

This repository contains introductory training materials for learning R and RStudio, designed for a one-hour teaching session. The content covers essential topics for beginners, with clear explanations and code examples using base R wherever possible. Optional exercises and challenges are included for self-paced practice. These materials are ideal for new users in statistics, data analysis, or bioinformatics.

1. Introduction to R and RStudio

R is a powerful, open-source programming language for statistical computing and graphics, while RStudio is an integrated development environment (IDE) that makes working with R easier. In this session, we'll cover the basics of setting up R and RStudio, navigating the interface, and running simple commands.

Installation: Download R from CRAN and RStudio from Posit.

RStudio Interface: Familiarize yourself with the Console (for running commands), Script Editor (for writing code), Environment (for viewing data), and Plots pane (for visualizations).

First Steps: Let's set up a workspace and install a basic package.

r

Set your working directory (adjust the path to your folder)

setwd("path/to/your/folder")

Install a package (e.g., 'utils' is built-in, but this shows the syntax)

install.packages("utils")

Load a library (though 'utils' is preloaded, this is for demonstration)

library(utils)

2. Importing Excel and CSV Files

Importing data is a fundamental step in any analysis. R provides built-in functions like read.csv() for CSV files, and we can use the readxl package for Excel files.

r

Importing a CSV file using base R

data_csv <- read.csv("data.csv")\

head(data_csv) # Display the first few rows

Importing an Excel file using the 'readxl' package

install.packages("readxl")\

library(readxl)\

data_excel <- read_excel("data.xlsx")\

head(data_excel) # Display the first few rows

3. Basic Data Manipulation (Using Base R)

Data manipulation involves cleaning and transforming data for analysis. In this section, we'll use base R functions to perform common tasks such as subsetting, creating new columns, and summarizing data.

r

Create a sample dataset for demonstration

data <- data.frame(ID = 1:5, Score = c(80, 90, 85, 70, 95))

Filter rows where Score is greater than 80

filtered_data <- subset(data, Score > 80)\

print(filtered_data)

Select specific columns by indexing

selected_data <- data,c("ID","Score")\

print(selected_data)

Add a new column based on a condition

dataPassed<−ifelse(dataScore >= 75, "Yes", "No")\

print(data)

Summarize data to calculate the average score

average_score <- mean(data$Score)\

cat("Average Score:", average_score, "\n")

4. Matching IDs Between Tables

Combining datasets based on common identifiers (like IDs) is a common task. Base R's merge() function can accomplish this without additional packages.

r

Create two sample datasets with a common 'ID' column

table1 <- data.frame(ID = 1:3, Name = c("Alice", "Bob", "Charlie"))\

table2 <- data.frame(ID = 2:4, Score = c(85, 90, 88))

Merge tables using base R's merge() function

merged_data <- merge(table1, table2, by = "ID", all = TRUE)\

print(merged_data)

5. Statistical Analyses

R excels at statistical analysis. We'll cover some common tests using base R functions, including chi-square tests, t-tests, linear regression, and logistic regression.

r

Chi-square test

observed <- c(50, 30, 20)\

expected <- c(40, 40, 20)\

chisq.test(observed, p = expected / sum(expected))

t-test

group1 <- c(5.1, 5.5, 5.8, 6.0)\

group2 <- c(6.2, 6.5, 6.8, 7.0)\

t.test(group1, group2)

Linear regression

data <- data.frame(x = 1:10, y = c(2.3, 2.5, 2.7, 3.0, 3.2, 3.5, 3.7, 4.0, 4.2, 4.5))\

model <- lm(y ~ x, data = data)\

summary(model)

Logistic regression

data <- data.frame(x = c(1, 2, 3, 4, 5), y = c(0, 1, 0, 1, 1))\

log_model <- glm(y ~ x, data = data, family = binomial)\

summary(log_model)

6. Plotting Basic Plots (Using Base R)

Visualization is key to understanding data. Base R provides simple and effective plotting functions.

r

Scatter plot

data <- data.frame(x = 1:10, y = c(2.3, 2.5, 2.7, 3.0, 3.2, 3.5, 3.7, 4.0, 4.2, 4.5))\

plot(datax,datay, main = "Scatter Plot", xlab = "X", ylab = "Y", pch = 19, col = "blue")\

abline(lm(y ~ x, data = data), col = "red")

Bar plot

bar_data <- c(A = 5, B = 3, C = 7)\

barplot(bar_data, main = "Bar Plot", xlab = "Category", ylab = "Count", col = "green")

Histogram

hist_data <- c(1, 2, 2, 3, 3, 3, 4, 4, 5)\

hist(hist_data, main = "Histogram", xlab = "Value", ylab = "Frequency", col = "lightblue", border = "black")

7. Plotting Advanced Examples (Using ggplot2)

For more complex visualizations, the ggplot2 package offers greater flexibility.

r

Install and load ggplot2

install.packages("ggplot2")\

library(ggplot2)

Scatter plot with regression line

data <- data.frame(x = 1:10, y = c(2.3, 2.5, 2.7, 3.0, 3.2, 3.5, 3.7, 4.0, 4.2, 4.5))\

ggplot(data, aes(x = x, y = y)) +\

geom_point() +\

geom_smooth(method = "lm")

Manhattan plot example

set.seed(123)\

manhattan_data <- data.frame(\

SNP = paste0("rs", 1:1000),\

Chromosome = rep(1:10, each = 100),\

Position = rep(1:100, times = 10),\

P_value = runif(1000, 0, 1)\

)\

manhattan_datalogP<−−log10(manhattand​ataP_value)\

ggplot(manhattan_data, aes(x = Position, y = logP, color = as.factor(Chromosome))) +\

geom_point() +\

theme_minimal() +\

labs(title = "Manhattan Plot", x = "Position", y = "-log10(P-value)")

8. Introduction to Bioconductor, CRAN, and Shiny Apps

R's ecosystem includes repositories like CRAN and Bioconductor, and Shiny allows users to build interactive web apps.

r

Install Bioconductor and Shiny

if (!requireNamespace("BiocManager", quietly = TRUE))\

install.packages("BiocManager")\

BiocManager::install("GenomicRanges")\

install.packages("shiny")\

library(shiny)

Simple Shiny app

ui <- fluidPage(\

titlePanel("Simple Shiny App"),\

sidebarLayout(\

sidebarPanel(\

sliderInput("num", "Choose a number:", min = 1, max = 100, value = 50)\

),\

mainPanel(\

textOutput("result"),\

plotOutput("myplot")\

)\

)\

)\

server <- function(input, output) {\

outputresult <- renderText({ paste("You selected:", inputnum) })\

output$myplot <- renderPlot({\

barplot(c(A = inputnum,B=100−inputnum, C = input$num / 2),\

ylim = c(0, 100), col = c("lightgreen", "red", "lightblue"))\

})\

}\

shinyApp(ui = ui, server = server)

9. Optional Extension Materials for Self-Paced Practice
Exercises

Data Import: Import a CSV or Excel file, display the first 10 rows, and check for missing values.

Data Manipulation: Filter rows based on a condition and create a new column with a calculated value.

Table Matching: Merge two datasets and explore the differences between all = TRUE and all = FALSE.

Statistics: Perform a t-test on two groups of data and interpret the p-value.

Basic Plotting: Create a scatter plot, bar plot, and histogram using base R.

Code Challenges

Simulation and Analysis: Simulate a dataset, fit a linear regression model, and plot the results.

Custom Function: Write a function to summarize a column (mean, median, min, max).

Advanced Shiny App: Extend the Shiny app to include a dropdown menu for selecting bar colors.

This Markdown file is structured for GitHub hosting. Feel free to clone this repository, run the code examples, and try the exercises to enhance your R skills!

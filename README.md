
# R and RStudio Training Materials

Welcome to this introductory session on R and RStudio! These materials are structured for a ~1-hour live session plus optional self-paced exploration.

You'll learn about setting up your environment, working with data, running basic analyses, and exploring more advanced features.

---

## 1. Introduction: What are R and RStudio?

**R** is a free, open-source language for statistics, data analysis, and visualization.  
**RStudio** is an Integrated Development Environment (IDE) that makes working with R easier.

**Resources**:  
- [Download R](https://cran.r-project.org/)  
- [Download RStudio](https://posit.co/download/rstudio-desktop/)  
- [CRAN Packages Repository](https://cran.r-project.org/web/packages/)  
- [Bioconductor for Bioinformatics](https://bioconductor.org/)  
- [Shiny Apps for Interactive Web Applications](https://shiny.posit.co/)

---

## 2. R Basics: Vectors, Data Frames, and More

Learn the foundational data structures and control flows in R, essential for any analysis.

**Vectors**  
A vector is a sequence of data elements of the same type.

```r
weights <- c(45.2, 50.1, 55.0)
```

**Data Frames**  
A data frame is like a table or spreadsheet in R.

```r
penguins_small <- data.frame(
  species = c("Adelie", "Chinstrap", "Gentoo"),
  Bill.Length..mm. = c(39.1, 48.7, 50.0),
  Body.Mass..g. = c(3750, 3800, 5000)
)
```

**Lists**  
Lists can contain different types of objects.

```r
example_list <- list(
  numbers = c(1, 2, 3),
  names = c("Alpha", "Beta"),
  data = penguins_small
)
```

**Matrices**  
Matrices are two-dimensional arrays.

```r
matrix_example <- matrix(1:6, nrow = 2, ncol = 3)
```

**Factors**  
Factors are used for categorical data.

```r
species_factor <- factor(c("Adelie", "Chinstrap", "Gentoo", "Adelie"))
```

**If-Else Statement**  
Control flow for decision making.

```r
x <- 5
if (x > 0) {
  print("Positive number")
} else {
  print("Zero or negative number")
}
```

---

## 3. Importing Example Data: Penguins Dataset

Practice loading real-world datasets into R.

```r
penguins <- read.csv("https://raw.githubusercontent.com/jcheng5/simplepenguins.R/main/penguins.csv")
head(penguins)
```

---

## 4. Basic Data Manipulation (Using Base R)

Learn to filter, create new variables, and summarize data.

**Subsetting and Filtering**

```r
heavy_penguins <- subset(penguins, Body.Mass..g. > 4000)
head(heavy_penguins)
```

**Creating New Columns**

```r
penguins$size_category <- ifelse(penguins$Body.Mass..g. > 4000, "Large", "Small")
head(penguins)
```

**Summarizing Data**

```r
mean(penguins$Body.Mass..g., na.rm = TRUE)
```

---

## 5. Matching IDs Between Tables

Understand how to join datasets together by a common variable.

```r
extra_info <- data.frame(
  Species = c("Adelie", "Chinstrap", "Gentoo"),
  conservation_status = c("Least Concern", "Least Concern", "Near Threatened")
)

merged_penguins <- merge(penguins, extra_info, by = "Species")
head(merged_penguins)
```

---

## 6. Basic Statistical Analyses

Explore simple statistical tests and models.

**Chi-Square Test**

```r
table(penguins$Sex)
chisq.test(table(penguins$Sex))
```

**t-test**

```r
t.test(Body.Mass..g. ~ Sex, data = penguins)
```

**Linear Regression**

```r
model <- lm(Body.Mass..g. ~ Bill.Length..mm., data = penguins)
summary(model)
```

---

## 7. Basic Plotting (Base R)

Visualize your data with simple plots.

**Scatter Plot**

```r
plot(penguins$Bill.Length..mm., penguins$Body.Mass..g.,
     main = "Bill Length vs Body Mass",
     xlab = "Bill Length (mm)", ylab = "Body Mass (g)",
     pch = 19, col = "blue")
abline(lm(Body.Mass..g. ~ Bill.Length..mm., data = penguins), col = "red")
```

**Histogram**

```r
hist(penguins$Body.Mass..g., main = "Body Mass Distribution", col = "lightblue")
```

---

## 8. Advanced Self-Exploration (Optional)

For those who want to go beyond the basics.

**Advanced Plotting with ggplot2**

```r
install.packages("ggplot2")
library(ggplot2)

ggplot(penguins, aes(x = Bill.Length..mm., y = Body.Mass..g., color = Species)) +
  geom_point() +
  geom_smooth(method = "lm") +
  theme_minimal()
```

**Shiny App Example**  
Create interactive web apps directly from R.

```r
install.packages("shiny")
library(shiny)

ui <- fluidPage(
  titlePanel("Penguins Explorer"),
  sidebarLayout(
    sidebarPanel(
      sliderInput("mass", "Minimum Body Mass:", 2500, 6500, 4000)
    ),
    mainPanel(
      tableOutput("filtered_penguins")
    )
  )
)

server <- function(input, output) {
  output$filtered_penguins <- renderTable({
    subset(penguins, Body.Mass..g. > input$mass)
  })
}

shinyApp(ui = ui, server = server)
```

For more Shiny examples, visit: https://shiny.posit.co/

---

## 9. Exercises for Self-Practice

Test your knowledge and skills!

- **Importing**: Load the penguins dataset.
- **Filtering**: Find penguins with flipper length above average.
- **Summary**: Calculate mean and median body mass for each species.
- **Plots**: Create a bar plot of species counts.
- **Statistical Test**: Compare bill lengths between species using ANOVA.
- **Advanced**: Build a Shiny app where users can select species to view.

---

Happy coding! 🚀

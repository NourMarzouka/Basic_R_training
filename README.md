
# R and RStudio Training Materials

Welcome to this introductory session on R and RStudio! These materials are structured for a ~1-hour live session plus optional self-paced exploration.

You'll learn about setting up your environment, working with data, running basic analyses, and exploring more advanced features.

---

## 0. Introduction: What are R and RStudio?

In this section, we introduce R and RStudio:
- **R** is a free, open-source language for statistics, data analysis, and visualization.
- **RStudio** is an Integrated Development Environment (IDE) that makes working with R easier.

**Resources**:
- [Download R](https://cran.r-project.org/)
- [Download RStudio](https://posit.co/download/rstudio-desktop/)
- [CRAN Packages Repository](https://cran.r-project.org/web/packages/)
- [Bioconductor for Bioinformatics](https://bioconductor.org/)
- [Shiny Apps for Interactive Web Applications](https://shiny.posit.co/)

---

## 1. Basics of R: Vectors, Data Frames, If-Else, and More

Learn the foundational data structures and control flows in R, essential for any analysis.

### Vectors

```r
weights <- c(45.2, 50.1, 55.0)
```

### Data Frames

```r
penguins_small <- data.frame(
  species = c("Adelie", "Chinstrap", "Gentoo"),
  bill_length_mm = c(39.1, 48.7, 50.0),
  body_mass_g = c(3750, 3800, 5000)
)
```

### Lists

```r
example_list <- list(
  numbers = c(1, 2, 3),
  names = c("Alpha", "Beta"),
  data = penguins_small
)
```

### Matrices

```r
matrix_example <- matrix(1:6, nrow = 2, ncol = 3)
```

### Factors

```r
species_factor <- factor(c("Adelie", "Chinstrap", "Gentoo", "Adelie"))
```

### If-Else Statement

```r
x <- 5
if (x > 0) {
  print("Positive number")
} else {
  print("Zero or negative number")
}
```

---

## 2. Importing Example Data: Penguins Dataset

Practice loading real-world datasets into R.

```r
penguins <- read.csv("https://raw.githubusercontent.com/jcheng5/simplepenguins.R/main/penguins.csv")
head(penguins)
```

---

## 3. Basic Data Manipulation (Using Base R)

Learn to filter, create new variables, and summarize data.

### Subsetting and Filtering

```r
heavy_penguins <- subset(penguins, body_mass_g > 4000)
head(heavy_penguins)
```

### Creating New Columns

```r
penguins$size_category <- ifelse(penguins$body_mass_g > 4000, "Large", "Small")
head(penguins)
```

### Summarizing Data

```r
mean(penguins$body_mass_g, na.rm = TRUE)
```

---

## 4. Matching IDs Between Tables

Understand how to join datasets together by a common variable.

```r
extra_info <- data.frame(
  species = c("Adelie", "Chinstrap", "Gentoo"),
  conservation_status = c("Least Concern", "Least Concern", "Near Threatened")
)

merged_penguins <- merge(penguins, extra_info, by = "species")
head(merged_penguins)
```

---

## 5. Basic Statistical Analyses

Explore simple statistical tests and models.

### Chi-Square Test

```r
table(penguins$sex)
chisq.test(table(penguins$sex))
```

### t-test

```r
t.test(body_mass_g ~ sex, data = penguins)
```

### Linear Regression

```r
model <- lm(body_mass_g ~ bill_length_mm, data = penguins)
summary(model)
```

---

## 6. Basic Plotting (Base R)

Visualize your data with simple plots.

### Scatter Plot

```r
plot(penguins$bill_length_mm, penguins$body_mass_g,
     main = "Bill Length vs Body Mass",
     xlab = "Bill Length (mm)", ylab = "Body Mass (g)",
     pch = 19, col = "blue")
abline(lm(body_mass_g ~ bill_length_mm, data = penguins), col = "red")
```

### Histogram

```r
hist(penguins$body_mass_g, main = "Body Mass Distribution", col = "lightblue")
```

---

## 7. Advanced Self-Exploration (Optional)

Opportunities for those who want to go beyond the basics.

### Advanced Plotting with ggplot2

```r
install.packages("ggplot2")
library(ggplot2)

ggplot(penguins, aes(x = bill_length_mm, y = body_mass_g, color = species)) +
  geom_point() +
  geom_smooth(method = "lm") +
  theme_minimal()
```

### Shiny App Example

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
    subset(penguins, body_mass_g > input$mass)
  })
}

shinyApp(ui = ui, server = server)
```

For other examples, visit: https://shiny.posit.co/

---

## 8. Exercises for Self-Practice

Test your knowledge and skills!

- **Importing**: Load the penguins dataset.
- **Filtering**: Find penguins with flipper length above average.
- **Summary**: Calculate mean and median body mass for each species.
- **Plots**: Create a bar plot of species counts.
- **Statistical Test**: Compare bill lengths between species using ANOVA.
- **Advanced**: Build a Shiny app where users can select species to view.

---

Happy coding! 🚀

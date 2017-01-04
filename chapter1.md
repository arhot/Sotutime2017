---
title       : Perustyökaluja
description : R for Data Science Chapter 3

--- type:NormalExercise lang:r xp:50 skills:1 key:ee4f3bacf1
## Perusfunktiot 

*** =instructions

Hyviä perusfunktiota ovat esimerkiksi summary() ja table(). Näihin ei tarvitse muuta kuin kertoa, mistä halutaan yhteenveto tai taulukko. 

*** =hint

*** =pre_exercise_code
```{r}
library(haven)
library(ggplot2)

ESS2014 <- read_sav("http://s3.amazonaws.com/assets.datacamp.com/production/course_2409/datasets/ESS2014.sav")
```

*** =sample_code
```{r}
# ESS2014 on ladattuna  

summary(ESS2014$f3_1)

table(ESS2014$f3_1)

# Tee yhteenveto ja taulukko muuttujasta Kuinka onnellinen yleisesti ottaen olette?



```
*** =sct
```{r}
test_function("summary", args = "object",
              not_called_msg = "Muista tehdä summary()",
              args_not_specified_msg = "Muista määritellä, mistä tehdään yhteenveto - `x`?",
              incorrect_msg = "Onko suluissa aineisto$muuttujannimi? Tarkista isot ja pienet kirjaimet ja välit")
             
test_error()
success_msg("Hyvin meni!")
```

--- type:NormalExercise lang:r xp:100 skills:1 key:8fac4da90d
## Argumentit

In the previous exercise, you saw a dataset about movies. In this exercise, we'll have a look at yet another dataset about movies!

A dataset with a selection of movies, `movie_selection`, is available in the workspace.

*** =instructions
- Check out the structure of `movie_selection`.
- Select movies with a rating of 5 or higher. Assign the result to `good_movies`.
- Use `plot()` to  plot `good_movies$Run` on the x-axis, `good_movies$Rating` on the y-axis and set `col` to `good_movies$Genre`.

*** =hint
- Use `str()` for the first instruction.
- For the second instruction, you should use `...[movie_selection$Rating >= 5, ]`.
- For the plot, use `plot(x = ..., y = ..., col = ...)`.

*** =pre_exercise_code
```{r}
# You can also prepare your dataset in a specific way in the pre exercise code

library(MindOnStats)
data(Movies)
movie_selection <- Movies[Movies$Genre %in% c("action", "animated", "comedy"),c("Genre", "Rating", "Run")]

# Clean up the environment
rm(Movies)
```

*** =sample_code
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection


# Select movies that have a rating of 5 or higher: good_movies


# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre

```

*** =solution
```{r}
# movie_selection is available in your workspace

# Check out the structure of movie_selection
str(movie_selection)

# Select movies that have a rating of 5 or higher: good_movies
good_movies <- movie_selection[movie_selection$Rating >= 5, ]

# Plot Run (i.e. run time) on the x axis, Rating on the y axis, and set the color using Genre
plot(good_movies$Run, good_movies$Rating, col = good_movies$Genre)
```

*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

test_function("str", args = "object",
              not_called_msg = "You didn't call `str()`!",
              incorrect_msg = "You didn't call `str(object = ...)` with the correct argument, `object`.")

test_object("good_movies")

test_function("plot", args = "x")
test_function("plot", args = "y")
test_function("plot", args = "col")

test_error()

success_msg("Good work!")
```


--- type:NormalExercise lang:r xp:100 skills:1 key:0ce38c3888
## Objektit



*** =instructions

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

```

*** =solution
```{r}

```

*** =sct
```{r}

```
--- type:NormalExercise lang:r xp:100 skills:1 key:3a496c24ee
## Filter

*** =pre_exercise_code
```{r}
# The pre exercise code runs code to initialize the user's workspace.
# You can use it to load packages, initialize datasets and draw a plot in the viewer

movies <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/course/introduction_to_r/movies.csv")
library(ggplot2)
library(dplyr)
library(tidyverse)

ggplot(movies, aes(x = runtime, y = rating, col = genre)) + geom_point()
```




--- type:NormalExercise lang:r xp:100 skills:1 key:9d303343ab
## Muuttujatyypit



*** =instructions

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

```

*** =solution
```{r}

```

*** =sct
```{r}

```
--- type:NormalExercise lang:r xp:100 skills:1 key:7e753c2042
## Arrange



*** =instructions

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

```

*** =solution
```{r}

```

*** =sct
```{r}

```


--- type:NormalExercise lang:r xp:100 skills:1 key:e3ba9a0de4
## Select



*** =instructions

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

```

*** =solution
```{r}

```

*** =sct
```{r}

```

--- type:NormalExercise lang:r xp:100 skills:1 key:05f64e585f
## Mutate



*** =instructions

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

```

*** =solution
```{r}

```

*** =sct
```{r}

```



--- type:NormalExercise lang:r xp:100 skills:1 key:6913b2ddd9
## Summarise



*** =instructions

*** =hint

*** =pre_exercise_code
```{r}

```

*** =sample_code
```{r}

```

*** =solution
```{r}

```

*** =sct
```{r}

```

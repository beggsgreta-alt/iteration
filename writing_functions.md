writing_functions
================

## Do something simple

``` r
x_vec = rnorm(30, mean = 5, sd = 3)

(x_vec - mean(x_vec)) / sd(x_vec)
```

    ##  [1] -2.15988024 -0.56931951  0.87611089 -0.39003930 -1.38585156  1.46016698
    ##  [7]  1.60519459  0.11461479 -0.14720508  0.36096326 -0.59045878 -0.63692635
    ## [13]  0.58557175  0.78555139  1.06348080 -0.34000068  1.07185863 -2.38809959
    ## [19]  0.31807720  0.01055859 -1.58117166 -0.74122165 -0.09686301  1.13651908
    ## [25]  0.35005068 -0.47302830  0.94274013 -0.14119242  0.08213961  0.87765976

I want a function to compute z-scores

``` r
z_scores = function(x) {
  
  if(!is.numeric(x)) {
    stop("Input must be numeric")
  }
  
  if (length(x) < 3 ) {
    stop("Input must have at least three numbers")
  }
  
  z = (x - mean(x)) / sd(x)
  
  return(z)
  
}

z_scores(x_vec)
```

    ##  [1] -2.15988024 -0.56931951  0.87611089 -0.39003930 -1.38585156  1.46016698
    ##  [7]  1.60519459  0.11461479 -0.14720508  0.36096326 -0.59045878 -0.63692635
    ## [13]  0.58557175  0.78555139  1.06348080 -0.34000068  1.07185863 -2.38809959
    ## [19]  0.31807720  0.01055859 -1.58117166 -0.74122165 -0.09686301  1.13651908
    ## [25]  0.35005068 -0.47302830  0.94274013 -0.14119242  0.08213961  0.87765976

Try my function on some other things. These should give errors.

``` r
z_scores(3)
```

    ## Error in `z_scores()`:
    ## ! Input must have at least three numbers

``` r
z_scores("my name is jeff")
```

    ## Error in `z_scores()`:
    ## ! Input must be numeric

``` r
z_scores(mtcars)
```

    ## Error in `z_scores()`:
    ## ! Input must be numeric

``` r
z_scores(c(TRUE, TRUE, FALSE, TRUE))
```

    ## Error in `z_scores()`:
    ## ! Input must be numeric

## Multiple outputs

``` r
mean_and_sd = function(x) {
  
  if(!is.numeric(x)) {
    stop("Input must be numeric")
  }
  
  if (length(x) < 3 ) {
    stop("Input must have at least three numbers")
  }
  
  mean_x = mean(x)  
  sd_x = sd(x)
  
  tibble(
    mean = mean_x,
    sd = sd_x
  )
  
}
```

Check that the function works.

``` r
x_vec = rnorm(100, mean = 3, sd = 4)
mean_and_sd(x_vec)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  2.41  3.99

## Multiple inputs

I’d like to do this with a function.

``` r
sim_data = 
  tibble(
    x = rnorm(100, mean = 4, sd = 3)
  )

sim_data %>% 
  summarize(
    mean = mean(x),
    sd = sd(x)
  )
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.85  2.67

``` r
sim_mean_sd = function(samp_size, mu = 3, sigma = 4) {
  
  sim_data = 
    tibble(
      x = rnorm(n = samp_size, mean = mu, sd = sigma)
  )

sim_data %>% 
  summarize(
    mean = mean(x),
    sd = sd(x)
  )

}

sim_mean_sd(samp_size = 100, mu = 6, sigma = 3)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  5.83  2.85

``` r
sim_mean_sd(mu = 6, samp_size = 100, sigma = 3)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  6.09  2.86

``` r
sim_mean_sd(samp_size = 100)
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.09  3.80

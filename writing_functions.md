writing_functions
================

## Do something simple

``` r
x_vec = rnorm(30, mean = 5, sd = 3)

(x_vec - mean(x_vec)) / sd(x_vec)
```

    ##  [1]  0.46825387  1.32460321 -1.60941307 -0.65762945  0.74034907  1.31981476
    ##  [7] -1.01006633 -0.46068544  0.27848273  0.20256266  1.45967392 -0.24153553
    ## [13]  1.00805397 -1.19157000 -0.41793352  0.05682444 -0.02323446  1.45052371
    ## [19] -1.58844429 -0.45568173 -1.55606887  0.85868299  0.73641509 -1.10197439
    ## [25] -1.40690678  0.70222560  1.75923280 -0.12815293 -0.47225270 -0.04414932

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

    ##  [1]  0.46825387  1.32460321 -1.60941307 -0.65762945  0.74034907  1.31981476
    ##  [7] -1.01006633 -0.46068544  0.27848273  0.20256266  1.45967392 -0.24153553
    ## [13]  1.00805397 -1.19157000 -0.41793352  0.05682444 -0.02323446  1.45052371
    ## [19] -1.58844429 -0.45568173 -1.55606887  0.85868299  0.73641509 -1.10197439
    ## [25] -1.40690678  0.70222560  1.75923280 -0.12815293 -0.47225270 -0.04414932

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

iteration_and_listcols
================

## Lists

You can put anything in a list.

``` r
l = list(
  vec_numeric = 5:8,
  vec_logical = c(TRUE, TRUE, FALSE, TRUE, FALSE, FALSE),
  mat = matrix(1:8, nrow = 2, ncol = 4),
  summary = summary(rnorm(100))
)
```

``` r
l
```

    ## $vec_numeric
    ## [1] 5 6 7 8
    ## 
    ## $vec_logical
    ## [1]  TRUE  TRUE FALSE  TRUE FALSE FALSE
    ## 
    ## $mat
    ##      [,1] [,2] [,3] [,4]
    ## [1,]    1    3    5    7
    ## [2,]    2    4    6    8
    ## 
    ## $summary
    ##     Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
    ## -3.29772 -0.57157  0.03075  0.01440  0.71491  2.07972

``` r
l$vec_numeric
```

    ## [1] 5 6 7 8

``` r
l[[1]]
```

    ## [1] 5 6 7 8

``` r
mean(l[["vec_numeric"]])
```

    ## [1] 6.5

## `for` loop

Create a new list.

``` r
list_norm = 
  list(
    a = rnorm(20, mean = 3, sd = 1),
    b = rnorm(30, mean = 0, sd = 5),
    c = rnorm(40, mean = 10, sd = 0.2),
    d = rnorm(20, mean = -3, sd = 1)
  )
```

``` r
list_norm
```

    ## $a
    ##  [1] 3.043105 3.750140 3.090334 2.659790 3.009643 2.608750 2.313366 3.015424
    ##  [9] 2.278461 2.372871 1.749292 2.411721 2.037609 2.694520 1.842475 4.718334
    ## [17] 2.783814 2.341336 5.619118 2.790408
    ## 
    ## $b
    ##  [1]   5.46540566   5.87671012   1.42958681  -0.56967443  -1.88605614
    ##  [6]  -3.74993829   5.79128577   7.18007374   7.04813228   2.06430303
    ## [11]   0.77088117   0.04621997   3.33972236   5.13547122   3.49275932
    ## [16]  -6.99272943  -0.14508348  -8.34147396   0.37083892  -2.09267797
    ## [21] -11.06300412  -2.98107480 -14.99749133  -5.31896854   9.06776014
    ## [26]   0.73182998   2.12150738   7.11792073  -5.95924214  -1.22177039
    ## 
    ## $c
    ##  [1]  9.977471  9.719547  9.986124  9.776768 10.317338 10.199337  9.729262
    ##  [8] 10.101066  9.825789 10.112270  9.829458  9.944010  9.988811  9.884543
    ## [15] 10.064441  9.920525 10.323942  9.946883  9.894333 10.298384  9.987299
    ## [22]  9.973227 10.124242  9.873240 10.008230  9.723737 10.258449 10.000855
    ## [29]  9.717970 10.065914 10.197060 10.266915  9.694436  9.928027 10.227861
    ## [36] 10.158871 10.244616 10.245025 10.202614  9.992511
    ## 
    ## $d
    ##  [1] -3.463165 -2.071016 -1.557480 -4.525819 -4.632780 -1.367125 -3.789223
    ##  [8] -2.785742 -1.888064 -2.718790 -1.617652 -2.268270 -1.395032 -3.103785
    ## [15] -4.076388 -2.515557 -3.726595 -3.716331 -2.692594 -2.901204

Pause and get my old function.

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

I can apply that function to each list element.

``` r
mean_and_sd(list_norm[[1]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  2.86 0.930

``` r
mean_and_sd(list_norm[[2]])
```

    ## # A tibble: 1 × 2
    ##     mean    sd
    ##    <dbl> <dbl>
    ## 1 0.0577  5.74

``` r
mean_and_sd(list_norm[[3]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  10.0 0.186

``` r
mean_and_sd(list_norm[[4]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -2.84  1.02

Let’s use a for loop:

``` r
output = vector("list", length = 4)

for (i in 1:4) (
  
  output[[1]] = mean_and_sd(list_norm[[i]])
  
)
```

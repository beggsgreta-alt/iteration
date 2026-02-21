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
    ## -2.16198 -0.55007 -0.01433 -0.06824  0.52962  1.45380

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
    ##  [1] 4.413484 4.698925 4.206744 1.617194 3.535839 3.236428 3.450793 2.588087
    ##  [9] 1.319172 4.552373 2.430133 1.954833 3.314969 1.420929 2.641316 2.164511
    ## [17] 3.791492 1.439078 2.333442 1.576897
    ## 
    ## $b
    ##  [1]  -3.813704   1.787227  -6.113747 -10.268261   8.065550 -10.427903
    ##  [7]  -6.052112  -6.734580   5.605439  -2.481504  -2.379711  -2.977062
    ## [13]   2.494921  -6.488116  -3.026250   3.844890   3.112705   1.440333
    ## [19]   4.693238  -0.669679   5.047562 -13.284866  -5.626199   4.125446
    ## [25]  -4.240549   3.683175   4.583427   3.009734  -4.603837   3.601847
    ## 
    ## $c
    ##  [1]  9.791092  9.997725  9.954879  9.822975  9.968550 10.071806  9.979343
    ##  [8]  9.775544 10.196486 10.177495  9.905606  9.766245  9.613174 10.369957
    ## [15] 10.090944  9.786376  9.866546  9.902174 10.234498 10.118858 10.093785
    ## [22] 10.012530 10.051644  9.964611 10.093074  9.917349  9.993742  9.693475
    ## [29]  9.992066 10.050780 10.301312  9.962909  9.955056  9.957770  9.961508
    ## [36] 10.006146 10.062578 10.333222  9.728784 10.148401
    ## 
    ## $d
    ##  [1] -4.666912 -2.719297 -2.250905 -4.226722 -2.582347 -2.557740 -1.222002
    ##  [8] -3.076977 -2.821680 -3.730197 -2.882975 -2.455353 -4.769630 -4.307955
    ## [15] -2.157341 -2.732681 -4.311884 -2.403908 -3.094384 -2.388635

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
    ## 1  2.83  1.12

``` r
mean_and_sd(list_norm[[2]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -1.14  5.52

``` r
mean_and_sd(list_norm[[3]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  9.99 0.171

``` r
mean_and_sd(list_norm[[4]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -3.07 0.955

Let’s use a for loop:

``` r
output = vector("list", length = 4)

for (i in 1:4) (
  
  output[[i]] = mean_and_sd(list_norm[[i]])
  
)
```

## Let’s try map!

``` r
output = map(list_norm, mean_and_sd)
```

what if you want a different function..?

``` r
output = map(list_norm, IQR)
```

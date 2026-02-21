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
    ## -2.69958 -0.63903 -0.05183  0.08154  0.89603  2.74467

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
    ##  [1] 2.179395 3.553475 2.771425 2.298618 4.576609 3.591457 2.191924 5.908688
    ##  [9] 3.273711 2.480674 2.185719 3.490323 3.000219 5.872557 2.961165 2.703666
    ## [17] 2.099644 3.154093 1.288442 1.811141
    ## 
    ## $b
    ##  [1]  -5.1798434 -13.6672953  -9.2566347   7.8575173   2.3792837   0.4118214
    ##  [7]  -3.7506289   8.8779423  -1.8729683   6.1712875   9.9725688  -4.2133243
    ## [13]  -5.0019910   0.5268083  -1.8374621  -2.8688161   9.5334016  -4.1439318
    ## [19]  -8.8921936   1.1277190  -8.2706563   5.4904672   0.9262457   6.1121873
    ## [25]  -1.2340188   0.3502083   1.2679352  -2.2189831  -7.3407183  -3.9004057
    ## 
    ## $c
    ##  [1] 10.169037 10.295747 10.195639  9.651683 10.099916  9.869323  9.815789
    ##  [8] 10.079120  9.904567 10.164595  9.719434  9.874384  9.669895  9.827144
    ## [15]  9.965308 10.338993 10.237980  9.981276 10.106839 10.029256  9.464353
    ## [22] 10.074338  9.961916  9.519398 10.127616  9.944169 10.016063  9.855557
    ## [29]  9.886520 10.264737  9.610940 10.141260  9.879327  9.936263  9.963223
    ## [36]  9.917452 10.332965 10.138406  9.539865 10.292362
    ## 
    ## $d
    ##  [1] -4.275821 -4.093046 -3.586317 -3.256382 -1.687757 -2.155317 -3.072066
    ##  [8] -1.119621 -3.437603 -2.838373 -3.763886 -3.972897 -1.756176 -2.825529
    ## [15] -3.781924 -3.798481 -2.835489 -2.072200 -3.825322 -2.598349

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
    ## 1  3.07  1.22

``` r
mean_and_sd(list_norm[[2]])
```

    ## # A tibble: 1 × 2
    ##     mean    sd
    ##    <dbl> <dbl>
    ## 1 -0.755  5.99

``` r
mean_and_sd(list_norm[[3]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  9.97 0.229

``` r
mean_and_sd(list_norm[[4]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -3.04 0.903

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
output = map(list_norm, median)
```

``` r
output = map_dbl(list_norm, median, .id = "input")
```

``` r
output = map_df(list_norm, mean_and_sd, .id = "input")
```

## List columns!

``` r
listcol_df = 
  tibble(
    name = c("a", "b", "c", "d"),
    samp = list_norm
  )
```

``` r
listcol_df %>% pull(name)
```

    ## [1] "a" "b" "c" "d"

``` r
listcol_df %>% pull(samp)
```

    ## $a
    ##  [1] 2.179395 3.553475 2.771425 2.298618 4.576609 3.591457 2.191924 5.908688
    ##  [9] 3.273711 2.480674 2.185719 3.490323 3.000219 5.872557 2.961165 2.703666
    ## [17] 2.099644 3.154093 1.288442 1.811141
    ## 
    ## $b
    ##  [1]  -5.1798434 -13.6672953  -9.2566347   7.8575173   2.3792837   0.4118214
    ##  [7]  -3.7506289   8.8779423  -1.8729683   6.1712875   9.9725688  -4.2133243
    ## [13]  -5.0019910   0.5268083  -1.8374621  -2.8688161   9.5334016  -4.1439318
    ## [19]  -8.8921936   1.1277190  -8.2706563   5.4904672   0.9262457   6.1121873
    ## [25]  -1.2340188   0.3502083   1.2679352  -2.2189831  -7.3407183  -3.9004057
    ## 
    ## $c
    ##  [1] 10.169037 10.295747 10.195639  9.651683 10.099916  9.869323  9.815789
    ##  [8] 10.079120  9.904567 10.164595  9.719434  9.874384  9.669895  9.827144
    ## [15]  9.965308 10.338993 10.237980  9.981276 10.106839 10.029256  9.464353
    ## [22] 10.074338  9.961916  9.519398 10.127616  9.944169 10.016063  9.855557
    ## [29]  9.886520 10.264737  9.610940 10.141260  9.879327  9.936263  9.963223
    ## [36]  9.917452 10.332965 10.138406  9.539865 10.292362
    ## 
    ## $d
    ##  [1] -4.275821 -4.093046 -3.586317 -3.256382 -1.687757 -2.155317 -3.072066
    ##  [8] -1.119621 -3.437603 -2.838373 -3.763886 -3.972897 -1.756176 -2.825529
    ## [15] -3.781924 -3.798481 -2.835489 -2.072200 -3.825322 -2.598349

``` r
listcol_df %>% 
  filter(name == "a")
```

    ## # A tibble: 1 × 2
    ##   name  samp        
    ##   <chr> <named list>
    ## 1 a     <dbl [20]>

Let’s try some operations.

``` r
mean_and_sd(listcol_df$samp[[1]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.07  1.22

``` r
mean_and_sd(listcol_df$samp[[2]])
```

    ## # A tibble: 1 × 2
    ##     mean    sd
    ##    <dbl> <dbl>
    ## 1 -0.755  5.99

Can I just … map?

``` r
map(listcol_df$samp, mean_and_sd)
```

    ## $a
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.07  1.22
    ## 
    ## $b
    ## # A tibble: 1 × 2
    ##     mean    sd
    ##    <dbl> <dbl>
    ## 1 -0.755  5.99
    ## 
    ## $c
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  9.97 0.229
    ## 
    ## $d
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -3.04 0.903

So … can I add a list column??

``` r
 listcol_df = 
  listcol_df %>% 
  mutate(
    summary = map(samp, mean_and_sd),
    medians = map_dbl(samp, median))
```

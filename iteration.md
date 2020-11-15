Iteration
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
    ## -2.15036 -0.69837  0.09476 -0.04098  0.53324  1.94540

``` r
l$vec_numeric
```

    ## [1] 5 6 7 8

``` r
l[[1]] #gives you the first element
```

    ## [1] 5 6 7 8

``` r
mean(l[["vec_numeric"]])
```

    ## [1] 6.5

## `for` loop

create new list

``` r
list_norm = 
  list(
    a = rnorm(20, mean = 3, sd = 1),
    b = rnorm(30, mean = 0, sd = 5),
    c = rnorm(40, mean = 10, sd = .2),
    d = rnorm(20, mean = -3, sd = 1)
  )
```

``` r
list_norm
```

    ## $a
    ##  [1] 4.448248 2.167327 4.107712 4.414319 3.028813 3.796953 1.939350 3.595045
    ##  [9] 2.256440 2.179165 2.764929 3.199184 2.067154 5.007696 2.740164 1.994490
    ## [17] 3.088013 3.286399 3.294372 5.062670
    ## 
    ## $b
    ##  [1]  1.3668274  1.3806254  1.9790557 -2.8792695 -6.9079365  4.8087105
    ##  [7]  2.8215408  1.5390043 -6.7471406  0.6989719 -4.1741536  5.1221369
    ## [13]  1.4891444 -2.6056008 -1.5932769 -1.5375771 -1.4733844  4.0577307
    ## [19] -5.7239839 -4.3830080  7.2014299  1.3076911 -2.4115469  2.4505326
    ## [25]  7.3231227  1.4704686  0.9031165  7.5842124  4.0522558  6.1807034
    ## 
    ## $c
    ##  [1] 10.068264  9.927601 10.120302  9.925243  9.677581  9.935244  9.813336
    ##  [8]  9.963922 10.183696 10.068112  9.936946  9.749388  9.901220  9.780218
    ## [15]  9.659877 10.133358  9.649509  9.922683  9.745505 10.069683  9.936654
    ## [22]  9.716076 10.094706 10.054241  9.685300  9.695331 10.384996 10.241507
    ## [29] 10.371952 10.159491 10.001417 10.127087  9.742066  9.929693  9.984893
    ## [36] 10.060547  9.620602  9.721943  9.983382 10.116825
    ## 
    ## $d
    ##  [1] -3.2157334 -2.2063450 -2.2915050 -3.5247908 -3.7531774 -2.4865669
    ##  [7] -3.3243381 -2.2722295 -0.7472542 -0.6035630 -4.2685151 -3.5806461
    ## [13] -2.6095462 -2.3689994 -3.7672958 -5.2785932 -3.2797734 -0.8911933
    ## [19] -1.9951551 -3.7973072

Pause and get my old function

``` r
mean_and_sd = function(x) {
  
  if (!is.numeric(x)) {
    stop("Argument x should be numeric")
    
  if (length(x) < 3) {
    stop("Input must have at least three numbers")
    }
    
  } else if (length(x) == 1) {
    stop("Z scores cannot be computed for length 1 vectors")
  }
  
 mean_x = mean(x)
 sd_x = sd(x)
  
tibble(
  mean = mean_x,
  sd = sd_x
)

}
```

I can apply that function to each list element

``` r
mean_and_sd(list_norm[[1]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.22 0.997

``` r
mean_and_sd(list_norm[[2]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.777  4.10

``` r
mean_and_sd(list_norm[[3]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  9.95 0.199

``` r
mean_and_sd(list_norm[[4]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -2.81  1.20

Let’s use a for loop

``` r
output = vector("list", length = 4)

for (i in 1:4) {
  output[[i]] = mean_and_sd(list_norm[[i]])
}
```

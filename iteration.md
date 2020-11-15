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
    ## -2.93036 -0.56203 -0.13916 -0.01365  0.56206  3.57511

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
    ##  [1] 4.6436821 3.2354262 0.8638865 1.9976680 3.3921476 3.6515807 2.5526768
    ##  [8] 2.6640176 4.4193235 3.8913248 2.2931608 3.4835284 1.5421455 1.5263668
    ## [15] 4.6905582 5.1696617 3.1043536 1.0599987 4.1927045 3.0003555
    ## 
    ## $b
    ##  [1]  4.77362899  2.75248323 -7.97064967 -4.52126535 -0.11689056 -3.58246709
    ##  [7] -0.35747688  3.17365602 -0.45024643  4.30288922 -3.79334648  5.23500882
    ## [13] -1.73949874  5.86193381  0.11759791 -7.37529140  0.97544490 -2.51220038
    ## [19]  8.90399155  2.32076718 -0.98385493 -0.07343519  2.45076586 -1.02924639
    ## [25] -0.50447165 -1.71762642  4.97713527 11.98683293 -7.40510369  0.20905995
    ## 
    ## $c
    ##  [1] 10.170120 10.024529  9.688337 10.017051  9.919810 10.096411  9.862800
    ##  [8]  9.868848  9.699240  9.570581  9.817341  9.993772  9.948361 10.189421
    ## [15] 10.140503 10.068570 10.002050 10.168663  9.891915  9.621800 10.022237
    ## [22]  9.995576  9.858849  9.996118 10.157005  9.777281  9.889048  9.639600
    ## [29] 10.043425 10.154810  9.770389 10.213397  9.805612 10.028013  9.936850
    ## [36] 10.158638 10.327765  9.877502  9.900733  9.972360
    ## 
    ## $d
    ##  [1] -3.647251 -2.382805 -3.907984 -2.781235 -4.203083 -3.395183 -2.629025
    ##  [8] -3.743652 -4.951004 -3.012832 -4.657996 -2.609977 -5.022887 -2.903584
    ## [15] -4.285549 -2.217782 -3.328843 -3.072405 -3.911731 -1.991283

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
    ## 1  3.07  1.25

``` r
mean_and_sd(list_norm[[2]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 0.464  4.59

``` r
mean_and_sd(list_norm[[3]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  9.96 0.177

``` r
mean_and_sd(list_norm[[4]])
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1 -3.43 0.896

Let’s use a for loop

``` r
output = vector("list", length = 4)

for (i in 1:4) {
  output[[i]] = mean_and_sd(list_norm[[i]])
}
```

## Let’s try map\!

``` r
output = map(list_norm, mean_and_sd)
```

what if you want a different function?

``` r
output = map(list_norm, IQR)
```

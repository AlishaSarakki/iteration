Simulation
================

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
```

I can “simulate” by running this line.

``` r
sim_mean_sd(300000)
```

    ## # A tibble: 1 x 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  2.98  4.00

## Let’s simulate a lot

Let’s start with a for loop

``` r
output = vector("list", length = 100)

for (i in 1:100) {
  
  output[[i]] = sim_mean_sd(samp_size = 30)
}

bind_rows(output)
```

    ## # A tibble: 100 x 2
    ##     mean    sd
    ##    <dbl> <dbl>
    ##  1  3.59  3.81
    ##  2  4.14  3.66
    ##  3  3.47  3.63
    ##  4  4.31  4.03
    ##  5  2.42  4.56
    ##  6  2.73  4.49
    ##  7  3.02  3.36
    ##  8  3.58  4.10
    ##  9  2.58  4.21
    ## 10  2.97  4.75
    ## # … with 90 more rows

Let’s use a loop function.

``` r
sim_results =
  rerun(100, sim_mean_sd(samp_size = 30)) %>% 
  bind_rows()
```

Let’s look at results…

``` r
sim_results %>% 
  ggplot(aes(x = mean)) + geom_density()
```

<img src="simulation_files/figure-gfm/unnamed-chunk-5-1.png" width="90%" />

``` r
sim_results %>% 
  summarize(
    avg_sample_mean = mean(mean),
    sd_sample_mean = sd(mean)
  )
```

    ## # A tibble: 1 x 2
    ##   avg_sample_mean sd_sample_mean
    ##             <dbl>          <dbl>
    ## 1            2.87          0.732

``` r
sim_results %>% 
  ggplot(aes(x = sd)) + geom_density()
```

<img src="simulation_files/figure-gfm/unnamed-chunk-5-2.png" width="90%" />

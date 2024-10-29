Iteration and list cols
================
Zeqi Li
2024-10-29

## Lists

``` r
l = list(vec_numeric = 1:4,
         unif_sample = runif(100),
         mat = matrix(1:8,
                      nrow = 2,
                      ncol = 4,
                      byrow = TRUE),
         summary = summary(rnorm(1000)))

l$mat
```

    ##      [,1] [,2] [,3] [,4]
    ## [1,]    1    2    3    4
    ## [2,]    5    6    7    8

``` r
l[["mat"]]
```

    ##      [,1] [,2] [,3] [,4]
    ## [1,]    1    2    3    4
    ## [2,]    5    6    7    8

``` r
l[["mat"]][1, 3]
```

    ## [1] 3

``` r
l[[4]]
```

    ##     Min.  1st Qu.   Median     Mean  3rd Qu.     Max. 
    ## -4.25363 -0.56713  0.09729  0.10053  0.77036  3.37920

``` r
list_norm = list(a = rnorm(20, 0, 5),
                 b = rnorm(20, 4, 5),
                 c = rnorm(20, 0, 10),
                 d = rnorm(20, 4, 10))

list_norm[["a"]]
```

    ##  [1]  1.75732508  7.64213282 15.06110469 -3.36705060 -0.93272495 -0.91844898
    ##  [7] -6.94355907  0.51573753 -1.05673101 11.61808617  5.54478144 -3.10622750
    ## [13] -9.14939588  5.83000082 12.16134750  8.09530073 -0.02240367  8.53396864
    ## [19]  3.39363930  0.47447204

Reusing the the `mean_and_sd` function

``` r
mean_and_sd = function(x) {
  
  mean_x = mean(x)
  sd_x = sd(x)

  out_df = tibble(mean = mean_x, 
                  sd = sd_x)
  
  return(out_df)
}
```

``` r
mean_and_sd(list_norm[["a"]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  2.76  6.45

``` r
mean_and_sd(list_norm[["b"]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  4.68  4.19

``` r
mean_and_sd(list_norm[["c"]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  1.45  10.7

``` r
mean_and_sd(list_norm[["d"]])
```

    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.94  11.4

## `for` loop

``` r
output = vector("list", length = 4)

for (i in 1:4){
  output[[i]] = mean_and_sd(list_norm[[i]])
}

output
```

    ## [[1]]
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  2.76  6.45
    ## 
    ## [[2]]
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  4.68  4.19
    ## 
    ## [[3]]
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  1.45  10.7
    ## 
    ## [[4]]
    ## # A tibble: 1 × 2
    ##    mean    sd
    ##   <dbl> <dbl>
    ## 1  3.94  11.4

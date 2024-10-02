Data Manipulation
================

This document will show how to manipulate data.

Import the two datasets that we’re going to manipulate.

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.3     ✔ tidyr     1.3.1
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

## Load in the FAS Litters Data

``` r
litters_df = read_csv('data/FAS_litters.csv', na = c("NA","",".")) #in this format, gd0 and gd18 are dbl (numerical)
```

    ## Rows: 49 Columns: 8
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (2): Group, Litter Number
    ## dbl (6): GD0 weight, GD18 weight, GD of Birth, Pups born alive, Pups dead @ ...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
litters_df = janitor::clean_names(litters_df)
litters_df
```

    ## # A tibble: 49 × 8
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #3/83/3-3             NA          NA            20               9
    ##  9 Con8  #2/95/3               NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
pups_df = read_csv('data/FAS_pups.csv', na = c("NA", "", "."))
```

    ## Rows: 313 Columns: 6
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): Litter Number
    ## dbl (5): Sex, PD ears, PD eyes, PD pivot, PD walk
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
pups_df = janitor::clean_names(pups_df)
pups_df
```

    ## # A tibble: 313 × 6
    ##    litter_number   sex pd_ears pd_eyes pd_pivot pd_walk
    ##    <chr>         <dbl>   <dbl>   <dbl>    <dbl>   <dbl>
    ##  1 #85               1       4      13        7      11
    ##  2 #85               1       4      13        7      12
    ##  3 #1/2/95/2         1       5      13        7       9
    ##  4 #1/2/95/2         1       5      13        8      10
    ##  5 #5/5/3/83/3-3     1       5      13        8      10
    ##  6 #5/5/3/83/3-3     1       5      14        6       9
    ##  7 #5/4/2/95/2       1      NA      14        5       9
    ##  8 #4/2/95/3-3       1       4      13        6       8
    ##  9 #4/2/95/3-3       1       4      13        7       9
    ## 10 #2/2/95/3-2       1       4      NA        8      10
    ## # ℹ 303 more rows

``` r
#litters_df = read_csv("./data/FAS_litters.csv") #in this format, the GD0 and GD18 are character
#litters_df
```

## `select`

Use `select()` to select variables

``` r
select(litters_df, group, litter_number, gd0_weight)
```

    ## # A tibble: 49 × 3
    ##    group litter_number   gd0_weight
    ##    <chr> <chr>                <dbl>
    ##  1 Con7  #85                   19.7
    ##  2 Con7  #1/2/95/2             27  
    ##  3 Con7  #5/5/3/83/3-3         26  
    ##  4 Con7  #5/4/2/95/2           28.5
    ##  5 Con7  #4/2/95/3-3           NA  
    ##  6 Con7  #2/2/95/3-2           NA  
    ##  7 Con7  #1/5/3/83/3-3/2       NA  
    ##  8 Con8  #3/83/3-3             NA  
    ##  9 Con8  #2/95/3               NA  
    ## 10 Con8  #3/5/2/2/95           28.5
    ## # ℹ 39 more rows

``` r
select(litters_df, group:gd18_weight)
```

    ## # A tibble: 49 × 4
    ##    group litter_number   gd0_weight gd18_weight
    ##    <chr> <chr>                <dbl>       <dbl>
    ##  1 Con7  #85                   19.7        34.7
    ##  2 Con7  #1/2/95/2             27          42  
    ##  3 Con7  #5/5/3/83/3-3         26          41.4
    ##  4 Con7  #5/4/2/95/2           28.5        44.1
    ##  5 Con7  #4/2/95/3-3           NA          NA  
    ##  6 Con7  #2/2/95/3-2           NA          NA  
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA  
    ##  8 Con8  #3/83/3-3             NA          NA  
    ##  9 Con8  #2/95/3               NA          NA  
    ## 10 Con8  #3/5/2/2/95           28.5        NA  
    ## # ℹ 39 more rows

``` r
select(litters_df, -pups_survive) #delete the column pups_survive
```

    ## # A tibble: 49 × 7
    ##    group litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #3/83/3-3             NA          NA            20               9
    ##  9 Con8  #2/95/3               NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 1 more variable: pups_dead_birth <dbl>

``` r
select(litters_df, -(group:gd18_weight)) 
```

    ## # A tibble: 49 × 4
    ##    gd_of_birth pups_born_alive pups_dead_birth pups_survive
    ##          <dbl>           <dbl>           <dbl>        <dbl>
    ##  1          20               3               4            3
    ##  2          19               8               0            7
    ##  3          19               6               0            5
    ##  4          19               5               1            4
    ##  5          20               6               0            6
    ##  6          20               6               0            4
    ##  7          20               9               0            9
    ##  8          20               9               1            8
    ##  9          20               8               0            8
    ## 10          20               8               0            8
    ## # ℹ 39 more rows

Renaming columns …

``` r
select(litters_df, GROUP = group, LITTer_NUmBer = litter_number)
```

    ## # A tibble: 49 × 2
    ##    GROUP LITTer_NUmBer  
    ##    <chr> <chr>          
    ##  1 Con7  #85            
    ##  2 Con7  #1/2/95/2      
    ##  3 Con7  #5/5/3/83/3-3  
    ##  4 Con7  #5/4/2/95/2    
    ##  5 Con7  #4/2/95/3-3    
    ##  6 Con7  #2/2/95/3-2    
    ##  7 Con7  #1/5/3/83/3-3/2
    ##  8 Con8  #3/83/3-3      
    ##  9 Con8  #2/95/3        
    ## 10 Con8  #3/5/2/2/95    
    ## # ℹ 39 more rows

``` r
rename(litters_df, GROUP = group, LITTer_NUmBer = litter_number)
```

    ## # A tibble: 49 × 8
    ##    GROUP LITTer_NUmBer   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>                <dbl>       <dbl>       <dbl>           <dbl>
    ##  1 Con7  #85                   19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2             27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3         26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2           28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3           NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2           NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 Con8  #3/83/3-3             NA          NA            20               9
    ##  9 Con8  #2/95/3               NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95           28.5        NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

Select helpers

``` r
select(litters_df, starts_with("gd"))
```

    ## # A tibble: 49 × 3
    ##    gd0_weight gd18_weight gd_of_birth
    ##         <dbl>       <dbl>       <dbl>
    ##  1       19.7        34.7          20
    ##  2       27          42            19
    ##  3       26          41.4          19
    ##  4       28.5        44.1          19
    ##  5       NA          NA            20
    ##  6       NA          NA            20
    ##  7       NA          NA            20
    ##  8       NA          NA            20
    ##  9       NA          NA            20
    ## 10       28.5        NA            20
    ## # ℹ 39 more rows

``` r
select(litters_df, contains("pups"))
```

    ## # A tibble: 49 × 3
    ##    pups_born_alive pups_dead_birth pups_survive
    ##              <dbl>           <dbl>        <dbl>
    ##  1               3               4            3
    ##  2               8               0            7
    ##  3               6               0            5
    ##  4               5               1            4
    ##  5               6               0            6
    ##  6               6               0            4
    ##  7               9               0            9
    ##  8               9               1            8
    ##  9               8               0            8
    ## 10               8               0            8
    ## # ℹ 39 more rows

``` r
select(litters_df, litter_number, gd0_weight, everything()) #move litter_number and gd0 to beginning
```

    ## # A tibble: 49 × 8
    ##    litter_number   gd0_weight group gd18_weight gd_of_birth pups_born_alive
    ##    <chr>                <dbl> <chr>       <dbl>       <dbl>           <dbl>
    ##  1 #85                   19.7 Con7         34.7          20               3
    ##  2 #1/2/95/2             27   Con7         42            19               8
    ##  3 #5/5/3/83/3-3         26   Con7         41.4          19               6
    ##  4 #5/4/2/95/2           28.5 Con7         44.1          19               5
    ##  5 #4/2/95/3-3           NA   Con7         NA            20               6
    ##  6 #2/2/95/3-2           NA   Con7         NA            20               6
    ##  7 #1/5/3/83/3-3/2       NA   Con7         NA            20               9
    ##  8 #3/83/3-3             NA   Con8         NA            20               9
    ##  9 #2/95/3               NA   Con8         NA            20               8
    ## 10 #3/5/2/2/95           28.5 Con8         NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
relocate(litters_df, litter_number, gd0_weight) #relocate to the beginning
```

    ## # A tibble: 49 × 8
    ##    litter_number   gd0_weight group gd18_weight gd_of_birth pups_born_alive
    ##    <chr>                <dbl> <chr>       <dbl>       <dbl>           <dbl>
    ##  1 #85                   19.7 Con7         34.7          20               3
    ##  2 #1/2/95/2             27   Con7         42            19               8
    ##  3 #5/5/3/83/3-3         26   Con7         41.4          19               6
    ##  4 #5/4/2/95/2           28.5 Con7         44.1          19               5
    ##  5 #4/2/95/3-3           NA   Con7         NA            20               6
    ##  6 #2/2/95/3-2           NA   Con7         NA            20               6
    ##  7 #1/5/3/83/3-3/2       NA   Con7         NA            20               9
    ##  8 #3/83/3-3             NA   Con8         NA            20               9
    ##  9 #2/95/3               NA   Con8         NA            20               8
    ## 10 #3/5/2/2/95           28.5 Con8         NA            20               8
    ## # ℹ 39 more rows
    ## # ℹ 2 more variables: pups_dead_birth <dbl>, pups_survive <dbl>

``` r
select(pups_df, litter_number, sex, pd_ears)
```

    ## # A tibble: 313 × 3
    ##    litter_number   sex pd_ears
    ##    <chr>         <dbl>   <dbl>
    ##  1 #85               1       4
    ##  2 #85               1       4
    ##  3 #1/2/95/2         1       5
    ##  4 #1/2/95/2         1       5
    ##  5 #5/5/3/83/3-3     1       5
    ##  6 #5/5/3/83/3-3     1       5
    ##  7 #5/4/2/95/2       1      NA
    ##  8 #4/2/95/3-3       1       4
    ##  9 #4/2/95/3-3       1       4
    ## 10 #2/2/95/3-2       1       4
    ## # ℹ 303 more rows

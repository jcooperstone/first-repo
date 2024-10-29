# My first GitHub document
Jessica Cooperstone
2024-10-28

# Load libraries

Let’s add some material to our document so we can better see what our
resulting documents will look like. This will also give us an
opportunity to practice some of what we’ve been going over in Code Club
this semester.

``` r
library(tidyverse)
```

    ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ✔ dplyr     1.1.3     ✔ readr     2.1.4
    ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ✔ ggplot2   3.4.4     ✔ tibble    3.2.1
    ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ✔ purrr     1.0.2     
    ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ✖ dplyr::filter() masks stats::filter()
    ✖ dplyr::lag()    masks stats::lag()
    ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

# Download data

Let’s go back to what we started with this semester. Let’s revisit data
from [The World Factbook](https://www.cia.gov/the-world-factbook/), put
together by the CIA to “provides basic intelligence on the history,
people, government, economy, energy, geography, environment,
communications, transportation, military, terrorism, and transnational
issues for 265 world entities.” I thought this data would give us some
opportunities to flex our R skills, and learn a bit about the world.

The data we are going to download can be found
[here](https://www.cia.gov/the-world-factbook/field/population/country-comparison/),
though I have saved the file, added it to our Code Club Github, and
included some code below for you to download it. This is a little bit
different than the data we started with which included only info from
2015. This dataset includes many more years.

``` r
download.file(
  url = "https://github.com/osu-codeclub/osu-codeclub.github.io/raw/refs/heads/main/posts/S08E01_wrangling_01/data/factbook.csv",
  destfile = "factbook_download.csv"
)
```

You should now see the file “factbook_download.csv” in your working
directory.

# Read in data

We can read it in using the tidyverse function from the
[`readr`](https://readr.tidyverse.org/index.html) package called
[`read_csv()`](https://readr.tidyverse.org/reference/read_delim.html).

``` r
# i've stored mine in a folder called data for organizational sake
factbook <- read_csv("data/factbook_download.csv")
```

    Rows: 11072 Columns: 20
    ── Column specification ────────────────────────────────────────────────────────
    Delimiter: ","
    chr (20): Series Name, Series Code, Country Name, Country Code, 2000 [YR2000...

    ℹ Use `spec()` to retrieve the full column specification for this data.
    ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

Let’s look at our data.

``` r
View(factbook)
```

# Wrangle

Let’s pull just the data for total population.

``` r
factbook_pop <- factbook |> 
  filter(`Series Name` == "Population, total")
```

And then we can look at it:

``` r
head(factbook_pop)
```

| Series Name       | Series Code | Country Name   | Country Code | 2000 \[YR2000\] | 2001 \[YR2001\] | 2002 \[YR2002\] | 2003 \[YR2003\] | 2004 \[YR2004\] | 2005 \[YR2005\] | 2006 \[YR2006\] | 2007 \[YR2007\] | 2008 \[YR2008\] | 2009 \[YR2009\] | 2010 \[YR2010\] | 2011 \[YR2011\] | 2012 \[YR2012\] | 2013 \[YR2013\] | 2014 \[YR2014\] | 2015 \[YR2015\] |
|:------------------|:------------|:---------------|:-------------|:----------------|:----------------|:----------------|:----------------|:----------------|:----------------|:----------------|:----------------|:----------------|:----------------|:----------------|:----------------|:----------------|:----------------|:----------------|:----------------|
| Population, total | SP.POP.TOTL | Afghanistan    | AFG          | 19542982        | 19688632        | 21000256        | 22645130        | 23553551        | 24411191        | 25442944        | 25903301        | 26427199        | 27385307        | 28189672        | 29249157        | 30466479        | 31541209        | 32716210        | 33753499        |
| Population, total | SP.POP.TOTL | Albania        | ALB          | 3089027         | 3060173         | 3051010         | 3039616         | 3026939         | 3011487         | 2992547         | 2970017         | 2947314         | 2927519         | 2913021         | 2905195         | 2900401         | 2895092         | 2889104         | 2880703         |
| Population, total | SP.POP.TOTL | Algeria        | DZA          | 30774621        | 31200985        | 31624696        | 32055883        | 32510186        | 32956690        | 33435080        | 33983827        | 34569592        | 35196037        | 35856344        | 36543541        | 37260563        | 38000626        | 38760168        | 39543154        |
| Population, total | SP.POP.TOTL | American Samoa | ASM          | 58230           | 58324           | 58177           | 57941           | 57626           | 57254           | 56837           | 56383           | 55891           | 55366           | 54849           | 54310           | 53691           | 52995           | 52217           | 51368           |
| Population, total | SP.POP.TOTL | Andorra        | AND          | 66097           | 67820           | 70849           | 73907           | 76933           | 79826           | 80221           | 78168           | 76055           | 73852           | 71519           | 70567           | 71013           | 71367           | 71621           | 71746           |
| Population, total | SP.POP.TOTL | Angola         | AGO          | 16394062        | 16941587        | 17516139        | 18124342        | 18771125        | 19450959        | 20162340        | 20909684        | 21691522        | 22507674        | 23364185        | 24259111        | 25188292        | 26147002        | 27128337        | 28127721        |

``` r
glimpse(factbook_pop)
```

    Rows: 217
    Columns: 20
    $ `Series Name`   <chr> "Population, total", "Population, total", "Population,…
    $ `Series Code`   <chr> "SP.POP.TOTL", "SP.POP.TOTL", "SP.POP.TOTL", "SP.POP.T…
    $ `Country Name`  <chr> "Afghanistan", "Albania", "Algeria", "American Samoa",…
    $ `Country Code`  <chr> "AFG", "ALB", "DZA", "ASM", "AND", "AGO", "ATG", "ARG"…
    $ `2000 [YR2000]` <chr> "19542982", "3089027", "30774621", "58230", "66097", "…
    $ `2001 [YR2001]` <chr> "19688632", "3060173", "31200985", "58324", "67820", "…
    $ `2002 [YR2002]` <chr> "21000256", "3051010", "31624696", "58177", "70849", "…
    $ `2003 [YR2003]` <chr> "22645130", "3039616", "32055883", "57941", "73907", "…
    $ `2004 [YR2004]` <chr> "23553551", "3026939", "32510186", "57626", "76933", "…
    $ `2005 [YR2005]` <chr> "24411191", "3011487", "32956690", "57254", "79826", "…
    $ `2006 [YR2006]` <chr> "25442944", "2992547", "33435080", "56837", "80221", "…
    $ `2007 [YR2007]` <chr> "25903301", "2970017", "33983827", "56383", "78168", "…
    $ `2008 [YR2008]` <chr> "26427199", "2947314", "34569592", "55891", "76055", "…
    $ `2009 [YR2009]` <chr> "27385307", "2927519", "35196037", "55366", "73852", "…
    $ `2010 [YR2010]` <chr> "28189672", "2913021", "35856344", "54849", "71519", "…
    $ `2011 [YR2011]` <chr> "29249157", "2905195", "36543541", "54310", "70567", "…
    $ `2012 [YR2012]` <chr> "30466479", "2900401", "37260563", "53691", "71013", "…
    $ `2013 [YR2013]` <chr> "31541209", "2895092", "38000626", "52995", "71367", "…
    $ `2014 [YR2014]` <chr> "32716210", "2889104", "38760168", "52217", "71621", "…
    $ `2015 [YR2015]` <chr> "33753499", "2880703", "39543154", "51368", "71746", "…

## Pivot

Looks like our year columns are characters, let’s convert them to be
numeric, and in the process practice pivoting.

``` r
factbook_pop_long <- factbook_pop |> 
  pivot_longer(cols = starts_with("2"), # pick columns start with 2
               names_to = "year", # take names to new col "year"
               values_to = "pop") |> # values in cells to new col "pop"
  mutate(year = parse_number(year)) |> # use mutate to remove extra year garbage
  mutate(pop = as.numeric(pop)) # convert pop to be numeric

glimpse(factbook_pop_long)
```

    Rows: 3,472
    Columns: 6
    $ `Series Name`  <chr> "Population, total", "Population, total", "Population, …
    $ `Series Code`  <chr> "SP.POP.TOTL", "SP.POP.TOTL", "SP.POP.TOTL", "SP.POP.TO…
    $ `Country Name` <chr> "Afghanistan", "Afghanistan", "Afghanistan", "Afghanist…
    $ `Country Code` <chr> "AFG", "AFG", "AFG", "AFG", "AFG", "AFG", "AFG", "AFG",…
    $ year           <dbl> 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2…
    $ pop            <dbl> 19542982, 19688632, 21000256, 22645130, 23553551, 24411…

Now that we’ve cleaned that up, let’s go back wide to calculate which
country had the largest percent population growth from 2000 to 2015.

Go wide! And let’s clean up those column names at the same time.

``` r
factbook_pop_wide <- factbook_pop_long |> 
  pivot_wider(names_from = year, # go from long to wide data
              values_from = pop) |> 
  janitor::clean_names()
```

## Calculate percent population growth

Let’s now see which country had the largest percent population growth
from 2000 to 2015.

``` r
factbook_pop_wide |> 
  mutate(perc_pop_growth = ((x2015 - x2000)/x2000 * 100)) |> 
  mutate(perc_pop_growth = round(perc_pop_growth, digits = 1)) |> 
  select(country_name, perc_pop_growth, x2000, x2015) |> # pull only the columns we want
  slice_max(perc_pop_growth, n = 5) # pick top 5
```

    # A tibble: 5 × 4
      country_name             perc_pop_growth   x2000   x2015
      <chr>                              <dbl>   <dbl>   <dbl>
    1 Qatar                              274.   645937 2414573
    2 United Arab Emirates               172.  3275333 8916899
    3 Kuwait                             102   1934901 3908743
    4 Equatorial Guinea                   96.6  684977 1346973
    5 Turks and Caicos Islands            94.9   18744   36538

And which country had the smallest percent population growth from 2000
to 2015.

``` r
factbook_pop_wide |> 
  mutate(perc_pop_growth = ((x2015 - x2000)/x2000 * 100)) |> 
  select(country_name, perc_pop_growth, x2000, x2015) |> # pull only the columns we want
  slice_min(perc_pop_growth, n = 5) # pick lowest 5
```

    # A tibble: 5 × 4
      country_name             perc_pop_growth   x2000   x2015
      <chr>                              <dbl>   <dbl>   <dbl>
    1 Northern Mariana Islands           -35.9   80338   51514
    2 Lithuania                          -17.0 3499536 2904910
    3 Latvia                             -16.5 2367550 1977527
    4 Bosnia and Herzegovina             -15.7 4179350 3524324
    5 Bulgaria                           -12.1 8170172 7177991

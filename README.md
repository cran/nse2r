
<!-- README.md is generated from README.Rmd. Please edit that file -->

# nse2r

> Fetch data from the National Stock Exchange, India.

<!-- badges: start -->

[![CRAN\_Status\_Badge](https://www.r-pkg.org/badges/version/nse2r)](https://cran.r-project.org/package=nse2r)
[![cran
checks](https://cranchecks.info/badges/summary/nse2r)](https://cran.r-project.org/web/checks/check_results_nse2r.html)
[![Travis-CI Build
Status](https://travis-ci.org/rsquaredacademy/nse2r.svg?branch=master)](https://travis-ci.org/rsquaredacademy/nse2r)
[![AppVeyor Build
Status](https://ci.appveyor.com/api/projects/status/github/rsquaredacademy/nse2r?branch=master&svg=true)](https://ci.appveyor.com/project/rsquaredacademy/nse2r)
[![Coverage
Status](https://img.shields.io/codecov/c/github/rsquaredacademy/nse2r/master.svg)](https://codecov.io/github/rsquaredacademy/nse2r?branch=master)
[![Lifecycle:
experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://www.tidyverse.org/lifecycle/#experimental)
[![](https://cranlogs.r-pkg.org/badges/grand-total/nse2r)](https://cran.r-project.org/package=nse2r)
<!-- badges: end -->

## Overview

[NSE](https://www.nseindia.com/) (National Stock Exchange) is the
leading stock exchange of India, located in the city of Mumbai. While
users can manually download data from NSE through a browser, importing
this data into R becomes cumbersome. The nse2r R package implements the
retrieval of data from NSE and aims to reduce the pre-processing steps
needed in analyzing such data.

nse2r is inspired by and a port of the Python package
[nsetools](https://nsetools.readthedocs.io/en/latest/). The authors and
contributors for this R package are not affiliated with NSE and NSE does
not offer support for this R package.

With nse2r, you can fetch the following data related to:

  - stocks
      - quote for a given stock
      - stock description
      - validate stock symbol/ticker
      - most actively traded stocks in a month
      - 52 week high/low
      - top gainers/losers for the last trading session
  - index
      - list of NSE indices
      - validate index symbol/ticker
      - quote for a given index
  - futures & options
      - top gainers/losers for the last trading session
  - pre open market data
      - nifty
      - nifty bank
  - indices advances & declines

## Installation

You can install the development version of nse2r from
[GitHub](https://github.com/rsquaredacademy/nse2r/) with:

``` r
# install.packages("devtools")
devtools::install_github("rsquaredacademy/nse2r")
```

## Usage

nse2r uses consistent prefix `nse_` for easy tab completion.

  - `nse_index_` for index
  - `nse_stock_` for stocks
  - `nse_fo_` for futures and options
  - `nse_preopen_` for preopen data

## Preprocessing

nse2r does basic data preprocessing which are listed below:

  - modify column data types from `character` to `numeric` and `Date`
  - modify column names
      - make them more descriptive
      - to `snake_case` from `camelCase`

Users can retain the names and format as returned by NSE using the
`clean_names` argument and setting it to `FALSE`.

### Index

##### Fetch Indices Quote

``` r
nse_index_quote()
#> # A tibble: 55 x 4
#>    index_name        last_traded_price change percent_change
#>    <chr>                         <dbl>  <dbl>          <dbl>
#>  1 NIFTY 50 Pre Open           12079.   86.0            0.72
#>  2 NIFTY 50                    12053.   59.9            0.5 
#>  3 NIFTY NEXT 50               28101.  206.             0.74
#>  4 NIFTY100 LIQ 15              3743.   10.3            0.28
#>  5 NIFTY BANK                  31399.  162.             0.52
#>  6 INDIA VIX                      14.6  -0.23          -1.53
#>  7 NIFTY 100                   12155.   64.4            0.53
#>  8 NIFTY 500                    9805.   58              0.6 
#>  9 NIFTY MIDCAP 100            17022.  117.             0.69
#> 10 NIFTY MIDCAP 50              4675.   35.4            0.76
#> # ... with 45 more rows

# retain original column names as returned by NSE
nse_index_quote(clean_names = FALSE)
#> # A tibble: 55 x 4
#>    name              lastPrice change pChange
#>    <chr>                 <dbl>  <dbl>   <dbl>
#>  1 NIFTY 50 Pre Open   12079.   86.0     0.72
#>  2 NIFTY 50            12053.   59.9     0.5 
#>  3 NIFTY NEXT 50       28101.  206.      0.74
#>  4 NIFTY100 LIQ 15      3743.   10.3     0.28
#>  5 NIFTY BANK          31399.  162.      0.52
#>  6 INDIA VIX              14.6  -0.23   -1.53
#>  7 NIFTY 100           12155.   64.4     0.53
#>  8 NIFTY 500            9805.   58       0.6 
#>  9 NIFTY MIDCAP 100    17022.  117.      0.69
#> 10 NIFTY MIDCAP 50      4675.   35.4     0.76
#> # ... with 45 more rows
```

### Stock

##### Top gainers for the last trading session.

``` r
nse_stock_top_gainers()
#> # A tibble: 10 x 12
#>    symbol series last_corp_annou~ last_corp_annou~ open_price high_price
#>    <chr>  <chr>  <date>           <chr>                 <dbl>      <dbl>
#>  1 VEDL   EQ     2019-07-04       Annual General ~       153.       157.
#>  2 ZEEL   EQ     2019-07-15       Annual General ~       265        271.
#>  3 ULTRA~ EQ     2019-07-10       Annual General ~      4200.      4254 
#>  4 UPL    EQ     2019-07-02       Bonus 1:2              585.       604 
#>  5 RELIA~ EQ     2019-08-02       Annual General ~      1519       1534.
#>  6 HDFCB~ EQ     2019-09-19       Face Value Spli~      1259.      1271.
#>  7 SUNPH~ EQ     2019-08-20       Annual General ~       441.       448 
#>  8 NTPC   EQ     2019-08-13       Dividend - Rs 2~       119.       122.
#>  9 HDFC   EQ     2019-07-19       Annual General ~      2401.      2429.
#> 10 ASIAN~ EQ     2019-10-30       Interim Dividen~      1711       1740.
#> # ... with 6 more variables: low_price <dbl>, last_traded_price <dbl>,
#> #   prev_close_price <dbl>, percent_change <dbl>, traded_quantity <dbl>,
#> #   turnover_in_lakhs <dbl>

# retain original column names as returned by NSE
nse_stock_top_gainers(clean_names = FALSE)
#> # A tibble: 10 x 12
#>    symbol series lastCorpAnnounc~ lastCorpAnnounc~ openPrice highPrice
#>    <chr>  <chr>  <date>           <chr>                <dbl>     <dbl>
#>  1 VEDL   EQ     2019-07-04       Annual General ~      153.      157.
#>  2 ZEEL   EQ     2019-07-15       Annual General ~      265       271.
#>  3 ULTRA~ EQ     2019-07-10       Annual General ~     4200.     4254 
#>  4 UPL    EQ     2019-07-02       Bonus 1:2             585.      604 
#>  5 RELIA~ EQ     2019-08-02       Annual General ~     1519      1534.
#>  6 HDFCB~ EQ     2019-09-19       Face Value Spli~     1259.     1271.
#>  7 SUNPH~ EQ     2019-08-20       Annual General ~      441.      448 
#>  8 NTPC   EQ     2019-08-13       Dividend - Rs 2~      119.      122.
#>  9 HDFC   EQ     2019-07-19       Annual General ~     2401.     2429.
#> 10 ASIAN~ EQ     2019-10-30       Interim Dividen~     1711      1740.
#> # ... with 6 more variables: lowPrice <dbl>, ltp <dbl>,
#> #   previousPrice <dbl>, netPrice <dbl>, tradedQuantity <dbl>,
#> #   turnoverInLakhs <dbl>
```

##### Stocks that have touched their 52 week highs during the day

``` r
nse_stock_year_high()
#> # A tibble: 27 x 10
#>    symbol symbol_desc date       new_high   year last_traded_pri~ prev_high
#>    <chr>  <chr>       <date>        <dbl>  <dbl>            <dbl>     <dbl>
#>  1 AAVAS  Aavas Fina~ 2020-01-03   2079   2079             1970.     2050. 
#>  2 ADANI~ Adani Gree~ 2020-01-06    211.   211.             211.      202. 
#>  3 ALKYL~ Alkyl Amin~ 2020-01-02   1250   1250             1234      1199  
#>  4 ASTER~ Aster DM H~ 2020-01-01    175.   175.             163.      171. 
#>  5 BALRA~ Balrampur ~ 2020-01-02    195    195              186.      189. 
#>  6 BRIGA~ Brigade En~ 2019-11-08    232.   232.             223.      224. 
#>  7 DIXON  Dixon Tech~ 2019-12-27   4315.  4315.            4240      4055  
#>  8 DWARK~ Dwarikesh ~ 2020-01-02     42     42               41.7      39.8
#>  9 EIDPA~ EID Parry ~ 2019-01-16    235    235              230.      233. 
#> 10 GMRIN~ GMR Infras~ 2020-01-03     23.8   23.8             23.2      23.4
#> # ... with 17 more rows, and 3 more variables: prev_close <dbl>,
#> #   change <dbl>, percent_change <dbl>

# retain original column names as returned by NSE
nse_stock_year_high(clean_names = FALSE)
#> # A tibble: 27 x 10
#>    symbol symbolDesc dt          value   year    ltp value_old   prev
#>    <chr>  <chr>      <date>      <dbl>  <dbl>  <dbl>     <dbl>  <dbl>
#>  1 AAVAS  Aavas Fin~ 2020-01-03 2079   2079   1970.     2050.  1990. 
#>  2 ADANI~ Adani Gre~ 2020-01-06  211.   211.   211.      202.   201. 
#>  3 ALKYL~ Alkyl Ami~ 2020-01-02 1250   1250   1234      1199   1142. 
#>  4 ASTER~ Aster DM ~ 2020-01-01  175.   175.   163.      171.   166. 
#>  5 BALRA~ Balrampur~ 2020-01-02  195    195    186.      189.   183. 
#>  6 BRIGA~ Brigade E~ 2019-11-08  232.   232.   223.      224.   218. 
#>  7 DIXON  Dixon Tec~ 2019-12-27 4315.  4315.  4240      4055   3959. 
#>  8 DWARK~ Dwarikesh~ 2020-01-02   42     42     41.7      39.8   38.4
#>  9 EIDPA~ EID Parry~ 2019-01-16  235    235    230.      233.   224. 
#> 10 GMRIN~ GMR Infra~ 2020-01-03   23.8   23.8   23.2      23.4   22.6
#> # ... with 17 more rows, and 2 more variables: change <dbl>, pChange <dbl>
```

##### Most actively traded stocks in a month

``` r
nse_stock_most_traded()
#> # A tibble: 12 x 6
#>    security share_turnover traded_quantity no_of_trades avg_daily_turno~
#>    <chr>             <dbl>           <dbl>        <dbl>            <dbl>
#>  1 Yes Ban~           4.38           57140     11058530            1423.
#>  2 Relianc~           3.93            1715      3803882            1276.
#>  3 Indiabu~           3.91            9077      8060572            1271.
#>  4 State B~           3.43            7114      4624946            1114.
#>  5 Tata Co~           2.69             866      2891204             875.
#>  6 ICICI B~           2.51            3204      2969145             814.
#>  7 HDFC Li~           2.33             670      2510572             756.
#>  8 Tata St~           2.26            3541      3008166             733.
#>  9 HDFC Ba~           2.18            1170      2969084             707.
#> 10 Tata Mo~           2.07            8128      3536571             671.
#> 11 TOTAL o~          29.7            92625     45432672            9640.
#> 12 TOTAL            100             391115    223723721           32475.
#> # ... with 1 more variable: turnover <dbl>

# retain original column names as returned by NSE
nse_stock_most_traded(clean_names = FALSE)
#> # A tibble: 12 x 6
#>    security              sharetotal trdQty nooftrades avgdailyturn turnover
#>    <chr>                      <dbl>  <dbl>      <dbl>        <dbl>    <dbl>
#>  1 Yes Bank Limited            4.38  57140   11058530        1423.   29880.
#>  2 Reliance Industries ~       3.93   1715    3803882        1276.   26799.
#>  3 Indiabulls Hsg Fin L~       3.91   9077    8060572        1271.   26683.
#>  4 State Bank of India         3.43   7114    4624946        1114.   23391.
#>  5 Tata Consultancy Ser~       2.69    866    2891204         875.   18367.
#>  6 ICICI Bank Limited          2.51   3204    2969145         814.   17098.
#>  7 HDFC Limited                2.33    670    2510572         756.   15868.
#>  8 Tata Steel Limited          2.26   3541    3008166         733.   15396.
#>  9 HDFC Bank Limited           2.18   1170    2969084         707.   14848.
#> 10 Tata Motors Limited         2.07   8128    3536571         671.   14100.
#> 11 TOTAL of Top Ten sec~      29.7   92625   45432672        9640.  202431.
#> 12 TOTAL                     100    391115  223723721       32475.  681983.
```

### Futures & Options

##### Top futures and options gainers for the last trading session.

``` r
nse_fo_top_gainers()
#> # A tibble: 10 x 12
#>    symbol series last_corp_annou~ last_corp_annou~ open_price high_price
#>    <chr>  <chr>  <date>           <chr>                 <dbl>      <dbl>
#>  1 RAMCO~ EQ     2019-07-31       Annual General ~      755        793  
#>  2 SHREE~ EQ     2019-07-31       Dividend - Rs 3~    21097.     22050  
#>  3 VEDL   EQ     2019-07-04       Annual General ~      153.       157. 
#>  4 PFC    EQ     2019-08-20       Annual General ~      114        119. 
#>  5 L&TFH  EQ     2019-07-19       Annual General ~      114        117  
#>  6 MINDT~ EQ     2019-10-24       Interim Dividen~      823.       854  
#>  7 INDIGO EQ     2019-08-19       Annual General ~     1327.      1384  
#>  8 MOTHE~ EQ     2019-08-08       Annual General ~      143        147. 
#>  9 GMRIN~ EQ     2019-09-05       Annual General ~       22.8       23.8
#> 10 ZEEL   EQ     2019-07-15       Annual General ~      265        271. 
#> # ... with 6 more variables: low_price <dbl>, last_traded_price <dbl>,
#> #   prev_close_price <dbl>, percent_change <dbl>, traded_quantity <dbl>,
#> #   turnover_in_lakhs <dbl>

# retain original column names as returned by NSE
nse_fo_top_gainers(clean_names = FALSE)
#> # A tibble: 10 x 12
#>    symbol series lastCorpAnnounc~ lastCorpAnnounc~ openPrice highPrice
#>    <chr>  <chr>  <date>           <chr>                <dbl>     <dbl>
#>  1 RAMCO~ EQ     2019-07-31       Annual General ~     755       793  
#>  2 SHREE~ EQ     2019-07-31       Dividend - Rs 3~   21097.    22050  
#>  3 VEDL   EQ     2019-07-04       Annual General ~     153.      157. 
#>  4 PFC    EQ     2019-08-20       Annual General ~     114       119. 
#>  5 L&TFH  EQ     2019-07-19       Annual General ~     114       117  
#>  6 MINDT~ EQ     2019-10-24       Interim Dividen~     823.      854  
#>  7 INDIGO EQ     2019-08-19       Annual General ~    1327.     1384  
#>  8 MOTHE~ EQ     2019-08-08       Annual General ~     143       147. 
#>  9 GMRIN~ EQ     2019-09-05       Annual General ~      22.8      23.8
#> 10 ZEEL   EQ     2019-07-15       Annual General ~     265       271. 
#> # ... with 6 more variables: lowPrice <dbl>, ltp <dbl>,
#> #   previousPrice <dbl>, netPrice <dbl>, tradedQuantity <dbl>,
#> #   turnoverInLakhs <dbl>
```

### Pre Open Market Data

##### Fetch data of pre open session of Nifty Bank.

``` r
nse_preopen_nifty_bank()
#> # A tibble: 12 x 17
#>    symbol series corp_action_date corp_action  price change percent_change
#>    <chr>  <chr>  <date>           <chr>        <dbl>  <dbl>          <dbl>
#>  1 BANKB~ EQ     NA               <NA>          97.6   1.8            1.88
#>  2 RBLBA~ EQ     NA               <NA>         343     6.15           1.83
#>  3 SBIN   EQ     NA               <NA>         324.    5.45           1.71
#>  4 HDFCB~ EQ     NA               <NA>        1259.   18.0            1.45
#>  5 INDUS~ EQ     NA               <NA>        1488.   19.0            1.3 
#>  6 YESBA~ EQ     NA               <NA>          45.7   0.55           1.22
#>  7 PNB    EQ     NA               <NA>          62.1   0.7            1.14
#>  8 ICICI~ EQ     NA               <NA>         531.    5.6            1.07
#>  9 IDFCF~ EQ     NA               <NA>          44     0.35           0.8 
#> 10 FEDER~ EQ     NA               <NA>          87.8   0.7            0.8 
#> 11 AXISB~ EQ     NA               <NA>         728     4.75           0.66
#> 12 KOTAK~ EQ     NA               <NA>        1661.    8.5            0.51
#> # ... with 10 more variables: prev_close <dbl>, quantity <dbl>,
#> #   value <dbl>, mkt_cap <dbl>, year_high <dbl>, year_low <dbl>,
#> #   sum_val <dbl>, sum_quantity <dbl>, fin_quantity <dbl>,
#> #   sum_fin_quantity <dbl>

# retain original column names as returned by NSE
nse_preopen_nifty(clean_names = FALSE)
#> # A tibble: 50 x 17
#>    symbol series xDt        caAct    iep   chn perChn   pCls trdQnty   iVal
#>    <chr>  <chr>  <date>     <chr>  <dbl> <dbl>  <dbl>  <dbl>   <dbl>  <dbl>
#>  1 SBIN   EQ     NA         <NA>   324.   5.45   1.71  319    119226  387. 
#>  2 VEDL   EQ     NA         <NA>   153.   2.25   1.49  151.    29896   45.7
#>  3 BAJFI~ EQ     NA         <NA>  4055   58.3    1.46 3997.     5803  235. 
#>  4 HDFCB~ EQ     NA         <NA>  1259.  18.0    1.45 1241.    95521 1203. 
#>  5 ZEEL   EQ     NA         <NA>   265    3.5    1.34  262.    37585   99.6
#>  6 INDUS~ EQ     NA         <NA>  1488.  19.0    1.3  1469.     8382  125. 
#>  7 YESBA~ EQ     NA         <NA>    45.7  0.55   1.22   45.2  186780   85.4
#>  8 RELIA~ EQ     NA         <NA>  1519   17.5    1.17 1502.    36027  547. 
#>  9 TITAN  EQ     NA         <NA>  1171.  12.4    1.07 1159.     7974   93.4
#> 10 ICICI~ EQ     NA         <NA>   531.   5.6    1.07  526.    32942  175. 
#> # ... with 40 more rows, and 7 more variables: mktCap <dbl>, yHigh <dbl>,
#> #   yLow <dbl>, sumVal <dbl>, sumQnty <dbl>, finQnty <dbl>,
#> #   sumfinQnty <dbl>
```

### Advances & Declines

``` r
nse_advances_declines()
#> # A tibble: 57 x 4
#>    index_name      advances declines unchanged
#>    <chr>              <dbl>    <dbl>     <dbl>
#>  1 NIFTY 50              33       17         0
#>  2 NIFTY NEXT 50         34       15         1
#>  3 NIFTY IT               8        2         0
#>  4 NIFTY BANK             7        4         1
#>  5 NIFTY MIDCAP 50       36       12         2
#>  6 NIFTY INFRA           18       12         0
#>  7 NIFTY REALTY           9        1         0
#>  8 NIFTY ENERGY           3        7         0
#>  9 NIFTY FMCG            10        5         0
#> 10 NIFTY MNC             19       11         0
#> # ... with 47 more rows

# retain original column names as returned by NSE
nse_advances_declines(clean_names = FALSE)
#> # A tibble: 57 x 4
#>    indice          advances declines unchanged
#>    <chr>              <dbl>    <dbl>     <dbl>
#>  1 NIFTY 50              33       17         0
#>  2 NIFTY NEXT 50         34       15         1
#>  3 NIFTY IT               8        2         0
#>  4 NIFTY BANK             7        4         1
#>  5 NIFTY MIDCAP 50       36       12         2
#>  6 NIFTY INFRA           18       12         0
#>  7 NIFTY REALTY           9        1         0
#>  8 NIFTY ENERGY           3        7         0
#>  9 NIFTY FMCG            10        5         0
#> 10 NIFTY MNC             19       11         0
#> # ... with 47 more rows
```

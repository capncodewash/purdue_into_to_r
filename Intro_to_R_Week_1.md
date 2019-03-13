Intro to R - Week 1
================

# Introduction to R for Data Science (FutureLearn) - Week 1

By Graeme West

This notebook covers the material in Week 1 of [Introduction to R for
Data Science](https://www.futurelearn.com/courses/data-science/5) by
Purdue University on FutureLearn.

The subject matter of the data is airline flight data from the United
States. Week 1 covers basic setup, exploratory data analysis, selecting
data, and basic plotting.

## Step 1.12

Read in the basic 2008 data (this takes a couple of minutes):

``` r
myDF <- read.csv("./datasets/2008.csv.bz2")
```

Phew, that was tough\! Let’s try and make heads and tails of
    it…

``` r
head(myDF)
```

    ##   Year Month DayofMonth DayOfWeek DepTime CRSDepTime ArrTime CRSArrTime
    ## 1 2008     1          3         4    2003       1955    2211       2225
    ## 2 2008     1          3         4     754        735    1002       1000
    ## 3 2008     1          3         4     628        620     804        750
    ## 4 2008     1          3         4     926        930    1054       1100
    ## 5 2008     1          3         4    1829       1755    1959       1925
    ## 6 2008     1          3         4    1940       1915    2121       2110
    ##   UniqueCarrier FlightNum TailNum ActualElapsedTime CRSElapsedTime AirTime
    ## 1            WN       335  N712SW               128            150     116
    ## 2            WN      3231  N772SW               128            145     113
    ## 3            WN       448  N428WN                96             90      76
    ## 4            WN      1746  N612SW                88             90      78
    ## 5            WN      3920  N464WN                90             90      77
    ## 6            WN       378  N726SW               101            115      87
    ##   ArrDelay DepDelay Origin Dest Distance TaxiIn TaxiOut Cancelled
    ## 1      -14        8    IAD  TPA      810      4       8         0
    ## 2        2       19    IAD  TPA      810      5      10         0
    ## 3       14        8    IND  BWI      515      3      17         0
    ## 4       -6       -4    IND  BWI      515      3       7         0
    ## 5       34       34    IND  BWI      515      3      10         0
    ## 6       11       25    IND  JAX      688      4      10         0
    ##   CancellationCode Diverted CarrierDelay WeatherDelay NASDelay
    ## 1                         0           NA           NA       NA
    ## 2                         0           NA           NA       NA
    ## 3                         0           NA           NA       NA
    ## 4                         0           NA           NA       NA
    ## 5                         0            2            0        0
    ## 6                         0           NA           NA       NA
    ##   SecurityDelay LateAircraftDelay
    ## 1            NA                NA
    ## 2            NA                NA
    ## 3            NA                NA
    ## 4            NA                NA
    ## 5             0                32
    ## 6            NA                NA

``` r
tail(myDF)
```

    ##         Year Month DayofMonth DayOfWeek DepTime CRSDepTime ArrTime
    ## 7009723 2008    12         13         6     749        750     901
    ## 7009724 2008    12         13         6    1002        959    1204
    ## 7009725 2008    12         13         6     834        835    1021
    ## 7009726 2008    12         13         6     655        700     856
    ## 7009727 2008    12         13         6    1251       1240    1446
    ## 7009728 2008    12         13         6    1110       1103    1413
    ##         CRSArrTime UniqueCarrier FlightNum TailNum ActualElapsedTime
    ## 7009723        859            DL      1636  N646DL                72
    ## 7009724       1150            DL      1636  N646DL               122
    ## 7009725       1023            DL      1637  N908DL               167
    ## 7009726        856            DL      1638  N671DN               121
    ## 7009727       1437            DL      1639  N646DL               115
    ## 7009728       1418            DL      1641  N908DL               123
    ##         CRSElapsedTime AirTime ArrDelay DepDelay Origin Dest Distance
    ## 7009723             69      41        2       -1    SAV  ATL      215
    ## 7009724            111      71       14        3    ATL  IAD      533
    ## 7009725            168     139       -2       -1    ATL  SAT      874
    ## 7009726            116      85        0       -5    PBI  ATL      545
    ## 7009727            117      89        9       11    IAD  ATL      533
    ## 7009728            135     104       -5        7    SAT  ATL      874
    ##         TaxiIn TaxiOut Cancelled CancellationCode Diverted CarrierDelay
    ## 7009723     20      11         0                         0           NA
    ## 7009724      6      45         0                         0           NA
    ## 7009725      5      23         0                         0           NA
    ## 7009726     24      12         0                         0           NA
    ## 7009727     13      13         0                         0           NA
    ## 7009728      8      11         0                         0           NA
    ##         WeatherDelay NASDelay SecurityDelay LateAircraftDelay
    ## 7009723           NA       NA            NA                NA
    ## 7009724           NA       NA            NA                NA
    ## 7009725           NA       NA            NA                NA
    ## 7009726           NA       NA            NA                NA
    ## 7009727           NA       NA            NA                NA
    ## 7009728           NA       NA            NA                NA

## Step 1.13: Looking at only Indianapolis flights

First let’s look at the top of the ‘Origin’ column.

``` r
head(myDF$Origin)
```

    ## [1] IAD IAD IND IND IND IND
    ## 303 Levels: ABE ABI ABQ ABY ACK ACT ACV ACY ADK ADQ AEX AGS AKN ALB ... YUM

And the tail:

``` r
tail(myDF$Origin)
```

    ## [1] SAV ATL ATL PBI IAD SAT
    ## 303 Levels: ABE ABI ABQ ABY ACK ACT ACV ACY ADK ADQ AEX AGS AKN ALB ... YUM

Let’s also check the ‘dest’ column:

``` r
head(myDF$Dest)
```

    ## [1] TPA TPA BWI BWI BWI JAX
    ## 304 Levels: ABE ABI ABQ ABY ACK ACT ACV ACY ADK ADQ AEX AGS AKN ALB ... YUM

``` r
tail(myDF$Dest)
```

    ## [1] ATL IAD SAT ATL ATL ATL
    ## 304 Levels: ABE ABI ABQ ABY ACK ACT ACV ACY ADK ADQ AEX AGS AKN ALB ... YUM

## Step 1.15: Identifying Properties

Let’s slice by origin to identify flights that began in Indianapolis:

``` r
head(myDF$Origin == "IND")
```

    ## [1] FALSE FALSE  TRUE  TRUE  TRUE  TRUE

Okay, so that returned a series of Booleans. Let’s get the total number
by doing a ‘sum’:

``` r
sum(myDF$Origin == "IND")
```

    ## [1] 42750

Let’s count the flights that were destined to Indianapolis:

``` r
sum(myDF$Dest == "IND")
```

    ## [1] 42732

## Step 1.17: Extracting Flight Data with a Common City of Origin

Make a new DataFrame with the entries from the total data where the
origin airport was Indianapolis:

``` r
MyIndyOrigins <- subset(myDF, myDF$Origin == "IND")
head(MyIndyOrigins)
```

    ##   Year Month DayofMonth DayOfWeek DepTime CRSDepTime ArrTime CRSArrTime
    ## 3 2008     1          3         4     628        620     804        750
    ## 4 2008     1          3         4     926        930    1054       1100
    ## 5 2008     1          3         4    1829       1755    1959       1925
    ## 6 2008     1          3         4    1940       1915    2121       2110
    ## 7 2008     1          3         4    1937       1830    2037       1940
    ## 8 2008     1          3         4    1039       1040    1132       1150
    ##   UniqueCarrier FlightNum TailNum ActualElapsedTime CRSElapsedTime AirTime
    ## 3            WN       448  N428WN                96             90      76
    ## 4            WN      1746  N612SW                88             90      78
    ## 5            WN      3920  N464WN                90             90      77
    ## 6            WN       378  N726SW               101            115      87
    ## 7            WN       509  N763SW               240            250     230
    ## 8            WN       535  N428WN               233            250     219
    ##   ArrDelay DepDelay Origin Dest Distance TaxiIn TaxiOut Cancelled
    ## 3       14        8    IND  BWI      515      3      17         0
    ## 4       -6       -4    IND  BWI      515      3       7         0
    ## 5       34       34    IND  BWI      515      3      10         0
    ## 6       11       25    IND  JAX      688      4      10         0
    ## 7       57       67    IND  LAS     1591      3       7         0
    ## 8      -18       -1    IND  LAS     1591      7       7         0
    ##   CancellationCode Diverted CarrierDelay WeatherDelay NASDelay
    ## 3                         0           NA           NA       NA
    ## 4                         0           NA           NA       NA
    ## 5                         0            2            0        0
    ## 6                         0           NA           NA       NA
    ## 7                         0           10            0        0
    ## 8                         0           NA           NA       NA
    ##   SecurityDelay LateAircraftDelay
    ## 3            NA                NA
    ## 4            NA                NA
    ## 5             0                32
    ## 6            NA                NA
    ## 7             0                47
    ## 8            NA                NA

Let’s do the same for the flights that were destined for Indianapolis:

``` r
IndianapolisDestinations <- subset(myDF, myDF$Dest == "IND")
head(IndianapolisDestinations)
```

    ##     Year Month DayofMonth DayOfWeek DepTime CRSDepTime ArrTime CRSArrTime
    ## 72  2008     1          3         4     802        750    1001        955
    ## 136 2008     1          3         4    2255       1820     509         55
    ## 137 2008     1          3         4    1129       1050    1757       1725
    ## 501 2008     1          3         4    1038       1010    1259       1230
    ## 502 2008     1          3         4    1920       1850    2140       2110
    ## 605 2008     1          3         4    1139       1140    1401       1405
    ##     UniqueCarrier FlightNum TailNum ActualElapsedTime CRSElapsedTime
    ## 72             WN      2272  N263WN               119            125
    ## 136            WN      1924  N761RR               194            215
    ## 137            WN      3920  N464WN               208            215
    ## 501            WN         4  N674AA                81             80
    ## 502            WN       321  N742SW                80             80
    ## 605            WN       829  N476WN               142            145
    ##     AirTime ArrDelay DepDelay Origin Dest Distance TaxiIn TaxiOut
    ## 72      104        6       12    JAX  IND      688      7       8
    ## 136     176      254      275    LAS  IND     1591      9       9
    ## 137     179       32       39    LAS  IND     1591      8      21
    ## 501      63       29       28    MCI  IND      451      8      10
    ## 502      61       30       30    MCI  IND      451      9      10
    ## 605     123       -4       -1    MCO  IND      828      8      11
    ##     Cancelled CancellationCode Diverted CarrierDelay WeatherDelay NASDelay
    ## 72          0                         0           NA           NA       NA
    ## 136         0                         0            0            0        0
    ## 137         0                         0           32            0        0
    ## 501         0                         0            3            0        1
    ## 502         0                         0           30            0        0
    ## 605         0                         0           NA           NA       NA
    ##     SecurityDelay LateAircraftDelay
    ## 72             NA                NA
    ## 136             8               246
    ## 137             0                 0
    ## 501             0                25
    ## 502             0                 0
    ## 605            NA                NA

How would we determine which flights departed in a particular month?
We’ll try a table first.

``` r
table(MyIndyOrigins$Month)
```

    ## 
    ##    1    2    3    4    5    6    7    8    9   10   11   12 
    ## 3580 3414 3764 3644 3768 3852 3986 3700 3300 3418 3126 3198

And now a table:

``` r
plot(table(MyIndyOrigins$Month))
```

![](Intro_to_R_Week_1_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

Now the same for destinations:

``` r
plot(table(IndianapolisDestinations$Month))
```

![](Intro_to_R_Week_1_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

## Step 1.19: Analyzing the Departure Times of Flights

Let’s look at the flights with departure times before 6AM:

``` r
sum(MyIndyOrigins$DepTime < 600)
```

    ## [1] NA

This causes an issue because some value are NaNs. We’ll set the `na.rm`
parameter to drop these from the calculation:

``` r
sum(MyIndyOrigins$DepTime < 600, na.rm=TRUE)
```

    ## [1] 692

Let’s count the ‘NaN’ values in the `DepTime` column:

``` r
sum(is.na(MyIndyOrigins$DepTime))
```

    ## [1] 739

## Step 1.21 Annotating R Code with Comments

“Make a plot of departure times, grouped by hour, for the flights from
ATL to
LAX.”:

``` r
atllaxflights <- myDF[ which(myDF$Origin == "ATL" & myDF$Dest == "LAX"), ]
head(atllaxflights)
```

    ##        Year Month DayofMonth DayOfWeek DepTime CRSDepTime ArrTime
    ## 302878 2008     1         15         2    1337       1330    1523
    ## 302989 2008     1         15         2    2117       2120    2316
    ## 303102 2008     1         15         2     656        700     852
    ## 303478 2008     1         16         3      NA       1850      NA
    ## 303503 2008     1         16         3    1742       1735    2329
    ## 303521 2008     1         16         3      NA        835      NA
    ##        CRSArrTime UniqueCarrier FlightNum TailNum ActualElapsedTime
    ## 302878       1515            DL      1185  N129DL               286
    ## 302989       2325            DL      1423  N644DL               299
    ## 303102        851            DL      1556  N640DL               296
    ## 303478       2054            DL        41  N130DL                NA
    ## 303503       1932            DL        75   N6709               527
    ## 303521       1033            DL       110  N837MH                NA
    ##        CRSElapsedTime AirTime ArrDelay DepDelay Origin Dest Distance
    ## 302878            285     267        8        7    ATL  LAX     1946
    ## 302989            305     265       -9       -3    ATL  LAX     1946
    ## 303102            291     268        1       -4    ATL  LAX     1946
    ## 303478            304      NA       NA       NA    ATL  LAX     1946
    ## 303503            297     269      237        7    ATL  LAX     1946
    ## 303521            298      NA       NA       NA    ATL  LAX     1946
    ##        TaxiIn TaxiOut Cancelled CancellationCode Diverted CarrierDelay
    ## 302878      4      15         0                         0           NA
    ## 302989     14      20         0                         0           NA
    ## 303102      7      21         0                         0           NA
    ## 303478     NA      NA         1                A        0           NA
    ## 303503      7     251         0                         0            0
    ## 303521     NA      NA         1                B        0           NA
    ##        WeatherDelay NASDelay SecurityDelay LateAircraftDelay
    ## 302878           NA       NA            NA                NA
    ## 302989           NA       NA            NA                NA
    ## 303102           NA       NA            NA                NA
    ## 303478           NA       NA            NA                NA
    ## 303503            7      230             0                 0
    ## 303521           NA       NA            NA                NA

I noticed that there are several NA entries in the DepTime column for
this DataFrame. So let’s drop those, then group it by hour:

``` r
atllaxflights_clean <- na.omit(atllaxflights, cols="DepTime")
atllaxflights_clean$timestamp <- strptime(sprintf("%04d", atllaxflights_clean$DepTime), format="%H%M")
atllaxflights_clean$depHour <- as.numeric(format(atllaxflights_clean$timestamp, format="%H"))
head(atllaxflights_clean, 250)
```

    ##        Year Month DayofMonth DayOfWeek DepTime CRSDepTime ArrTime
    ## 303503 2008     1         16         3    1742       1735    2329
    ## 303863 2008     1         16         3    1505       1440    1705
    ## 304349 2008     1         16         3     712        700     907
    ## 304757 2008     1         17         4    1742       1735    1954
    ## 305126 2008     1         17         4    1533       1440    1725
    ## 305165 2008     1         17         4    1114       1100    1321
    ## 305385 2008     1         17         4    1356       1330    1547
    ## 305502 2008     1         17         4    2145       2120    2349
    ## 306087 2008     1         18         5    1658       1600    1850
    ## 307337 2008     1         19         6    2007       1850    2155
    ## 307356 2008     1         19         6    2148       1735     112
    ## 307665 2008     1         19         6    1557       1440    1914
    ## 307871 2008     1         19         6    1334       1330    1735
    ## 307961 2008     1         19         6    2319       2120     127
    ## 308409 2008     1         20         7    1621       1600    1814
    ## 309057 2008     1         20         7    2127       2120    2345
    ## 309502 2008     1         21         1    1853       1850    2116
    ## 309545 2008     1         21         1     834        835    1054
    ## 309551 2008     1         21         1    1607       1600    1811
    ## 309897 2008     1         21         1    1504       1440    1658
    ## 310262 2008     1         21         1    2136       2120       2
    ## 310776 2008     1         22         2    1733       1735    1956
    ## 310794 2008     1         22         2     835        835    1103
    ## 310800 2008     1         22         2    1559       1600    1812
    ## 311164 2008     1         22         2    1109       1100    1342
    ## 311371 2008     1         22         2    1338       1330    1600
    ## 311482 2008     1         22         2    2117       2120    2351
    ## 311596 2008     1         22         2     702        700     909
    ## 311973 2008     1         23         3    1850       1850    2127
    ## 311998 2008     1         23         3    1743       1735    2016
    ## 312016 2008     1         23         3     833        835    1111
    ## 312022 2008     1         23         3    1601       1600    1823
    ## 312144 2008     1         23         3    2117       2120    2348
    ## 312320 2008     1         23         3     958        950    1238
    ## 312358 2008     1         23         3    1501       1440    1742
    ## 312395 2008     1         23         3    1058       1100    1326
    ## 312612 2008     1         23         3    1330       1330    1557
    ## 312843 2008     1         23         3     658        700     922
    ## 313228 2008     1         24         4    1847       1850    2148
    ## 313253 2008     1         24         4    1740       1735    2023
    ## 313271 2008     1         24         4     834        835    1112
    ## 313277 2008     1         24         4    1603       1600    1836
    ## 313296 2008     1         24         4     950        950    1213
    ## 313400 2008     1         24         4    2001       2000    2258
    ## 313621 2008     1         24         4    1444       1440    1712
    ## 313660 2008     1         24         4    1055       1100    1313
    ## 313880 2008     1         24         4    1346       1330    1610
    ## 313998 2008     1         24         4    2115       2120    2351
    ## 314526 2008     1         25         5    1922       1850    2149
    ## 314551 2008     1         25         5    1734       1735    1952
    ## 314575 2008     1         25         5    1610       1600    1843
    ## 314594 2008     1         25         5     950        950    1225
    ## 314697 2008     1         25         5    2001       2000    2248
    ## 314917 2008     1         25         5    1552       1440    1806
    ## 314956 2008     1         25         5    1059       1100    1333
    ## 315173 2008     1         25         5    1337       1330    1600
    ## 315293 2008     1         25         5    2127       2120       7
    ## 315414 2008     1         25         5     656        700     920
    ## 315817 2008     1         26         6    1845       1850    2136
    ## 315836 2008     1         26         6    1735       1735    2013
    ## 315851 2008     1         26         6     846        835    1050
    ## 315856 2008     1         26         6    1559       1600    1844
    ## 316175 2008     1         26         6    1233       1100    1515
    ## 316353 2008     1         26         6    1330       1330    1608
    ## 316446 2008     1         26         6    2121       2120      22
    ## 316865 2008     1         27         7    1934       1850    2139
    ## 316908 2008     1         27         7     835        835    1050
    ## 316914 2008     1         27         7    1613       1600    1824
    ## 316932 2008     1         27         7     950        950    1209
    ## 317292 2008     1         27         7    1056       1100    1341
    ## 317502 2008     1         27         7    1325       1330    1540
    ## 317736 2008     1         27         7     657        700     921
    ## 318137 2008     1         28         1    1754       1735    2004
    ## 318155 2008     1         28         1     840        835    1054
    ## 318161 2008     1         28         1    1559       1600    1826
    ## 318283 2008     1         28         1    1958       2000    2253
    ## 318546 2008     1         28         1    1230       1100    1440
    ## 318764 2008     1         28         1    1328       1330    1532
    ## 318882 2008     1         28         1    2116       2120    2342
    ## 319008 2008     1         28         1     702        700     919
    ## 319751 2008     1         29         2     952        950    1216
    ## 320032 2008     1         29         2    1328       1330    1536
    ## 320257 2008     1         29         2     657        700     908
    ## 321057 2008     1         30         3    1127       1100    1328
    ## 322658 2008     1         31         4    2202       2120      13
    ## 322786 2008     1         31         4     713        700     921
    ## 354084 2008     1          1         2    1055       1047    1305
    ## 354086 2008     1          1         2    2155       2125    2358
    ## 354829 2008     1          2         3    1154       1047    1347
    ## 354831 2008     1          2         3    2204       2125    2400
    ## 355570 2008     1          3         4     957        930    1154
    ## 355571 2008     1          3         4    1108       1047    1308
    ## 355572 2008     1          3         4    1818       1759    2024
    ## 355573 2008     1          3         4    2146       2125    2351
    ## 356319 2008     1          4         5    1043       1047    1305
    ## 356320 2008     1          4         5    1807       1759    2030
    ## 356321 2008     1          4         5    2137       2125    2356
    ## 357053 2008     1          5         6    1112       1047    1327
    ## 357781 2008     1          6         7    2139       2125       3
    ## 358524 2008     1          7         1     938        930    1152
    ## 359256 2008     1          8         2     941        930    1158
    ## 359258 2008     1          8         2    1842       1759    2107
    ## 362419 2008     1         13         7    1853       1759    2037
    ## 363078 2008     1         14         1    2230       2125      11
    ## 364325 2008     1         16         3    1758       1759    2222
    ## 364326 2008     1         16         3    2346       2125     129
    ## 364928 2008     1         17         4    1840       1759    2035
    ## 364929 2008     1         17         4    2156       2125    2355
    ## 366255 2008     1         19         6    1047       1037    1309
    ## 366256 2008     1         19         6    2053       1759    2238
    ## 368224 2008     1         22         2     938        930    1150
    ## 368226 2008     1         22         2    1757       1759    2016
    ## 368820 2008     1         23         3     942        930    1200
    ## 368822 2008     1         23         3    1757       1759    2033
    ## 369424 2008     1         24         4     937        930    1156
    ## 369425 2008     1         24         4    1029       1037    1313
    ## 369426 2008     1         24         4    1756       1759    2047
    ## 369427 2008     1         24         4    2128       2125    2352
    ## 370088 2008     1         25         5     930        930    1153
    ## 370089 2008     1         25         5    1033       1037    1310
    ## 370090 2008     1         25         5    1757       1759    2031
    ## 370091 2008     1         25         5    2202       2125      42
    ## 370752 2008     1         26         6     930        930    1204
    ## 370753 2008     1         26         6    1034       1037    1321
    ## 370754 2008     1         26         6    1758       1759    2032
    ## 370755 2008     1         26         6    2151       2125      43
    ## 371405 2008     1         27         7     936        930    1207
    ## 371406 2008     1         27         7    1036       1037    1341
    ## 371407 2008     1         27         7    1759       1759    2034
    ## 371408 2008     1         27         7    2133       2125    2355
    ## 372070 2008     1         28         1     934        930    1152
    ## 372072 2008     1         28         1    1754       1759    2017
    ## 372073 2008     1         28         1    2119       2125    2345
    ## 372732 2008     1         29         2    1035       1037    1254
    ## 373330 2008     1         30         3    1838       1759    2037
    ## 373331 2008     1         30         3    2122       2125    2340
    ## 373933 2008     1         31         4    2202       2125       2
    ## 587929 2008     1          1         2    2113       1850    2340
    ## 587971 2008     1          1         2     837        838    1126
    ## 587977 2008     1          1         2    1601       1600    1818
    ## 588097 2008     1          1         2    2007       2000    2257
    ## 588307 2008     1          1         2    1446       1440    1647
    ## 588658 2008     1          1         2    2129       2135       2
    ## 588758 2008     1          1         2     659        700     915
    ## 589138 2008     1          2         3     853        835    1056
    ## 589508 2008     1          2         3    1532       1440    1720
    ## 589579 2008     1          2         3    1218       1202    1410
    ## 590026 2008     1          2         3     713        700     911
    ## 590389 2008     1          3         4    1907       1850    2131
    ## 590413 2008     1          3         4    1735       1735    1955
    ## 590430 2008     1          3         4     841        835    1110
    ## 590436 2008     1          3         4    1620       1600    1812
    ## 590455 2008     1          3         4    1010        950    1206
    ## 590565 2008     1          3         4    2034       2000    2306
    ## 591158 2008     1          3         4    2157       2120      32
    ## 591284 2008     1          3         4     658        700     910
    ## 591686 2008     1          4         5    1914       1850    2153
    ## 591711 2008     1          4         5    1734       1735    1959
    ## 591735 2008     1          4         5    1611       1600    1849
    ## 591754 2008     1          4         5    1016        950    1215
    ## 591864 2008     1          4         5    2002       2000    2340
    ## 592088 2008     1          4         5    1456       1440    1707
    ## 592132 2008     1          4         5    1142       1100    1353
    ## 592347 2008     1          4         5    1332       1330    1537
    ## 592469 2008     1          4         5    2134       2120     126
    ## 592594 2008     1          4         5     705        700     907
    ## 592996 2008     1          5         6    1941       1850    2145
    ## 593015 2008     1          5         6    1739       1735    2010
    ## 593035 2008     1          5         6    1559       1600    1814
    ## 593330 2008     1          5         6    1455       1440    1649
    ## 593632 2008     1          5         6    2211       2120      11
    ## 594071 2008     1          6         7    1743       1735    2022
    ## 594089 2008     1          6         7     942        835    1144
    ## 594095 2008     1          6         7    1601       1600    1813
    ## 594113 2008     1          6         7    1121        950    1317
    ## 594219 2008     1          6         7    2002       2000    2251
    ## 594681 2008     1          6         7    1331       1330    1531
    ## 594796 2008     1          6         7    2100       2100    2344
    ## 595328 2008     1          7         1     842        835    1048
    ## 595353 2008     1          7         1    1001        950    1206
    ## 595461 2008     1          7         1    1958       2000    2237
    ## 595726 2008     1          7         1    1104       1100    1324
    ## 596062 2008     1          7         1    2123       2120    2347
    ## 596189 2008     1          7         1     711        700     906
    ## 596620 2008     1          8         2    1737       1735    1948
    ## 596644 2008     1          8         2    1603       1600    1818
    ## 596974 2008     1          8         2    1511       1440    1702
    ## 597012 2008     1          8         2    1104       1100    1313
    ## 597329 2008     1          8         2    2120       2120    2345
    ## 597821 2008     1          9         3    1930       1850    2113
    ## 598211 2008     1          9         3    1539       1440    1723
    ## 599475 2008     1         10         4    1440       1440    1647
    ## 599512 2008     1         10         4    1112       1100    1316
    ## 600443 2008     1         11         5    1016        950    1216
    ## 601145 2008     1         11         5    2118       2120    2354
    ## 601671 2008     1         12         6    2015       1850    2200
    ## 602034 2008     1         12         6    1122       1100    1334
    ## 603104 2008     1         13         7    1509       1440    1652
    ## 603350 2008     1         13         7    1339       1330    1530
    ## 604003 2008     1         14         1     849        835    1058
    ## 604724 2008     1         14         1    2143       2120    2347
    ## 605591 2008     1         15         2     956        950    1208
    ## 605628 2008     1         15         2    1510       1440    1705
    ## 890284 2008     2         14         4     708        700     919
    ## 890686 2008     2         15         5    2036       1915    2226
    ## 890878 2008     2         15         5    2110       2020    2303
    ## 893158 2008     2         17         7    1558       1600    1812
    ## 893274 2008     2         17         7      25       2020     234
    ## 893784 2008     2         17         7      48       2140     251
    ## 894226 2008     2         18         1    1927       1915    2148
    ## 894251 2008     2         18         1    1724       1705    1933
    ## 894411 2008     2         18         1    2029       2020    2247
    ## 894630 2008     2         18         1    1445       1440    1658
    ## 894668 2008     2         18         1    1206       1110    1408
    ## 894871 2008     2         18         1    1355       1330    1557
    ## 894996 2008     2         18         1    2139       2140      11
    ## 895491 2008     2         19         2    1932       1915    2134
    ## 895858 2008     2         19         2    1012        950    1219
    ## 895891 2008     2         19         2    1453       1440    1701
    ## 896365 2008     2         19         2     701        700     916
    ## 896759 2008     2         20         3    1909       1915    2137
    ## 897170 2008     2         20         3    1526       1440    1731
    ## 897208 2008     2         20         3    1118       1110    1322
    ## 897535 2008     2         20         3    2145       2140       4
    ## 898058 2008     2         21         4    2004       1915    2231
    ## 898083 2008     2         21         4    1714       1705    1935
    ## 898108 2008     2         21         4    1624       1600    1900
    ## 898248 2008     2         21         4    2056       2020    2320
    ## 898472 2008     2         21         4    1447       1440    1654
    ## 898511 2008     2         21         4    1113       1110    1331
    ## 898840 2008     2         21         4    2203       2140      16
    ## 898969 2008     2         21         4     700        700     906
    ## 899374 2008     2         22         5    1915       1915    2140
    ## 899399 2008     2         22         5    1806       1705    2024
    ## 899424 2008     2         22         5    1703       1600    1920
    ## 899443 2008     2         22         5    1001        950    1216
    ## 899566 2008     2         22         5    2201       2020      14
    ## 899787 2008     2         22         5    1446       1440    1705
    ## 899827 2008     2         22         5    1156       1110    1410
    ## 900035 2008     2         22         5    1341       1330    1602
    ## 900163 2008     2         22         5    2327       2140     122
    ## 900289 2008     2         22         5     700        700     908
    ## 900682 2008     2         23         6    1927       1915    2152
    ## 900722 2008     2         23         6     835        835    1054
    ## 900831 2008     2         23         6    2020       2020    2249
    ## 901000 2008     2         23         6    1024        950    1241
    ## 901030 2008     2         23         6    1533       1440    1740
    ## 901064 2008     2         23         6    1121       1110    1338
    ## 901243 2008     2         23         6    1330       1330    1548
    ## 901355 2008     2         23         6    2230       2140      51
    ##        CRSArrTime UniqueCarrier FlightNum TailNum ActualElapsedTime
    ## 303503       1932            DL        75   N6709               527
    ## 303863       1631            DL       885  N831MH               300
    ## 304349        851            DL      1556  N702TW               295
    ## 304757       1932            DL        75   N6701               312
    ## 305126       1631            DL       885  N830MH               292
    ## 305165       1255            DL       937  N139DL               307
    ## 305385       1515            DL      1185  N144DA               291
    ## 305502       2325            DL      1423  N6704Z               304
    ## 306087       1756            DL       125  N6712B               292
    ## 307337       2054            DL        41  N124DE               288
    ## 307356       1932            DL        75  N6707A               384
    ## 307665       1631            DL       885  N828MH               377
    ## 307871       1515            DL      1185  N140LL               421
    ## 307961       2325            DL      1423  N649DL               308
    ## 308409       1756            DL       125  N721TW               293
    ## 309057       2325            DL      1423  N697DL               318
    ## 309502       2054            DL        41  N136DL               323
    ## 309545       1033            DL       110  N131DN               320
    ## 309551       1756            DL       125  N697DL               304
    ## 309897       1631            DL       885  N829MH               294
    ## 310262       2325            DL      1423  N695DA               326
    ## 310776       1932            DL        75  N6710E               323
    ## 310794       1033            DL       110  N617DL               328
    ## 310800       1756            DL       125  N640DL               313
    ## 311164       1255            DL       937  N137DL               333
    ## 311371       1515            DL      1185  N1402A               322
    ## 311482       2325            DL      1423  N710TW               334
    ## 311596        851            DL      1556  N641DL               307
    ## 311973       2054            DL        41  N136DL               337
    ## 311998       1932            DL        75  N654DL               333
    ## 312016       1033            DL       110  N699DL               338
    ## 312022       1756            DL       125  N143DA               322
    ## 312144       2325            DL       535  N639DL               331
    ## 312320       1153            DL       823  N675DL               340
    ## 312358       1631            DL       885  N832MH               341
    ## 312395       1255            DL       937  N131DN               328
    ## 312612       1515            DL      1185  N140LL               327
    ## 312843        851            DL      1556  N652DL               324
    ## 313228       2054            DL        41  N125DL               361
    ## 313253       1932            DL        75  N652DL               343
    ## 313271       1033            DL       110  N138DL               338
    ## 313277       1756            DL       125  N1402A               333
    ## 313296       1150            DL       189  N843MH               323
    ## 313400       2215            DL       535  N699DL               357
    ## 313621       1631            DL       885  N835MH               328
    ## 313660       1255            DL       937  N121DE               318
    ## 313880       1515            DL      1185  N143DA               324
    ## 313998       2325            DL      1423  N6716C               336
    ## 314526       2054            DL        41  N130DL               327
    ## 314551       1932            DL        75  N6703D               318
    ## 314575       1756            DL       125  N699DL               333
    ## 314594       1150            DL       189  N825MH               335
    ## 314697       2215            DL       535  N124DE               347
    ## 314917       1631            DL       885  N829MH               314
    ## 314956       1255            DL       937  N139DL               334
    ## 315173       1515            DL      1185  N144DA               323
    ## 315293       2325            DL      1423  N6706Q               340
    ## 315414        851            DL      1556  N645DL               324
    ## 315817       2054            DL        41  N130DL               351
    ## 315836       1932            DL        75  N6710E               338
    ## 315851       1033            DL       110  N125DL               304
    ## 315856       1756            DL       125  N710TW               345
    ## 316175       1255            DL       937  N136DL               342
    ## 316353       1515            DL      1185  N1402A               338
    ## 316446       2325            DL      1423  N637DL               361
    ## 316865       2054            DL        41  N143DA               305
    ## 316908       1033            DL       110  N138DL               315
    ## 316914       1756            DL       125  N710TW               311
    ## 316932       1150            DL       189  N861DA               319
    ## 317292       1255            DL       937  N131DN               345
    ## 317502       1515            DL      1185  N140LL               315
    ## 317736        851            DL      1556  N655DL               324
    ## 318137       1932            DL        75  N699DL               310
    ## 318155       1033            DL       110  N139DL               314
    ## 318161       1756            DL       125  N712TW               327
    ## 318283       2215            DL       535  N138DL               355
    ## 318546       1255            DL       937  N135DL               310
    ## 318764       1515            DL      1185  N144DA               304
    ## 318882       2325            DL      1423  N6703D               326
    ## 319008        851            DL      1556  N638DL               317
    ## 319751       1153            DL       823  N683DA               324
    ## 320032       1515            DL      1185  N143DA               308
    ## 320257        851            DL      1556  N696DA               311
    ## 321057       1255            DL       937  N139DL               301
    ## 322658       2325            DL      1423  N67171               311
    ## 322786        851            DL      1556  N641DL               308
    ## 354084       1250            FL        54  N173AT               310
    ## 354086       2328            FL        41  N317AT               303
    ## 354829       1250            FL        54  N166AT               293
    ## 354831       2328            FL        41  N278AT               296
    ## 355570       1133            FL        55  N288AT               297
    ## 355571       1250            FL        54  N311AT               300
    ## 355572       2002            FL        40  N240AT               306
    ## 355573       2328            FL        41  N330AT               305
    ## 356319       1250            FL        54  N329AT               322
    ## 356320       2002            FL        40  N276AT               323
    ## 356321       2328            FL        41  N284AT               319
    ## 357053       1250            FL        54  N299AT               315
    ## 357781       2328            FL        41  N326AT               324
    ## 358524       1133            FL        55  N318AT               314
    ## 359256       1130            FL        55  N307AT               317
    ## 359258       1959            FL        40  N173AT               325
    ## 362419       1959            FL        40  N174AT               284
    ## 363078       2325            FL        41  N309AT               281
    ## 364325       1959            FL        40  N174AT               444
    ## 364326       2325            FL        41  N149AT               283
    ## 364928       1959            FL        40  N317AT               295
    ## 364929       2325            FL        41  N296AT               299
    ## 366255       1237            FL        54  N308AT               322
    ## 366256       1959            FL        40  N283AT               285
    ## 368224       1130            FL        55  N289AT               312
    ## 368226       1959            FL        40  N287AT               319
    ## 368820       1130            FL        55  N292AT               318
    ## 368822       1959            FL        40  N283AT               336
    ## 369424       1130            FL        55  N329AT               319
    ## 369425       1237            FL        54  N317AT               344
    ## 369426       1959            FL        40  N281AT               351
    ## 369427       2325            FL        41  N276AT               324
    ## 370088       1130            FL        55  N300AT               323
    ## 370089       1237            FL        54  N267AT               337
    ## 370090       1959            FL        40  N284AT               334
    ## 370091       2325            FL        41  N268AT               340
    ## 370752       1130            FL        55  N167AT               334
    ## 370753       1237            FL        54  N286AT               347
    ## 370754       1959            FL        40  N149AT               334
    ## 370755       2325            FL        41  N286AT               352
    ## 371405       1130            FL        55  N174AT               331
    ## 371406       1237            FL        54  N328AT               365
    ## 371407       1959            FL        40  N167AT               335
    ## 371408       2325            FL        41  N279AT               322
    ## 372070       1130            FL        55  N168AT               318
    ## 372072       1959            FL        40  N299AT               323
    ## 372073       2325            FL        41  N169AT               326
    ## 372732       1237            FL        54  N149AT               319
    ## 373330       1959            FL        40  N283AT               299
    ## 373331       2325            FL        41  N289AT               318
    ## 373933       2325            FL        41  N295AT               300
    ## 587929       2054            DL        41  N134DL               327
    ## 587971       1036            DL       110  N128DL               349
    ## 587977       1756            DL       125  N829MH               317
    ## 588097       2215            DL       535  N127DL               350
    ## 588307       1631            DL       885  N827MH               301
    ## 588658       2342            DL      1423  N379DA               333
    ## 588758        851            DL      1556  N655DL               316
    ## 589138       1033            DL       110  N127DL               303
    ## 589508       1631            DL       885  N829MH               288
    ## 589579       1353            DL       963  N129DL               292
    ## 590026        851            DL      1556  N608DA               298
    ## 590389       2054            DL        41  N834MH               324
    ## 590413       1932            DL        75  N613DL               320
    ## 590430       1033            DL       110  N139DL               329
    ## 590436       1756            DL       125  N140LL               292
    ## 590455       1150            DL       189  N861DA               296
    ## 590565       2215            DL       535  N609DL               332
    ## 591158       2325            DL      1423  N615DL               335
    ## 591284        851            DL      1556  N703TW               312
    ## 591686       2054            DL        41  N835MH               339
    ## 591711       1932            DL        75  N657DL               325
    ## 591735       1756            DL       125  N703TW               338
    ## 591754       1150            DL       189  N841MH               299
    ## 591864       2215            DL       535  N139DL               398
    ## 592088       1631            DL       885  N832MH               311
    ## 592132       1255            DL       937  N138DL               311
    ## 592347       1515            DL      1185  N140LL               305
    ## 592469       2327            DL      1423  N381DA               412
    ## 592594        851            DL      1556  N6716C               302
    ## 592996       2054            DL        41  N835MH               304
    ## 593015       1932            DL        75  N67171               331
    ## 593035       1758            DL       125  N3731T               315
    ## 593330       1631            DL       885  N834MH               294
    ## 593632       2325            DL      1423  N831MH               300
    ## 594071       1932            DL        75  N702TW               339
    ## 594089       1033            DL       110  N131DN               302
    ## 594095       1756            DL       125  N721TW               312
    ## 594113       1150            DL       189  N837MH               296
    ## 594219       2215            DL       535  N131DN               349
    ## 594681       1515            DL      1185  N143DA               300
    ## 594796       2307            DL      1423  N650DL               344
    ## 595328       1033            DL       110  N131DN               306
    ## 595353       1150            DL       189  N867DA               305
    ## 595461       2215            DL       535  N136DL               339
    ## 595726       1255            DL       937  N129DL               320
    ## 596062       2325            DL      1423  N900PC               324
    ## 596189        851            DL      1556  N654DL               295
    ## 596620       1932            DL        75  N6705Y               311
    ## 596644       1756            DL       125  N652DL               315
    ## 596974       1631            DL       885  N833MH               291
    ## 597012       1255            DL       937  N132DN               309
    ## 597329       2325            DL      1423  N721TW               325
    ## 597821       2054            DL        41  N834MH               283
    ## 598211       1631            DL       885  N829MH               284
    ## 599475       1631            DL       885  N832MH               307
    ## 599512       1255            DL       937  N131DN               304
    ## 600443       1150            DL       189  N181DN               300
    ## 601145       2327            DL      1423  N399DA               336
    ## 601671       2054            DL        41  N832MH               285
    ## 602034       1255            DL       937  N132DN               312
    ## 603104       1631            DL       885  N832MH               283
    ## 603350       1515            DL      1185  N140LL               291
    ## 604003       1033            DL       110  N613DL               309
    ## 604724       2325            DL      1423  N654DL               304
    ## 605591       1153            DL       823  N617DL               312
    ## 605628       1631            DL       885  N828MH               295
    ## 890284        851            DL      1556  N609DL               311
    ## 890686       2115            DL        41  N131DN               290
    ## 890878       2226            DL       535  N689DL               293
    ## 893158       1756            DL       125  N614DL               314
    ## 893274       2226            DL       535  N6714Q               309
    ## 893784       2345            DL      1423  N709TW               303
    ## 894226       2115            DL        41  N121DE               321
    ## 894251       1905            DL        75  N6716C               309
    ## 894411       2226            DL       535  N612DL               318
    ## 894630       1631            DL       885  N830MH               313
    ## 894668       1307            DL       937  N702TW               302
    ## 894871       1517            DL      1185  N143DA               302
    ## 894996       2345            DL      1423  N695DA               332
    ## 895491       2115            DL        41  N138DL               302
    ## 895858       1153            DL       823  N617DL               307
    ## 895891       1631            DL       885  N828MH               308
    ## 896365        851            DL      1556  N6705Y               315
    ## 896759       2115            DL        41  N136DL               328
    ## 897170       1631            DL       885  N831MH               305
    ## 897208       1307            DL       937   N704X               304
    ## 897535       2345            DL      1423   N6702               319
    ## 898058       2115            DL        41  N135DL               327
    ## 898083       1907            DL        75  N3754A               321
    ## 898108       1756            DL       125  N6703D               336
    ## 898248       2226            DL       535  N690DL               324
    ## 898472       1631            DL       885  N832MH               307
    ## 898511       1307            DL       937  N703TW               318
    ## 898840       2345            DL      1423   N6709               313
    ## 898969        851            DL      1556  N614DL               306
    ## 899374       2115            DL        41  N132DN               325
    ## 899399       1905            DL        75  N610DL               318
    ## 899424       1756            DL       125  N640DL               317
    ## 899443       1150            DL       189  N839MH               315
    ## 899566       2226            DL       535  N682DA               313
    ## 899787       1631            DL       885  N830MH               319
    ## 899827       1307            DL       937  N710TW               314
    ## 900035       1517            DL      1185  N143DA               321
    ## 900163       2345            DL      1423  N697DL               295
    ## 900289        851            DL      1556  N609DL               308
    ## 900682       2115            DL        41  N126DL               325
    ## 900722       1033            DL       110  N138DL               319
    ## 900831       2226            DL       535  N623DL               329
    ## 901000       1153            DL       823   N6700               317
    ## 901030       1631            DL       885  N832MH               307
    ## 901064       1307            DL       937  N706TW               317
    ## 901243       1517            DL      1185  N140LL               318
    ## 901355       2345            DL      1423  N702TW               321
    ##        CRSElapsedTime AirTime ArrDelay DepDelay Origin Dest Distance
    ## 303503            297     269      237        7    ATL  LAX     1946
    ## 303863            291     261       34       25    ATL  LAX     1946
    ## 304349            291     271       16       12    ATL  LAX     1946
    ## 304757            297     266       22        7    ATL  LAX     1946
    ## 305126            291     263       54       53    ATL  LAX     1946
    ## 305165            295     264       26       14    ATL  LAX     1946
    ## 305385            285     268       32       26    ATL  LAX     1946
    ## 305502            305     264       24       25    ATL  LAX     1946
    ## 306087            296     265       54       58    ATL  LAX     1946
    ## 307337            304     255       61       77    ATL  LAX     1946
    ## 307356            297     263      340      253    ATL  LAX     1946
    ## 307665            291     259      163       77    ATL  LAX     1946
    ## 307871            285     256      140        4    ATL  LAX     1946
    ## 307961            305     266      122      119    ATL  LAX     1946
    ## 308409            296     266       18       21    ATL  LAX     1946
    ## 309057            305     271       20        7    ATL  LAX     1946
    ## 309502            304     286       22        3    ATL  LAX     1946
    ## 309545            298     297       21       -1    ATL  LAX     1946
    ## 309551            296     279       15        7    ATL  LAX     1946
    ## 309897            291     271       27       24    ATL  LAX     1946
    ## 310262            305     285       37       16    ATL  LAX     1946
    ## 310776            297     303       24       -2    ATL  LAX     1946
    ## 310794            298     301       30        0    ATL  LAX     1946
    ## 310800            296     292       16       -1    ATL  LAX     1946
    ## 311164            295     302       47        9    ATL  LAX     1946
    ## 311371            285     296       45        8    ATL  LAX     1946
    ## 311482            305     293       26       -3    ATL  LAX     1946
    ## 311596            291     287       18        2    ATL  LAX     1946
    ## 311973            304     296       33        0    ATL  LAX     1946
    ## 311998            297     299       44        8    ATL  LAX     1946
    ## 312016            298     308       38       -2    ATL  LAX     1946
    ## 312022            296     297       27        1    ATL  LAX     1946
    ## 312144            305     297       23       -3    ATL  LAX     1946
    ## 312320            303     308       45        8    ATL  LAX     1946
    ## 312358            291     314       71       21    ATL  LAX     1946
    ## 312395            295     297       31       -2    ATL  LAX     1946
    ## 312612            285     300       42        0    ATL  LAX     1946
    ## 312843            291     294       31       -2    ATL  LAX     1946
    ## 313228            304     314       54       -3    ATL  LAX     1946
    ## 313253            297     312       51        5    ATL  LAX     1946
    ## 313271            298     309       39       -1    ATL  LAX     1946
    ## 313277            296     300       40        3    ATL  LAX     1946
    ## 313296            300     300       23        0    ATL  LAX     1946
    ## 313400            315     321       43        1    ATL  LAX     1946
    ## 313621            291     305       41        4    ATL  LAX     1946
    ## 313660            295     291       18       -5    ATL  LAX     1946
    ## 313880            285     303       55       16    ATL  LAX     1946
    ## 313998            305     296       26       -5    ATL  LAX     1946
    ## 314526            304     283       55       32    ATL  LAX     1946
    ## 314551            297     292       20       -1    ATL  LAX     1946
    ## 314575            296     297       47       10    ATL  LAX     1946
    ## 314594            300     303       35        0    ATL  LAX     1946
    ## 314697            315     317       33        1    ATL  LAX     1946
    ## 314917            291     290       95       72    ATL  LAX     1946
    ## 314956            295     302       38       -1    ATL  LAX     1946
    ## 315173            285     308       45        7    ATL  LAX     1946
    ## 315293            305     301       42        7    ATL  LAX     1946
    ## 315414            291     291       29       -4    ATL  LAX     1946
    ## 315817            304     307       42       -5    ATL  LAX     1946
    ## 315836            297     312       41        0    ATL  LAX     1946
    ## 315851            298     275       17       11    ATL  LAX     1946
    ## 315856            296     318       48       -1    ATL  LAX     1946
    ## 316175            295     316      140       93    ATL  LAX     1946
    ## 316353            285     309       53        0    ATL  LAX     1946
    ## 316446            305     317       57        1    ATL  LAX     1946
    ## 316865            304     268       45       44    ATL  LAX     1946
    ## 316908            298     285       17        0    ATL  LAX     1946
    ## 316914            296     277       28       13    ATL  LAX     1946
    ## 316932            300     282       19        0    ATL  LAX     1946
    ## 317292            295     295       46       -4    ATL  LAX     1946
    ## 317502            285     285       25       -5    ATL  LAX     1946
    ## 317736            291     289       30       -3    ATL  LAX     1946
    ## 318137            297     285       32       19    ATL  LAX     1946
    ## 318155            298     282       21        5    ATL  LAX     1946
    ## 318161            296     298       30       -1    ATL  LAX     1946
    ## 318283            315     288       38       -2    ATL  LAX     1946
    ## 318546            295     288      105       90    ATL  LAX     1946
    ## 318764            285     287       17       -2    ATL  LAX     1946
    ## 318882            305     298       17       -4    ATL  LAX     1946
    ## 319008            291     285       28        2    ATL  LAX     1946
    ## 319751            303     285       23        2    ATL  LAX     1946
    ## 320032            285     284       21       -2    ATL  LAX     1946
    ## 320257            291     284       17       -3    ATL  LAX     1946
    ## 321057            295     273       33       27    ATL  LAX     1946
    ## 322658            305     273       48       42    ATL  LAX     1946
    ## 322786            291     283       30       13    ATL  LAX     1946
    ## 354084            303     287       15        8    ATL  LAX     1946
    ## 354086            303     281       30       30    ATL  LAX     1946
    ## 354829            303     272       57       67    ATL  LAX     1946
    ## 354831            303     272       32       39    ATL  LAX     1946
    ## 355570            303     269       21       27    ATL  LAX     1946
    ## 355571            303     273       18       21    ATL  LAX     1946
    ## 355572            303     280       22       19    ATL  LAX     1946
    ## 355573            303     282       23       21    ATL  LAX     1946
    ## 356319            303     287       15       -4    ATL  LAX     1946
    ## 356320            303     290       28        8    ATL  LAX     1946
    ## 356321            303     295       28       12    ATL  LAX     1946
    ## 357053            303     291       37       25    ATL  LAX     1946
    ## 357781            303     294       35       14    ATL  LAX     1946
    ## 358524            303     284       19        8    ATL  LAX     1946
    ## 359256            300     276       28       11    ATL  LAX     1946
    ## 359258            300     296       68       43    ATL  LAX     1946
    ## 362419            300     255       38       54    ATL  LAX     1946
    ## 363078            300     262       46       65    ATL  LAX     1946
    ## 364325            300     269      143       -1    ATL  LAX     1946
    ## 364326            300     268      124      141    ATL  LAX     1946
    ## 364928            300     270       36       41    ATL  LAX     1946
    ## 364929            300     269       30       31    ATL  LAX     1946
    ## 366255            300     265       32       10    ATL  LAX     1946
    ## 366256            300     266      159      174    ATL  LAX     1946
    ## 368224            300     295       20        8    ATL  LAX     1946
    ## 368226            300     301       17       -2    ATL  LAX     1946
    ## 368820            300     294       30       12    ATL  LAX     1946
    ## 368822            300     308       34       -2    ATL  LAX     1946
    ## 369424            300     302       26        7    ATL  LAX     1946
    ## 369425            300     295       36       -8    ATL  LAX     1946
    ## 369426            300     323       48       -3    ATL  LAX     1946
    ## 369427            300     299       27        3    ATL  LAX     1946
    ## 370088            300     300       23        0    ATL  LAX     1946
    ## 370089            300     311       33       -4    ATL  LAX     1946
    ## 370090            300     306       32       -2    ATL  LAX     1946
    ## 370091            300     319       77       37    ATL  LAX     1946
    ## 370752            300     315       34        0    ATL  LAX     1946
    ## 370753            300     327       44       -3    ATL  LAX     1946
    ## 370754            300     311       33       -1    ATL  LAX     1946
    ## 370755            300     330       78       26    ATL  LAX     1946
    ## 371405            300     304       37        6    ATL  LAX     1946
    ## 371406            300     315       64       -1    ATL  LAX     1946
    ## 371407            300     311       35        0    ATL  LAX     1946
    ## 371408            300     298       30        8    ATL  LAX     1946
    ## 372070            300     291       22        4    ATL  LAX     1946
    ## 372072            300     300       18       -5    ATL  LAX     1946
    ## 372073            300     299       20       -6    ATL  LAX     1946
    ## 372732            300     286       17       -2    ATL  LAX     1946
    ## 373330            300     278       38       39    ATL  LAX     1946
    ## 373331            300     278       15       -3    ATL  LAX     1946
    ## 373933            300     273       37       37    ATL  LAX     1946
    ## 587929            304     275      166      143    ATL  LAX     1946
    ## 587971            298     269       50       -1    ATL  LAX     1946
    ## 587977            296     276       22        1    ATL  LAX     1946
    ## 588097            315     276       42        7    ATL  LAX     1946
    ## 588307            291     277       16        6    ATL  LAX     1946
    ## 588658            307     278       20       -6    ATL  LAX     1946
    ## 588758            291     289       24       -1    ATL  LAX     1946
    ## 589138            298     263       23       18    ATL  LAX     1946
    ## 589508            291     261       49       52    ATL  LAX     1946
    ## 589579            291     261       17       16    ATL  LAX     1946
    ## 590026            291     270       20       13    ATL  LAX     1946
    ## 590389            304     266       37       17    ATL  LAX     1946
    ## 590413            297     274       23        0    ATL  LAX     1946
    ## 590430            298     279       37        6    ATL  LAX     1946
    ## 590436            296     267       16       20    ATL  LAX     1946
    ## 590455            300     258       16       20    ATL  LAX     1946
    ## 590565            315     267       51       34    ATL  LAX     1946
    ## 591158            305     269       67       37    ATL  LAX     1946
    ## 591284            291     268       19       -2    ATL  LAX     1946
    ## 591686            304     271       59       24    ATL  LAX     1946
    ## 591711            297     281       27       -1    ATL  LAX     1946
    ## 591735            296     289       53       11    ATL  LAX     1946
    ## 591754            300     280       25       26    ATL  LAX     1946
    ## 591864            315     288       85        2    ATL  LAX     1946
    ## 592088            291     283       36       16    ATL  LAX     1946
    ## 592132            295     284       58       42    ATL  LAX     1946
    ## 592347            285     286       22        2    ATL  LAX     1946
    ## 592469            307     285      119       14    ATL  LAX     1946
    ## 592594            291     278       16        5    ATL  LAX     1946
    ## 592996            304     272       51       51    ATL  LAX     1946
    ## 593015            297     282       38        4    ATL  LAX     1946
    ## 593035            298     280       16       -1    ATL  LAX     1946
    ## 593330            291     269       18       15    ATL  LAX     1946
    ## 593632            305     272       46       51    ATL  LAX     1946
    ## 594071            297     282       50        8    ATL  LAX     1946
    ## 594089            298     272       71       67    ATL  LAX     1946
    ## 594095            296     283       17        1    ATL  LAX     1946
    ## 594113            300     273       87       91    ATL  LAX     1946
    ## 594219            315     308       36        2    ATL  LAX     1946
    ## 594681            285     278       16        1    ATL  LAX     1946
    ## 594796            307     291       37        0    ATL  LAX     1946
    ## 595328            298     271       15        7    ATL  LAX     1946
    ## 595353            300     268       16       11    ATL  LAX     1946
    ## 595461            315     284       22       -2    ATL  LAX     1946
    ## 595726            295     273       29        4    ATL  LAX     1946
    ## 596062            305     274       22        3    ATL  LAX     1946
    ## 596189            291     275       15       11    ATL  LAX     1946
    ## 596620            297     280       16        2    ATL  LAX     1946
    ## 596644            296     285       22        3    ATL  LAX     1946
    ## 596974            291     273       31       31    ATL  LAX     1946
    ## 597012            295     284       18        4    ATL  LAX     1946
    ## 597329            305     282       20        0    ATL  LAX     1946
    ## 597821            304     258       19       40    ATL  LAX     1946
    ## 598211            291     252       52       59    ATL  LAX     1946
    ## 599475            291     269       16        0    ATL  LAX     1946
    ## 599512            295     269       21       12    ATL  LAX     1946
    ## 600443            300     270       26       26    ATL  LAX     1946
    ## 601145            307     270       27       -2    ATL  LAX     1946
    ## 601671            304     257       66       85    ATL  LAX     1946
    ## 602034            295     270       39       22    ATL  LAX     1946
    ## 603104            291     259       21       29    ATL  LAX     1946
    ## 603350            285     262       15        9    ATL  LAX     1946
    ## 604003            298     275       25       14    ATL  LAX     1946
    ## 604724            305     250       22       23    ATL  LAX     1946
    ## 605591            303     276       15        6    ATL  LAX     1946
    ## 605628            291     258       34       30    ATL  LAX     1946
    ## 890284            291     284       28        8    ATL  LAX     1946
    ## 890686            300     251       71       81    ATL  LAX     1946
    ## 890878            306     253       37       50    ATL  LAX     1946
    ## 893158            296     278       16       -2    ATL  LAX     1946
    ## 893274            306     268      248      245    ATL  LAX     1946
    ## 893784            305     270      186      188    ATL  LAX     1946
    ## 894226            300     286       33       12    ATL  LAX     1946
    ## 894251            300     279       28       19    ATL  LAX     1946
    ## 894411            306     281       21        9    ATL  LAX     1946
    ## 894630            291     281       27        5    ATL  LAX     1946
    ## 894668            297     286       61       56    ATL  LAX     1946
    ## 894871            287     279       40       25    ATL  LAX     1946
    ## 894996            305     288       26       -1    ATL  LAX     1946
    ## 895491            300     271       19       17    ATL  LAX     1946
    ## 895858            303     274       26       22    ATL  LAX     1946
    ## 895891            291     274       30       13    ATL  LAX     1946
    ## 896365            291     284       25        1    ATL  LAX     1946
    ## 896759            300     266       22       -6    ATL  LAX     1946
    ## 897170            291     273       60       46    ATL  LAX     1946
    ## 897208            297     274       15        8    ATL  LAX     1946
    ## 897535            305     268       19        5    ATL  LAX     1946
    ## 898058            300     278       76       49    ATL  LAX     1946
    ## 898083            302     284       28        9    ATL  LAX     1946
    ## 898108            296     283       64       24    ATL  LAX     1946
    ## 898248            306     286       54       36    ATL  LAX     1946
    ## 898472            291     274       23        7    ATL  LAX     1946
    ## 898511            297     279       24        3    ATL  LAX     1946
    ## 898840            305     281       31       23    ATL  LAX     1946
    ## 898969            291     276       15        0    ATL  LAX     1946
    ## 899374            300     278       25        0    ATL  LAX     1946
    ## 899399            300     275       79       61    ATL  LAX     1946
    ## 899424            296     284       84       63    ATL  LAX     1946
    ## 899443            300     278       26       11    ATL  LAX     1946
    ## 899566            306     279      108      101    ATL  LAX     1946
    ## 899787            291     279       34        6    ATL  LAX     1946
    ## 899827            297     288       63       46    ATL  LAX     1946
    ## 900035            287     279       45       11    ATL  LAX     1946
    ## 900163            305     273       97      107    ATL  LAX     1946
    ## 900289            291     284       17        0    ATL  LAX     1946
    ## 900682            300     290       37       12    ATL  LAX     1946
    ## 900722            298     287       21        0    ATL  LAX     1946
    ## 900831            306     303       23        0    ATL  LAX     1946
    ## 901000            303     281       48       34    ATL  LAX     1946
    ## 901030            291     281       69       53    ATL  LAX     1946
    ## 901064            297     282       31       11    ATL  LAX     1946
    ## 901243            287     294       31        0    ATL  LAX     1946
    ## 901355            305     291       66       50    ATL  LAX     1946
    ##        TaxiIn TaxiOut Cancelled CancellationCode Diverted CarrierDelay
    ## 303503      7     251         0                         0            0
    ## 303863     10      29         0                         0           25
    ## 304349      8      16         0                         0           12
    ## 304757     14      32         0                         0            7
    ## 305126     11      18         0                         0           53
    ## 305165     14      29         0                         0           12
    ## 305385      4      19         0                         0            0
    ## 305502     15      25         0                         0            0
    ## 306087     14      13         0                         0           54
    ## 307337     13      20         0                         0           61
    ## 307356     12     109         0                         0          150
    ## 307665     14     104         0                         0            0
    ## 307871      6     159         0                         0            0
    ## 307961     16      26         0                         0            0
    ## 308409      6      21         0                         0           18
    ## 309057     27      20         0                         0            7
    ## 309502      6      31         0                         0            0
    ## 309545      6      17         0                         0            0
    ## 309551     15      10         0                         0            7
    ## 309897      9      14         0                         0           14
    ## 310262     17      24         0                         0           16
    ## 310776      6      14         0                         0            0
    ## 310794     12      15         0                         0            0
    ## 310800     11      10         0                         0            0
    ## 311164      6      25         0                         0            9
    ## 311371      9      17         0                         0            8
    ## 311482     18      23         0                         0            0
    ## 311596      7      13         0                         0            0
    ## 311973     17      24         0                         0            0
    ## 311998     12      22         0                         0            8
    ## 312016     12      18         0                         0            0
    ## 312022      7      18         0                         0            0
    ## 312144     15      19         0                         0            0
    ## 312320      6      26         0                         0            0
    ## 312358     10      17         0                         0           21
    ## 312395      7      24         0                         0            0
    ## 312612      9      18         0                         0            0
    ## 312843     16      14         0                         0            0
    ## 313228     21      26         0                         0            0
    ## 313253      9      22         0                         0            0
    ## 313271      8      21         0                         0            0
    ## 313277     15      18         0                         0            0
    ## 313296     10      13         0                         0            0
    ## 313400     21      15         0                         0            0
    ## 313621      9      14         0                         0            0
    ## 313660     10      17         0                         0            0
    ## 313880      7      14         0                         0           10
    ## 313998     17      23         0                         0            0
    ## 314526     23      21         0                         0           32
    ## 314551     10      16         0                         0            0
    ## 314575     11      25         0                         0           10
    ## 314594      8      24         0                         0            0
    ## 314697     13      17         0                         0            0
    ## 314917      9      15         0                         0           60
    ## 314956      9      23         0                         0            0
    ## 315173      7       8         0                         0            7
    ## 315293     15      24         0                         0            7
    ## 315414     11      22         0                         0            0
    ## 315817     27      17         0                         0            0
    ## 315836      9      17         0                         0            0
    ## 315851      6      23         0                         0           11
    ## 315856      9      18         0                         0            0
    ## 316175     14      12         0                         0            0
    ## 316353     11      18         0                         0            0
    ## 316446     15      29         0                         0            0
    ## 316865     18      19         0                         0           16
    ## 316908     12      18         0                         0            0
    ## 316914     14      20         0                         0           13
    ## 316932      8      29         0                         0            0
    ## 317292     14      36         0                         0            0
    ## 317502      8      22         0                         0            0
    ## 317736     14      21         0                         0            0
    ## 318137      6      19         0                         0           19
    ## 318155     13      19         0                         0            0
    ## 318161      9      20         0                         0            0
    ## 318283     52      15         0                         0            0
    ## 318546      7      15         0                         0           90
    ## 318764      7      10         0                         0            0
    ## 318882     10      18         0                         0            0
    ## 319008     12      20         0                         0            0
    ## 319751     11      28         0                         0            0
    ## 320032      7      17         0                         0            0
    ## 320257     10      17         0                         0            0
    ## 321057     11      17         0                         0           27
    ## 322658     12      26         0                         0           42
    ## 322786     11      14         0                         0           13
    ## 354084      8      15         0                         0            8
    ## 354086      9      13         0                         0           30
    ## 354829      9      12         0                         0           57
    ## 354831      7      17         0                         0           32
    ## 355570      7      21         0                         0           21
    ## 355571     12      15         0                         0            0
    ## 355572     11      15         0                         0           19
    ## 355573     10      13         0                         0           21
    ## 356319     20      15         0                         0            0
    ## 356320     23      10         0                         0            8
    ## 356321      5      19         0                         0           12
    ## 357053      7      17         0                         0           25
    ## 357781     14      16         0                         0           14
    ## 358524      7      23         0                         0            8
    ## 359256      7      34         0                         0            0
    ## 359258     17      12         0                         0           43
    ## 362419      6      23         0                         0           38
    ## 363078      8      11         0                         0           46
    ## 364325     12     163         0                         0            0
    ## 364326      4      11         0                         0            0
    ## 364928      8      17         0                         0            0
    ## 364929      7      23         0                         0           30
    ## 366255     10      47         0                         0           10
    ## 366256      6      13         0                         0            0
    ## 368224      7      10         0                         0            0
    ## 368226      8      10         0                         0            0
    ## 368820     10      14         0                         0           12
    ## 368822     11      17         0                         0            0
    ## 369424      8       9         0                         0            0
    ## 369425      4      45         0                         0            0
    ## 369426     14      14         0                         0            0
    ## 369427      6      19         0                         0            0
    ## 370088     11      12         0                         0            0
    ## 370089      5      21         0                         0            0
    ## 370090     12      16         0                         0            0
    ## 370091      4      17         0                         0           37
    ## 370752      6      13         0                         0            0
    ## 370753      6      14         0                         0            0
    ## 370754     11      12         0                         0            0
    ## 370755      5      17         0                         0           26
    ## 371405      5      22         0                         0            6
    ## 371406     23      27         0                         0            0
    ## 371407     10      14         0                         0            0
    ## 371408      5      19         0                         0            8
    ## 372070     14      13         0                         0            4
    ## 372072      8      15         0                         0            0
    ## 372073     10      17         0                         0            0
    ## 372732     15      18         0                         0            0
    ## 373330     10      11         0                         0            0
    ## 373331     23      17         0                         0            0
    ## 373933      8      19         0                         0            0
    ## 587929     29      23         0                         0          143
    ## 587971     60      20         0                         0            0
    ## 587977     16      25         0                         0            0
    ## 588097     54      20         0                         0            7
    ## 588307      8      16         0                         0            6
    ## 588658     35      20         0                         0            0
    ## 588758     11      16         0                         0            0
    ## 589138     17      23         0                         0           18
    ## 589508      8      19         0                         0           13
    ## 589579     13      18         0                         0            0
    ## 590026     10      18         0                         0           13
    ## 590389     39      19         0                         0           17
    ## 590413     22      24         0                         0            0
    ## 590430     24      26         0                         0            6
    ## 590436     13      12         0                         0           16
    ## 590455     13      25         0                         0           16
    ## 590565     43      22         0                         0           24
    ## 591158     33      33         0                         0           37
    ## 591284     23      21         0                         0            0
    ## 591686     55      13         0                         0           21
    ## 591711     30      14         0                         0            0
    ## 591735     23      26         0                         0            4
    ## 591754      5      14         0                         0           25
    ## 591864     87      23         0                         0            0
    ## 592088     13      15         0                         0           16
    ## 592132      7      20         0                         0           19
    ## 592347     10       9         0                         0            0
    ## 592469    109      18         0                         0           14
    ## 592594     12      12         0                         0            0
    ## 592996     17      15         0                         0            0
    ## 593015     29      20         0                         0            0
    ## 593035     26       9         0                         0            0
    ## 593330     14      11         0                         0           12
    ## 593632     14      14         0                         0           46
    ## 594071     42      15         0                         0            8
    ## 594089      6      24         0                         0           67
    ## 594095     13      16         0                         0            0
    ## 594113      5      18         0                         0           87
    ## 594219     12      29         0                         0            0
    ## 594681     10      12         0                         0            0
    ## 594796     38      15         0                         0            0
    ## 595328      7      28         0                         0            7
    ## 595353     14      23         0                         0           11
    ## 595461     39      16         0                         0            0
    ## 595726     20      27         0                         0            0
    ## 596062     33      17         0                         0            0
    ## 596189     10      10         0                         0           11
    ## 596620     14      17         0                         0            0
    ## 596644     10      20         0                         0            0
    ## 596974      5      13         0                         0           31
    ## 597012      6      19         0                         0            0
    ## 597329     22      21         0                         0            0
    ## 597821      6      19         0                         0           19
    ## 598211     11      21         0                         0           31
    ## 599475     17      21         0                         0            0
    ## 599512      7      28         0                         0           12
    ## 600443      7      23         0                         0           26
    ## 601145     23      43         0                         0            0
    ## 601671     15      13         0                         0           53
    ## 602034     16      26         0                         0           22
    ## 603104      6      18         0                         0            0
    ## 603350     11      18         0                         0            0
    ## 604003      8      26         0                         0            0
    ## 604724     35      19         0                         0           22
    ## 605591      6      30         0                         0            6
    ## 605628     13      24         0                         0           28
    ## 890284     12      15         0                         0            8
    ## 890686     15      24         0                         0            0
    ## 890878     24      16         0                         0           37
    ## 893158      7      29         0                         0            0
    ## 893274     11      30         0                         0          245
    ## 893784      7      26         0                         0          186
    ## 894226     14      21         0                         0           12
    ## 894251     14      16         0                         0           19
    ## 894411     11      26         0                         0            9
    ## 894630      4      28         0                         0            0
    ## 894668      3      13         0                         0            5
    ## 894871      5      18         0                         0           25
    ## 894996     20      24         0                         0            0
    ## 895491     11      20         0                         0           17
    ## 895858     17      16         0                         0           22
    ## 895891      8      26         0                         0           13
    ## 896365     12      19         0                         0            0
    ## 896759      9      53         0                         0            0
    ## 897170      6      26         0                         0           46
    ## 897208      6      24         0                         0            8
    ## 897535     23      28         0                         0            0
    ## 898058     17      32         0                         0           14
    ## 898083     12      25         0                         0            9
    ## 898108     17      36         0                         0           24
    ## 898248     27      11         0                         0            0
    ## 898472     11      22         0                         0            0
    ## 898511     12      27         0                         0            0
    ## 898840     16      16         0                         0           18
    ## 898969     18      12         0                         0            0
    ## 899374     13      34         0                         0            0
    ## 899399     13      30         0                         0           55
    ## 899424     11      22         0                         0           63
    ## 899443      9      28         0                         0            0
    ## 899566      8      26         0                         0          101
    ## 899787      8      32         0                         0            0
    ## 899827      6      20         0                         0            8
    ## 900035     14      28         0                         0            0
    ## 900163      7      15         0                         0           97
    ## 900289     11      13         0                         0            0
    ## 900682     13      22         0                         0            0
    ## 900722      8      24         0                         0            0
    ## 900831     13      13         0                         0            0
    ## 901000      7      29         0                         0           34
    ## 901030      9      17         0                         0           53
    ## 901064      7      28         0                         0           11
    ## 901243      7      17         0                         0            0
    ## 901355     12      18         0                         0           50
    ##        WeatherDelay NASDelay SecurityDelay LateAircraftDelay
    ## 303503            7      230             0                 0
    ## 303863            0        9             0                 0
    ## 304349            0        4             0                 0
    ## 304757            0       15             0                 0
    ## 305126            0        1             0                 0
    ## 305165            0       12             0                 2
    ## 305385            0        6             0                26
    ## 305502           24        0             0                 0
    ## 306087            0        0             0                 0
    ## 307337            0        0             0                 0
    ## 307356          103       87             0                 0
    ## 307665           77       86             0                 0
    ## 307871            0      140             0                 0
    ## 307961            7        3             0               112
    ## 308409            0        0             0                 0
    ## 309057            0       13             0                 0
    ## 309502            0       22             0                 0
    ## 309545            0       21             0                 0
    ## 309551            0        8             0                 0
    ## 309897            0        3             0                10
    ## 310262            0       21             0                 0
    ## 310776            0       24             0                 0
    ## 310794            0       30             0                 0
    ## 310800            0       16             0                 0
    ## 311164            0       38             0                 0
    ## 311371            0       37             0                 0
    ## 311482            0       26             0                 0
    ## 311596            0       18             0                 0
    ## 311973            0       33             0                 0
    ## 311998            0       36             0                 0
    ## 312016            0       38             0                 0
    ## 312022            0       27             0                 0
    ## 312144            0       23             0                 0
    ## 312320            0       37             0                 8
    ## 312358            0       50             0                 0
    ## 312395            0       31             0                 0
    ## 312612            0       42             0                 0
    ## 312843            0       31             0                 0
    ## 313228            0       54             0                 0
    ## 313253            0       51             0                 0
    ## 313271            0       39             0                 0
    ## 313277            0       40             0                 0
    ## 313296            0       23             0                 0
    ## 313400            0       43             0                 0
    ## 313621            0       41             0                 0
    ## 313660            0       18             0                 0
    ## 313880            0       39             0                 6
    ## 313998            0       26             0                 0
    ## 314526            0       23             0                 0
    ## 314551            0       20             0                 0
    ## 314575            0       37             0                 0
    ## 314594            0       35             0                 0
    ## 314697            0       33             0                 0
    ## 314917            0       23             0                12
    ## 314956            0       38             0                 0
    ## 315173            0       38             0                 0
    ## 315293            0       35             0                 0
    ## 315414            0       29             0                 0
    ## 315817            0       42             0                 0
    ## 315836            0       41             0                 0
    ## 315851            0        6             0                 0
    ## 315856            0       48             0                 0
    ## 316175            0       47             0                93
    ## 316353            0       53             0                 0
    ## 316446            0       57             0                 0
    ## 316865            0        1             0                28
    ## 316908            0       17             0                 0
    ## 316914            0       15             0                 0
    ## 316932            0       19             0                 0
    ## 317292            0       46             0                 0
    ## 317502            0       25             0                 0
    ## 317736            0       30             0                 0
    ## 318137            0       13             0                 0
    ## 318155            0       21             0                 0
    ## 318161            0       30             0                 0
    ## 318283            0       38             0                 0
    ## 318546            0       15             0                 0
    ## 318764            0       17             0                 0
    ## 318882            0       17             0                 0
    ## 319008            0       28             0                 0
    ## 319751            0       23             0                 0
    ## 320032            0       21             0                 0
    ## 320257            0       17             0                 0
    ## 321057            0        6             0                 0
    ## 322658            0        6             0                 0
    ## 322786            0       17             0                 0
    ## 354084            0        7             0                 0
    ## 354086            0        0             0                 0
    ## 354829            0        0             0                 0
    ## 354831            0        0             0                 0
    ## 355570            0        0             0                 0
    ## 355571            0        0             0                18
    ## 355572            0        3             0                 0
    ## 355573            0        2             0                 0
    ## 356319            0       15             0                 0
    ## 356320            0       20             0                 0
    ## 356321            0       16             0                 0
    ## 357053            0       12             0                 0
    ## 357781            0       21             0                 0
    ## 358524            0       11             0                 0
    ## 359256            0       17             0                11
    ## 359258            0       25             0                 0
    ## 362419            0        0             0                 0
    ## 363078            0        0             0                 0
    ## 364325            0      143             0                 0
    ## 364326            0        0             0               124
    ## 364928            0        0             0                36
    ## 364929            0        0             0                 0
    ## 366255            0       22             0                 0
    ## 366256            0        0             0               159
    ## 368224            0       12             0                 8
    ## 368226            0       17             0                 0
    ## 368820            0       18             0                 0
    ## 368822            0       34             0                 0
    ## 369424            0       19             0                 7
    ## 369425            0       36             0                 0
    ## 369426            0       48             0                 0
    ## 369427            0       24             0                 3
    ## 370088            0       23             0                 0
    ## 370089            0       33             0                 0
    ## 370090            0       32             0                 0
    ## 370091            0       40             0                 0
    ## 370752            0       34             0                 0
    ## 370753            0       44             0                 0
    ## 370754            0       33             0                 0
    ## 370755            0       52             0                 0
    ## 371405            0       31             0                 0
    ## 371406            0       64             0                 0
    ## 371407            0       35             0                 0
    ## 371408            0       22             0                 0
    ## 372070            0       18             0                 0
    ## 372072            0       18             0                 0
    ## 372073            0       20             0                 0
    ## 372732            0       17             0                 0
    ## 373330            0        0             0                38
    ## 373331            0       15             0                 0
    ## 373933            0        0             0                37
    ## 587929            0       23             0                 0
    ## 587971            0       50             0                 0
    ## 587977            0       22             0                 0
    ## 588097            0       35             0                 0
    ## 588307            0       10             0                 0
    ## 588658            0       20             0                 0
    ## 588758            0       24             0                 0
    ## 589138            0        5             0                 0
    ## 589508            0        0             0                36
    ## 589579            0        1             0                16
    ## 590026            0        7             0                 0
    ## 590389            0       20             0                 0
    ## 590413            0       23             0                 0
    ## 590430            0       31             0                 0
    ## 590436            0        0             0                 0
    ## 590455            0        0             0                 0
    ## 590565            0       17             0                10
    ## 591158            0       30             0                 0
    ## 591284            0       19             0                 0
    ## 591686            0       35             0                 3
    ## 591711            0       27             0                 0
    ## 591735            0       42             0                 7
    ## 591754            0        0             0                 0
    ## 591864            0       85             0                 0
    ## 592088            0       20             0                 0
    ## 592132            0       16             0                23
    ## 592347            0       22             0                 0
    ## 592469            0      105             0                 0
    ## 592594            0       16             0                 0
    ## 592996            0        0             0                51
    ## 593015            0       38             0                 0
    ## 593035            0       16             0                 0
    ## 593330            0        3             0                 3
    ## 593632            0        0             0                 0
    ## 594071            0       42             0                 0
    ## 594089            0        4             0                 0
    ## 594095            0       17             0                 0
    ## 594113            0        0             0                 0
    ## 594219            0       36             0                 0
    ## 594681            0       16             0                 0
    ## 594796            0       37             0                 0
    ## 595328            0        8             0                 0
    ## 595353            0        5             0                 0
    ## 595461            0       22             0                 0
    ## 595726            0       29             0                 0
    ## 596062            0       22             0                 0
    ## 596189            0        4             0                 0
    ## 596620            0       16             0                 0
    ## 596644            0       22             0                 0
    ## 596974            0        0             0                 0
    ## 597012            0       18             0                 0
    ## 597329            0       20             0                 0
    ## 597821            0        0             0                 0
    ## 598211            0        0             0                21
    ## 599475            0       16             0                 0
    ## 599512            0        9             0                 0
    ## 600443            0        0             0                 0
    ## 601145            0       27             0                 0
    ## 601671            0        0             0                13
    ## 602034            0       17             0                 0
    ## 603104            0        0             0                21
    ## 603350            0        6             0                 9
    ## 604003            0       11             0                14
    ## 604724            0        0             0                 0
    ## 605591            0        9             0                 0
    ## 605628            0        4             0                 2
    ## 890284            0       20             0                 0
    ## 890686            0        0             0                71
    ## 890878            0        0             0                 0
    ## 893158            0       16             0                 0
    ## 893274            0        3             0                 0
    ## 893784            0        0             0                 0
    ## 894226            0       21             0                 0
    ## 894251            0        9             0                 0
    ## 894411            0       12             0                 0
    ## 894630            0       27             0                 0
    ## 894668            0        5             0                51
    ## 894871            0       15             0                 0
    ## 894996            0       26             0                 0
    ## 895491            0        2             0                 0
    ## 895858            0        4             0                 0
    ## 895891            0       17             0                 0
    ## 896365            0       25             0                 0
    ## 896759            0       22             0                 0
    ## 897170            0       14             0                 0
    ## 897208            0        7             0                 0
    ## 897535            0       19             0                 0
    ## 898058            0       27             0                35
    ## 898083            0       19             0                 0
    ## 898108            0       40             0                 0
    ## 898248            0       18             0                36
    ## 898472            0       16             0                 7
    ## 898511            0       24             0                 0
    ## 898840            5        8             0                 0
    ## 898969            0       15             0                 0
    ## 899374            0       25             0                 0
    ## 899399            0       18             0                 6
    ## 899424            0       21             0                 0
    ## 899443            0       15             0                11
    ## 899566            0        7             0                 0
    ## 899787            0       28             0                 6
    ## 899827            4       17             0                34
    ## 900035            0       34             0                11
    ## 900163            0        0             0                 0
    ## 900289            0       17             0                 0
    ## 900682            0       25             0                12
    ## 900722            0       21             0                 0
    ## 900831            0       23             0                 0
    ## 901000            0       14             0                 0
    ## 901030            0       16             0                 0
    ## 901064            0       20             0                 0
    ## 901243            0       31             0                 0
    ## 901355            0       16             0                 0
    ##                  timestamp depHour
    ## 303503 2019-03-13 17:42:00      17
    ## 303863 2019-03-13 15:05:00      15
    ## 304349 2019-03-13 07:12:00       7
    ## 304757 2019-03-13 17:42:00      17
    ## 305126 2019-03-13 15:33:00      15
    ## 305165 2019-03-13 11:14:00      11
    ## 305385 2019-03-13 13:56:00      13
    ## 305502 2019-03-13 21:45:00      21
    ## 306087 2019-03-13 16:58:00      16
    ## 307337 2019-03-13 20:07:00      20
    ## 307356 2019-03-13 21:48:00      21
    ## 307665 2019-03-13 15:57:00      15
    ## 307871 2019-03-13 13:34:00      13
    ## 307961 2019-03-13 23:19:00      23
    ## 308409 2019-03-13 16:21:00      16
    ## 309057 2019-03-13 21:27:00      21
    ## 309502 2019-03-13 18:53:00      18
    ## 309545 2019-03-13 08:34:00       8
    ## 309551 2019-03-13 16:07:00      16
    ## 309897 2019-03-13 15:04:00      15
    ## 310262 2019-03-13 21:36:00      21
    ## 310776 2019-03-13 17:33:00      17
    ## 310794 2019-03-13 08:35:00       8
    ## 310800 2019-03-13 15:59:00      15
    ## 311164 2019-03-13 11:09:00      11
    ## 311371 2019-03-13 13:38:00      13
    ## 311482 2019-03-13 21:17:00      21
    ## 311596 2019-03-13 07:02:00       7
    ## 311973 2019-03-13 18:50:00      18
    ## 311998 2019-03-13 17:43:00      17
    ## 312016 2019-03-13 08:33:00       8
    ## 312022 2019-03-13 16:01:00      16
    ## 312144 2019-03-13 21:17:00      21
    ## 312320 2019-03-13 09:58:00       9
    ## 312358 2019-03-13 15:01:00      15
    ## 312395 2019-03-13 10:58:00      10
    ## 312612 2019-03-13 13:30:00      13
    ## 312843 2019-03-13 06:58:00       6
    ## 313228 2019-03-13 18:47:00      18
    ## 313253 2019-03-13 17:40:00      17
    ## 313271 2019-03-13 08:34:00       8
    ## 313277 2019-03-13 16:03:00      16
    ## 313296 2019-03-13 09:50:00       9
    ## 313400 2019-03-13 20:01:00      20
    ## 313621 2019-03-13 14:44:00      14
    ## 313660 2019-03-13 10:55:00      10
    ## 313880 2019-03-13 13:46:00      13
    ## 313998 2019-03-13 21:15:00      21
    ## 314526 2019-03-13 19:22:00      19
    ## 314551 2019-03-13 17:34:00      17
    ## 314575 2019-03-13 16:10:00      16
    ## 314594 2019-03-13 09:50:00       9
    ## 314697 2019-03-13 20:01:00      20
    ## 314917 2019-03-13 15:52:00      15
    ## 314956 2019-03-13 10:59:00      10
    ## 315173 2019-03-13 13:37:00      13
    ## 315293 2019-03-13 21:27:00      21
    ## 315414 2019-03-13 06:56:00       6
    ## 315817 2019-03-13 18:45:00      18
    ## 315836 2019-03-13 17:35:00      17
    ## 315851 2019-03-13 08:46:00       8
    ## 315856 2019-03-13 15:59:00      15
    ## 316175 2019-03-13 12:33:00      12
    ## 316353 2019-03-13 13:30:00      13
    ## 316446 2019-03-13 21:21:00      21
    ## 316865 2019-03-13 19:34:00      19
    ## 316908 2019-03-13 08:35:00       8
    ## 316914 2019-03-13 16:13:00      16
    ## 316932 2019-03-13 09:50:00       9
    ## 317292 2019-03-13 10:56:00      10
    ## 317502 2019-03-13 13:25:00      13
    ## 317736 2019-03-13 06:57:00       6
    ## 318137 2019-03-13 17:54:00      17
    ## 318155 2019-03-13 08:40:00       8
    ## 318161 2019-03-13 15:59:00      15
    ## 318283 2019-03-13 19:58:00      19
    ## 318546 2019-03-13 12:30:00      12
    ## 318764 2019-03-13 13:28:00      13
    ## 318882 2019-03-13 21:16:00      21
    ## 319008 2019-03-13 07:02:00       7
    ## 319751 2019-03-13 09:52:00       9
    ## 320032 2019-03-13 13:28:00      13
    ## 320257 2019-03-13 06:57:00       6
    ## 321057 2019-03-13 11:27:00      11
    ## 322658 2019-03-13 22:02:00      22
    ## 322786 2019-03-13 07:13:00       7
    ## 354084 2019-03-13 10:55:00      10
    ## 354086 2019-03-13 21:55:00      21
    ## 354829 2019-03-13 11:54:00      11
    ## 354831 2019-03-13 22:04:00      22
    ## 355570 2019-03-13 09:57:00       9
    ## 355571 2019-03-13 11:08:00      11
    ## 355572 2019-03-13 18:18:00      18
    ## 355573 2019-03-13 21:46:00      21
    ## 356319 2019-03-13 10:43:00      10
    ## 356320 2019-03-13 18:07:00      18
    ## 356321 2019-03-13 21:37:00      21
    ## 357053 2019-03-13 11:12:00      11
    ## 357781 2019-03-13 21:39:00      21
    ## 358524 2019-03-13 09:38:00       9
    ## 359256 2019-03-13 09:41:00       9
    ## 359258 2019-03-13 18:42:00      18
    ## 362419 2019-03-13 18:53:00      18
    ## 363078 2019-03-13 22:30:00      22
    ## 364325 2019-03-13 17:58:00      17
    ## 364326 2019-03-13 23:46:00      23
    ## 364928 2019-03-13 18:40:00      18
    ## 364929 2019-03-13 21:56:00      21
    ## 366255 2019-03-13 10:47:00      10
    ## 366256 2019-03-13 20:53:00      20
    ## 368224 2019-03-13 09:38:00       9
    ## 368226 2019-03-13 17:57:00      17
    ## 368820 2019-03-13 09:42:00       9
    ## 368822 2019-03-13 17:57:00      17
    ## 369424 2019-03-13 09:37:00       9
    ## 369425 2019-03-13 10:29:00      10
    ## 369426 2019-03-13 17:56:00      17
    ## 369427 2019-03-13 21:28:00      21
    ## 370088 2019-03-13 09:30:00       9
    ## 370089 2019-03-13 10:33:00      10
    ## 370090 2019-03-13 17:57:00      17
    ## 370091 2019-03-13 22:02:00      22
    ## 370752 2019-03-13 09:30:00       9
    ## 370753 2019-03-13 10:34:00      10
    ## 370754 2019-03-13 17:58:00      17
    ## 370755 2019-03-13 21:51:00      21
    ## 371405 2019-03-13 09:36:00       9
    ## 371406 2019-03-13 10:36:00      10
    ## 371407 2019-03-13 17:59:00      17
    ## 371408 2019-03-13 21:33:00      21
    ## 372070 2019-03-13 09:34:00       9
    ## 372072 2019-03-13 17:54:00      17
    ## 372073 2019-03-13 21:19:00      21
    ## 372732 2019-03-13 10:35:00      10
    ## 373330 2019-03-13 18:38:00      18
    ## 373331 2019-03-13 21:22:00      21
    ## 373933 2019-03-13 22:02:00      22
    ## 587929 2019-03-13 21:13:00      21
    ## 587971 2019-03-13 08:37:00       8
    ## 587977 2019-03-13 16:01:00      16
    ## 588097 2019-03-13 20:07:00      20
    ## 588307 2019-03-13 14:46:00      14
    ## 588658 2019-03-13 21:29:00      21
    ## 588758 2019-03-13 06:59:00       6
    ## 589138 2019-03-13 08:53:00       8
    ## 589508 2019-03-13 15:32:00      15
    ## 589579 2019-03-13 12:18:00      12
    ## 590026 2019-03-13 07:13:00       7
    ## 590389 2019-03-13 19:07:00      19
    ## 590413 2019-03-13 17:35:00      17
    ## 590430 2019-03-13 08:41:00       8
    ## 590436 2019-03-13 16:20:00      16
    ## 590455 2019-03-13 10:10:00      10
    ## 590565 2019-03-13 20:34:00      20
    ## 591158 2019-03-13 21:57:00      21
    ## 591284 2019-03-13 06:58:00       6
    ## 591686 2019-03-13 19:14:00      19
    ## 591711 2019-03-13 17:34:00      17
    ## 591735 2019-03-13 16:11:00      16
    ## 591754 2019-03-13 10:16:00      10
    ## 591864 2019-03-13 20:02:00      20
    ## 592088 2019-03-13 14:56:00      14
    ## 592132 2019-03-13 11:42:00      11
    ## 592347 2019-03-13 13:32:00      13
    ## 592469 2019-03-13 21:34:00      21
    ## 592594 2019-03-13 07:05:00       7
    ## 592996 2019-03-13 19:41:00      19
    ## 593015 2019-03-13 17:39:00      17
    ## 593035 2019-03-13 15:59:00      15
    ## 593330 2019-03-13 14:55:00      14
    ## 593632 2019-03-13 22:11:00      22
    ## 594071 2019-03-13 17:43:00      17
    ## 594089 2019-03-13 09:42:00       9
    ## 594095 2019-03-13 16:01:00      16
    ## 594113 2019-03-13 11:21:00      11
    ## 594219 2019-03-13 20:02:00      20
    ## 594681 2019-03-13 13:31:00      13
    ## 594796 2019-03-13 21:00:00      21
    ## 595328 2019-03-13 08:42:00       8
    ## 595353 2019-03-13 10:01:00      10
    ## 595461 2019-03-13 19:58:00      19
    ## 595726 2019-03-13 11:04:00      11
    ## 596062 2019-03-13 21:23:00      21
    ## 596189 2019-03-13 07:11:00       7
    ## 596620 2019-03-13 17:37:00      17
    ## 596644 2019-03-13 16:03:00      16
    ## 596974 2019-03-13 15:11:00      15
    ## 597012 2019-03-13 11:04:00      11
    ## 597329 2019-03-13 21:20:00      21
    ## 597821 2019-03-13 19:30:00      19
    ## 598211 2019-03-13 15:39:00      15
    ## 599475 2019-03-13 14:40:00      14
    ## 599512 2019-03-13 11:12:00      11
    ## 600443 2019-03-13 10:16:00      10
    ## 601145 2019-03-13 21:18:00      21
    ## 601671 2019-03-13 20:15:00      20
    ## 602034 2019-03-13 11:22:00      11
    ## 603104 2019-03-13 15:09:00      15
    ## 603350 2019-03-13 13:39:00      13
    ## 604003 2019-03-13 08:49:00       8
    ## 604724 2019-03-13 21:43:00      21
    ## 605591 2019-03-13 09:56:00       9
    ## 605628 2019-03-13 15:10:00      15
    ## 890284 2019-03-13 07:08:00       7
    ## 890686 2019-03-13 20:36:00      20
    ## 890878 2019-03-13 21:10:00      21
    ## 893158 2019-03-13 15:58:00      15
    ## 893274 2019-03-13 00:25:00       0
    ## 893784 2019-03-13 00:48:00       0
    ## 894226 2019-03-13 19:27:00      19
    ## 894251 2019-03-13 17:24:00      17
    ## 894411 2019-03-13 20:29:00      20
    ## 894630 2019-03-13 14:45:00      14
    ## 894668 2019-03-13 12:06:00      12
    ## 894871 2019-03-13 13:55:00      13
    ## 894996 2019-03-13 21:39:00      21
    ## 895491 2019-03-13 19:32:00      19
    ## 895858 2019-03-13 10:12:00      10
    ## 895891 2019-03-13 14:53:00      14
    ## 896365 2019-03-13 07:01:00       7
    ## 896759 2019-03-13 19:09:00      19
    ## 897170 2019-03-13 15:26:00      15
    ## 897208 2019-03-13 11:18:00      11
    ## 897535 2019-03-13 21:45:00      21
    ## 898058 2019-03-13 20:04:00      20
    ## 898083 2019-03-13 17:14:00      17
    ## 898108 2019-03-13 16:24:00      16
    ## 898248 2019-03-13 20:56:00      20
    ## 898472 2019-03-13 14:47:00      14
    ## 898511 2019-03-13 11:13:00      11
    ## 898840 2019-03-13 22:03:00      22
    ## 898969 2019-03-13 07:00:00       7
    ## 899374 2019-03-13 19:15:00      19
    ## 899399 2019-03-13 18:06:00      18
    ## 899424 2019-03-13 17:03:00      17
    ## 899443 2019-03-13 10:01:00      10
    ## 899566 2019-03-13 22:01:00      22
    ## 899787 2019-03-13 14:46:00      14
    ## 899827 2019-03-13 11:56:00      11
    ## 900035 2019-03-13 13:41:00      13
    ## 900163 2019-03-13 23:27:00      23
    ## 900289 2019-03-13 07:00:00       7
    ## 900682 2019-03-13 19:27:00      19
    ## 900722 2019-03-13 08:35:00       8
    ## 900831 2019-03-13 20:20:00      20
    ## 901000 2019-03-13 10:24:00      10
    ## 901030 2019-03-13 15:33:00      15
    ## 901064 2019-03-13 11:21:00      11
    ## 901243 2019-03-13 13:30:00      13
    ## 901355 2019-03-13 22:30:00      22

Now, let’s generate a plot of these, grouped by
hour:

``` r
hist(atllaxflights_clean$depHour, main="ATL to LAX Flights by Hour of Day, 2008", xlab="Hour of Day", ylab="Number of Flights", border="blue")
```

![](Intro_to_R_Week_1_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

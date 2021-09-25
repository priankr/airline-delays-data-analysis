The data was downloaded from CORGIS Dataset Project:
<a href="https://think.cs.vt.edu/corgis/csv/airlines/">Original
Dataset</a>

This dataset is all about flights in the united states, including
information about the number, length, and type of delays between
2003-2016. The data is reported for individual months at every major
airport for every carrier.

    library(tidyverse)

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.2     ✓ dplyr   1.0.7
    ## ✓ tidyr   1.1.3     ✓ stringr 1.4.0
    ## ✓ readr   1.4.0     ✓ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

    library(ggplot2)
    library(gghighlight)

    #Importing the csv file to a books Data Frame
    delays <- read.csv("airlines.csv")

    #Viewing the Data Frame
    head(delays)

    ##   Airport.Code
    ## 1          ATL
    ## 2          BOS
    ## 3          BWI
    ## 4          CLT
    ## 5          DCA
    ## 6          DEN
    ##                                                          Airport.Name
    ## 1               Atlanta, GA: Hartsfield-Jackson Atlanta International
    ## 2                                     Boston, MA: Logan International
    ## 3 Baltimore, MD: Baltimore/Washington International Thurgood Marshall
    ## 4                      Charlotte, NC: Charlotte Douglas International
    ## 5                   Washington, DC: Ronald Reagan Washington National
    ## 6                                    Denver, CO: Denver International
    ##   Time.Label Time.Month Time.Month.Name Time.Year
    ## 1    2003/06          6            June      2003
    ## 2    2003/06          6            June      2003
    ## 3    2003/06          6            June      2003
    ## 4    2003/06          6            June      2003
    ## 5    2003/06          6            June      2003
    ## 6    2003/06          6            June      2003
    ##   Statistics...of.Delays.Carrier Statistics...of.Delays.Late.Aircraft
    ## 1                           1009                                 1275
    ## 2                            374                                  495
    ## 3                            296                                  477
    ## 4                            300                                  472
    ## 5                            283                                  268
    ## 6                            516                                  323
    ##   Statistics...of.Delays.National.Aviation.System
    ## 1                                            3217
    ## 2                                             685
    ## 3                                             389
    ## 4                                             735
    ## 5                                             487
    ## 6                                             664
    ##   Statistics...of.Delays.Security Statistics...of.Delays.Weather
    ## 1                              17                            328
    ## 2                               3                             66
    ## 3                               8                             78
    ## 4                               2                             54
    ## 5                               4                             58
    ## 6                              11                             98
    ##                                                                                                                                                                                                                                                                                                                           Statistics.Carriers.Names
    ## 1                                                                                  American Airlines Inc.,JetBlue Airways,Continental Air Lines Inc.,Delta Air Lines Inc.,Atlantic Southeast Airlines,AirTran Airways Corporation,America West Airlines Inc.,Northwest Airlines Inc.,ExpressJet Airlines Inc.,United Air Lines Inc.,US Airways Inc.
    ## 2 American Airlines Inc.,Alaska Airlines Inc.,Continental Air Lines Inc.,Atlantic Coast Airlines,Delta Air Lines Inc.,Atlantic Southeast Airlines,AirTran Airways Corporation,America West Airlines Inc.,American Eagle Airlines Inc.,Northwest Airlines Inc.,ExpressJet Airlines Inc.,ATA Airlines d/b/a ATA,United Air Lines Inc.,US Airways Inc.
    ## 3                                                                          American Airlines Inc.,Continental Air Lines Inc.,Delta Air Lines Inc.,AirTran Airways Corporation,America West Airlines Inc.,American Eagle Airlines Inc.,Northwest Airlines Inc.,ExpressJet Airlines Inc.,United Air Lines Inc.,US Airways Inc.,Southwest Airlines Co.
    ## 4                                                                             American Airlines Inc.,Continental Air Lines Inc.,Atlantic Coast Airlines,Delta Air Lines Inc.,Atlantic Southeast Airlines,American Eagle Airlines Inc.,Northwest Airlines Inc.,ExpressJet Airlines Inc.,ATA Airlines d/b/a ATA,United Air Lines Inc.,US Airways Inc.
    ## 5                             American Airlines Inc.,Alaska Airlines Inc.,Continental Air Lines Inc.,Atlantic Coast Airlines,Delta Air Lines Inc.,Atlantic Southeast Airlines,America West Airlines Inc.,American Eagle Airlines Inc.,Northwest Airlines Inc.,ExpressJet Airlines Inc.,ATA Airlines d/b/a ATA,United Air Lines Inc.,US Airways Inc.
    ## 6                                         American Airlines Inc.,Alaska Airlines Inc.,JetBlue Airways,Continental Air Lines Inc.,Delta Air Lines Inc.,Atlantic Southeast Airlines,AirTran Airways Corporation,America West Airlines Inc.,Northwest Airlines Inc.,SkyWest Airlines Inc.,ATA Airlines d/b/a ATA,United Air Lines Inc.,US Airways Inc.
    ##   Statistics.Carriers.Total Statistics.Flights.Cancelled
    ## 1                        11                          216
    ## 2                        14                          138
    ## 3                        11                           29
    ## 4                        11                           73
    ## 5                        13                           74
    ## 6                        13                           34
    ##   Statistics.Flights.Delayed Statistics.Flights.Diverted
    ## 1                       5843                          27
    ## 2                       1623                           3
    ## 3                       1245                          15
    ## 4                       1562                          14
    ## 5                       1100                          18
    ## 6                       1611                          22
    ##   Statistics.Flights.On.Time Statistics.Flights.Total
    ## 1                      23974                    30060
    ## 2                       7875                     9639
    ## 3                       6998                     8287
    ## 4                       7021                     8670
    ## 5                       5321                     6513
    ## 6                      10024                    11691
    ##   Statistics.Minutes.Delayed.Carrier Statistics.Minutes.Delayed.Late.Aircraft
    ## 1                              61606                                    68335
    ## 2                              20319                                    28189
    ## 3                              13635                                    26810
    ## 4                              14763                                    23379
    ## 5                              13775                                    13712
    ## 6                              26634                                    18969
    ##   Statistics.Minutes.Delayed.National.Aviation.System
    ## 1                                              118831
    ## 2                                               24400
    ## 3                                               17556
    ## 4                                               23804
    ## 5                                               20999
    ## 6                                               23538
    ##   Statistics.Minutes.Delayed.Security Statistics.Minutes.Delayed.Total
    ## 1                                 518                           268764
    ## 2                                  99                            77167
    ## 3                                 278                            64480
    ## 4                                 127                            65865
    ## 5                                 120                            52747
    ## 6                                 706                            75428
    ##   Statistics.Minutes.Delayed.Weather
    ## 1                              19474
    ## 2                               4160
    ## 3                               6201
    ## 4                               3792
    ## 5                               4141
    ## 6                               5581

### Missing Values

    #Identifying total number of missing values
    sum(is.na(delays))

    ## [1] 0

There are no missing values in the data.

    #Identifying the column names
    colnames(delays)

    ##  [1] "Airport.Code"                                       
    ##  [2] "Airport.Name"                                       
    ##  [3] "Time.Label"                                         
    ##  [4] "Time.Month"                                         
    ##  [5] "Time.Month.Name"                                    
    ##  [6] "Time.Year"                                          
    ##  [7] "Statistics...of.Delays.Carrier"                     
    ##  [8] "Statistics...of.Delays.Late.Aircraft"               
    ##  [9] "Statistics...of.Delays.National.Aviation.System"    
    ## [10] "Statistics...of.Delays.Security"                    
    ## [11] "Statistics...of.Delays.Weather"                     
    ## [12] "Statistics.Carriers.Names"                          
    ## [13] "Statistics.Carriers.Total"                          
    ## [14] "Statistics.Flights.Cancelled"                       
    ## [15] "Statistics.Flights.Delayed"                         
    ## [16] "Statistics.Flights.Diverted"                        
    ## [17] "Statistics.Flights.On.Time"                         
    ## [18] "Statistics.Flights.Total"                           
    ## [19] "Statistics.Minutes.Delayed.Carrier"                 
    ## [20] "Statistics.Minutes.Delayed.Late.Aircraft"           
    ## [21] "Statistics.Minutes.Delayed.National.Aviation.System"
    ## [22] "Statistics.Minutes.Delayed.Security"                
    ## [23] "Statistics.Minutes.Delayed.Total"                   
    ## [24] "Statistics.Minutes.Delayed.Weather"

As there are quite a few columns it might be helpful to look at a some
some subsets of the data.

We can look at three subsets specifically:

-   Number of Flights Delayed Overall
-   Number of Flights Delayed by Reason
-   Duration of Flight Delay

<!-- -->

    #Creating a character vector named flights in which we are storing column names
    flights <- c("Airport.Code","Airport.Name","Time.Month","Time.Month.Name","Time.Year","Statistics.Flights.Cancelled","Statistics.Flights.Delayed","Statistics.Flights.Diverted","Statistics.Flights.On.Time","Statistics.Flights.Total")

    #Creating a data frame with information on number of delays
    delays_flights <-delays[flights]

    #Creating a character vector named flights in which we are storing column names
    reason <- c("Airport.Code","Airport.Name","Time.Month","Time.Month.Name","Time.Year", "Statistics...of.Delays.Carrier","Statistics...of.Delays.Late.Aircraft", "Statistics...of.Delays.National.Aviation.System","Statistics...of.Delays.Security","Statistics...of.Delays.Weather")

    #Creating a data frame with information on number of delays due to different reasons
    delays_reason <-delays[reason]

    #Creating a character vector named duration in which we are storing column names
    duration <- c("Airport.Code","Airport.Name","Time.Month","Time.Month.Name","Time.Year","Statistics.Minutes.Delayed.Carrier","Statistics.Minutes.Delayed.Late.Aircraft","Statistics.Minutes.Delayed.National.Aviation.System","Statistics.Minutes.Delayed.Security","Statistics.Minutes.Delayed.Total","Statistics.Minutes.Delayed.Weather")

    #Creating a data frame with information on duration of delays
    delays_duration <-delays[duration]

# Flight Data: Number of Flights Delayed Overall

## Average Flights per Month

The average percentage of flights cancelled, delayed, diverted and on
time between 2003-2016.

    #Average number of delayed flights per month since 2003
    avg_flights_cancelled <- sum(delays_flights$Statistics.Flights.Cancelled)

    #Average number of delayed flights per month since 2003
    avg_flights_delayed <- sum(delays_flights$Statistics.Flights.Delayed)

    #Average number of diverted flights per month since 2003
    avg_flights_diverted <- sum(delays_flights$Statistics.Flights.Diverted)

    #Average number of flights on time per month since 2003
    avg_flights_on_time <- sum(delays_flights$Statistics.Flights.On.Time)

    #Creating a Pie Chart 
    flights_values = c(avg_flights_cancelled,avg_flights_delayed,avg_flights_diverted,avg_flights_on_time )
    flights_labels = c("Cancelled","Delayed","Diverted","On Time")

    #Calculating the percent each will be of the total
    piepercent<- round(100*flights_values/sum(flights_values), 1)

    # Plot the chart.
    pie(flights_values, labels = piepercent, main = "Distribution of Flights per Month between 2003-2016",col = rainbow(length(flights_values)))
    legend("topright", flights_labels, cex = 0.8,fill = rainbow(length(flights_values)))

![](airport_delays_files/figure-markdown_strict/unnamed-chunk-5-1.png)
On average, <b>77.8%</b> of flights were On Time each month and
<b>20.2%</b> of flights were Delayed.

## Average Flights per Month by Month of Year

The average percentage of flights cancelled, delayed, diverted and on
time per month between 2003-2016.

    #Grouping by month
    month <- delays_flights %>% group_by(Time.Month)

    #Creating a data frame to store the summarized values of flights cancelled each year
    delays_flights_month <- month %>% summarise(Statistics.Flights.Cancelled = mean(Statistics.Flights.Cancelled))

    #Renaming the columns
    colnames(delays_flights_month)[which(names(delays_flights_month) == "Time.Month")] <- "Month"
    colnames(delays_flights_month)[which(names(delays_flights_month) == "Statistics.Flights.Cancelled")] <- "Cancelled"

    #Summarizing by number of flights delayed each year
    month_delayed <- month %>% summarise(Statistics.Flights.Delayed = mean(Statistics.Flights.Delayed))

    #Adding the column to delays_flights_month
    delays_flights_month$Delayed <-month_delayed$Statistics.Flights.Delayed

    #Summarizing by number of flights delayed
    month_delayed <- month %>% summarise(Statistics.Flights.Delayed = mean(Statistics.Flights.Delayed))
    delays_flights_month$Delayed <-month_delayed$Statistics.Flights.Delayed

    #Summarizing by number of flights diverted
    month_diverted <- month %>% summarise(Statistics.Flights.Diverted = mean(Statistics.Flights.Diverted))
    delays_flights_month$Diverted <-month_diverted$Statistics.Flights.Diverted

    #Summarizing by number of flights on time
    month_on_time <- month %>% summarise(Statistics.Flights.On.Time = mean(Statistics.Flights.On.Time))
    delays_flights_month$On_Time <-month_on_time$Statistics.Flights.On.Time

    #Creating a column to display percentage of flights that were on time, on average
    delays_flights_month$Percent_On_Time <-100*delays_flights_month$On_Time/(delays_flights_month$On_Time+delays_flights_month$Diverted+delays_flights_month$Delayed+delays_flights_month$Cancelled)

    #Display averages for numbers of flights cancelled, delayed, diverted and on time
    round(delays_flights_month) 

    ## # A tibble: 12 x 6
    ##    Month Cancelled Delayed Diverted On_Time Percent_On_Time
    ##    <dbl>     <dbl>   <dbl>    <dbl>   <dbl>           <dbl>
    ##  1     1       341    2411       22    8801              76
    ##  2     2       361    2303       20    8125              75
    ##  3     3       223    2513       23    9525              78
    ##  4     4       159    2204       25    9475              80
    ##  5     5       155    2348       33    9642              79
    ##  6     6       209    2880       45    9037              74
    ##  7     7       210    2877       44    9481              75
    ##  8     8       196    2555       38    9747              78
    ##  9     9       158    1774       21    9549              83
    ## 10    10       149    2079       19    9752              81
    ## 11    11       118    1939       18    9350              82
    ## 12    12       287    2923       25    8549              73

    #Identifying month with the greatest percent of flights on time, on overage
    round(delays_flights_month[which.max(delays_flights_month$Percent_On_Time),])

    ## # A tibble: 1 x 6
    ##   Month Cancelled Delayed Diverted On_Time Percent_On_Time
    ##   <dbl>     <dbl>   <dbl>    <dbl>   <dbl>           <dbl>
    ## 1     9       158    1774       21    9549              83

    #Identifying year with the least percent of flights on time, on overage
    round(delays_flights_month[which.min(delays_flights_month$Percent_On_Time),])

    ## # A tibble: 1 x 6
    ##   Month Cancelled Delayed Diverted On_Time Percent_On_Time
    ##   <dbl>     <dbl>   <dbl>    <dbl>   <dbl>           <dbl>
    ## 1    12       287    2923       25    8549              73

On average, flights were on time each month the most in <b>September</b>
and they were on time the least in <b>December.</b>

## Average Flights per Month by Year

The average number of flights cancelled, delayed, diverted and on time
per month, each year between 2003-2016.

    #Grouping by year
    year <- delays_flights %>% group_by(Time.Year)

    #Creating a data frame to store the summarized values of flights cancelled each year
    delays_flights_year <- year %>% summarise(Statistics.Flights.Cancelled = mean(Statistics.Flights.Cancelled))

    #Renaming the columns
    colnames(delays_flights_year)[which(names(delays_flights_year) == "Time.Year")] <- "Year"
    colnames(delays_flights_year)[which(names(delays_flights_year) == "Statistics.Flights.Cancelled")] <- "Cancelled"

    #Summarizing by number of flights delayed each year
    year_delayed <- year %>% summarise(Statistics.Flights.Delayed = mean(Statistics.Flights.Delayed))

    #Adding the column to delays_flights_year
    delays_flights_year$Delayed <-year_delayed$Statistics.Flights.Delayed

    #Summarizing by number of flights delayed each year
    year_delayed <- year %>% summarise(Statistics.Flights.Delayed = mean(Statistics.Flights.Delayed))
    delays_flights_year$Delayed <-year_delayed$Statistics.Flights.Delayed

    #Summarizing by number of flights diverted each year
    year_diverted <- year %>% summarise(Statistics.Flights.Diverted = mean(Statistics.Flights.Diverted))
    delays_flights_year$Diverted <-year_diverted$Statistics.Flights.Diverted

    #Summarizing by number of flights on time each year
    year_on_time <- year %>% summarise(Statistics.Flights.On.Time = mean(Statistics.Flights.On.Time))
    delays_flights_year$On_Time <-year_on_time$Statistics.Flights.On.Time

    #Creating a column to display percentage of flights that were on time each year, on average
    delays_flights_year$Percent_On_Time <-100*delays_flights_year$On_Time/(delays_flights_year$On_Time+delays_flights_year$Diverted+delays_flights_year$Delayed+delays_flights_year$Cancelled)

    #Display yearly averages for numbers of flights cancelled, delayed, diverted and on time
    round(delays_flights_year) 

    ## # A tibble: 14 x 6
    ##     Year Cancelled Delayed Diverted On_Time Percent_On_Time
    ##    <dbl>     <dbl>   <dbl>    <dbl>   <dbl>           <dbl>
    ##  1  2003       170    2027       24    9469              81
    ##  2  2004       224    2531       25    9705              78
    ##  3  2005       239    2660       26    9643              77
    ##  4  2006       226    2944       32    9551              75
    ##  5  2007       295    3246       33    9468              73
    ##  6  2008       252    2773       32    9321              75
    ##  7  2009       168    2263       28    9147              79
    ##  8  2010       216    2105       28    9292              80
    ##  9  2011       223    2056       27    8968              80
    ## 10  2012       154    1892       23    9298              82
    ## 11  2013       178    2313       27    9287              79
    ## 12  2014       235    2288       27    8439              77
    ## 13  2015       172    2034       29    8886              80
    ## 14  2016       303    1656       15    8323              81

    #Identifying year with the greatest percent of flights on time, on overage
    round(delays_flights_year[which.max(delays_flights_year$Percent_On_Time),])

    ## # A tibble: 1 x 6
    ##    Year Cancelled Delayed Diverted On_Time Percent_On_Time
    ##   <dbl>     <dbl>   <dbl>    <dbl>   <dbl>           <dbl>
    ## 1  2012       154    1892       23    9298              82

    #Identifying year with the least percent of flights on time, on overage
    round(delays_flights_year[which.min(delays_flights_year$Percent_On_Time),])

    ## # A tibble: 1 x 6
    ##    Year Cancelled Delayed Diverted On_Time Percent_On_Time
    ##   <dbl>     <dbl>   <dbl>    <dbl>   <dbl>           <dbl>
    ## 1  2007       295    3246       33    9468              73

On average, flights were on time each month the most in <b>2012</b> and
they were on time the least in <b>2007.</b>

# Delay Reason

## Average Number Flights Delayed per Month by Reason

The average percentage of flights delayed because of carrier, aircraft,
national aviation system, security and weather delays between 2003-2016.

    #Average number of flights per month since 2003 delayed because of carriers
    avg_flights_carriers <- sum(delays_reason$Statistics...of.Delays.Carrier)

    #Average number of flights per month since 2003 delayed because of late arriving aircraft
    avg_flights_aircraft <- sum(delays_reason$Statistics...of.Delays.Late.Aircraft)

    #Average number of flights per month since 2003 delayed because of national aviation system
    avg_flights_nas <- sum(delays_reason$Statistics...of.Delays.National.Aviation.System)

    #Average number of flights per month since 2003 delayed because of security delays
    avg_flights_security <- sum(delays_reason$Statistics...of.Delays.Security)

    #Average number of flights per month since 2003 delayed because of weather
    avg_flights_weather <- sum(delays_reason$Statistics...of.Delays.Weather)

    #Creating a Pie Chart  
    reason_values = c(avg_flights_carriers,avg_flights_aircraft,avg_flights_nas, avg_flights_security, avg_flights_weather)
    reason_labels = c("Carrier","Late Aircraft","National Aviation System","Security","Weather")

    #Calculating the percent each will be of the total
    piepercent<- round(100*reason_values/sum(reason_values), 1)

    # Plot the chart.
    pie(reason_values, labels = piepercent, main = "Reasons for Flight Delay between 2003-2016",col = rainbow(length(reason_values)))
    legend("topright", reason_labels, cex = 0.7,fill = rainbow(length(reason_values)))

![](airport_delays_files/figure-markdown_strict/unnamed-chunk-12-1.png)
The three biggest reasons for flight delays are

-   National Aviation System: <b>39.7%</b>
-   Late Aircraft: <b>32.8%</b>
-   Carrier: <b>23.9%</b>

## Delay Reason by Month of Year

    #Grouping by month
    month <- delays_reason %>% group_by(Time.Month)

    #Creating a data frame to store the summarized values of flight delayed because of carriers
    delays_reason_month <- month %>% summarise(Statistics...of.Delays.Carrier = mean(Statistics...of.Delays.Carrier))

    #Renaming the columns
    colnames(delays_reason_month)[which(names(delays_reason_month) == "Time.Month")] <- "Month"
    colnames(delays_reason_month)[which(names(delays_reason_month) == "Statistics...of.Delays.Carrier")] <- "Carrier"

    #Summarizing by flights delayed because of late aircraft
    month_aircraft <- month %>% summarise(Statistics...of.Delays.Late.Aircraft = mean(Statistics...of.Delays.Late.Aircraft))

    #Adding the column to delays_flights_year
    delays_reason_month$Aircraft <-month_aircraft$Statistics...of.Delays.Late.Aircraft

    #Summarizing by flights delayed because of national aviation system
    month_nas <- month %>% summarise(Statistics...of.Delays.National.Aviation.System = mean(Statistics...of.Delays.National.Aviation.System))
    delays_reason_month$National_Aviation_System<-month_nas$Statistics...of.Delays.National.Aviation.System

    #Summarizing by flights delayed because of security
    month_security <- month %>% summarise(Statistics...of.Delays.Security = mean(Statistics...of.Delays.Security))
    delays_reason_month$Security<-month_security$Statistics...of.Delays.Security

    #Summarizing by flights delayed because of weather
    month_weather <- month %>% summarise(Statistics...of.Delays.Weather = mean(Statistics...of.Delays.Weather))
    delays_reason_month$Weather<-month_weather$Statistics...of.Delays.Weather

    #Display yearly averages for numbers of flights cancelled, delayed, diverted and on time
    round(delays_reason_month) 

    ## # A tibble: 12 x 6
    ##    Month Carrier Aircraft National_Aviation_System Security Weather
    ##    <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>
    ##  1     1     585      767                      958        6      94
    ##  2     2     532      743                      940        5      83
    ##  3     3     602      842                      995        6      69
    ##  4     4     521      723                      898        5      58
    ##  5     5     540      761                      967        4      75
    ##  6     6     681      987                     1096        6     109
    ##  7     7     703     1011                     1050        6     107
    ##  8     8     633      870                      952        9      92
    ##  9     9     434      535                      750        4      51
    ## 10    10     484      644                      898        4      49
    ## 11    11     457      591                      837        4      49
    ## 12    12     716      987                     1111        9     100

    #Identifying month with the greatest number of delays due to each reasons for delay
    round(delays_reason_month[which.max(delays_reason_month$National_Aviation_System),])

    ## # A tibble: 1 x 6
    ##   Month Carrier Aircraft National_Aviation_System Security Weather
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>
    ## 1    12     716      987                     1111        9     100

    round(delays_reason_month[which.max(delays_reason_month$Aircraft),])

    ## # A tibble: 1 x 6
    ##   Month Carrier Aircraft National_Aviation_System Security Weather
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>
    ## 1     7     703     1011                     1050        6     107

    round(delays_reason_month[which.max(delays_reason_month$Carrier),])

    ## # A tibble: 1 x 6
    ##   Month Carrier Aircraft National_Aviation_System Security Weather
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>
    ## 1    12     716      987                     1111        9     100

    round(delays_reason_month[which.max(delays_reason_month$Weather),])

    ## # A tibble: 1 x 6
    ##   Month Carrier Aircraft National_Aviation_System Security Weather
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>
    ## 1     6     681      987                     1096        6     109

    round(delays_reason_month[which.max(delays_reason_month$Security),])

    ## # A tibble: 1 x 6
    ##   Month Carrier Aircraft National_Aviation_System Security Weather
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>
    ## 1    12     716      987                     1111        9     100

-   <b>December</b> has the most delays happen due to the National
    Aviation System, Carrier and Security.
-   <b>July</b> has the most delays due to Aircraft.
-   <b>June</b> has the most delays due to Weather.

## Delay Reason by Year

    #Grouping by year
    year <- delays_reason %>% group_by(Time.Year)

    #Creating a data frame to store the summarized values of flight delayed because of carriers
    delays_reason_year <- year %>% summarise(Statistics...of.Delays.Carrier = mean(Statistics...of.Delays.Carrier))

    #Renaming the columns
    colnames(delays_reason_year)[which(names(delays_reason_year) == "Time.Year")] <- "Year"
    colnames(delays_reason_year)[which(names(delays_reason_year) == "Statistics...of.Delays.Carrier")] <- "Carrier"

    #Summarizing by flights delayed because of late aircraft
    year_aircraft <- year %>% summarise(Statistics...of.Delays.Late.Aircraft = mean(Statistics...of.Delays.Late.Aircraft))

    #Adding the column to delays_flights_year
    delays_reason_year$Aircraft <-year_aircraft$Statistics...of.Delays.Late.Aircraft

    #Summarizing by flights delayed because of national aviation system
    year_nas <- year %>% summarise(Statistics...of.Delays.National.Aviation.System = mean(Statistics...of.Delays.National.Aviation.System))
    delays_reason_year$National_Aviation_System<-year_nas$Statistics...of.Delays.National.Aviation.System

    #Summarizing by flights delayed because of security
    year_security <- year %>% summarise(Statistics...of.Delays.Security = mean(Statistics...of.Delays.Security))
    delays_reason_year$Security<-year_security$Statistics...of.Delays.Security

    #Summarizing by flights delayed because of weather
    year_weather <- year %>% summarise(Statistics...of.Delays.Weather = mean(Statistics...of.Delays.Weather))
    delays_reason_year$Weather<-year_weather$Statistics...of.Delays.Weather

    #Display yearly averages for numbers of flights cancelled, delayed, diverted and on time
    round(delays_reason_year) 

    ## # A tibble: 14 x 6
    ##     Year Carrier Aircraft National_Aviation_System Security Weather
    ##    <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>
    ##  1  2003     429      514                     1000        7      76
    ##  2  2004     543      697                     1180        9     102
    ##  3  2005     628      775                     1155        6      95
    ##  4  2006     701      931                     1200       10     101
    ##  5  2007     785     1062                     1276        8     114
    ##  6  2008     624      881                     1173        5      90
    ##  7  2009     501      710                      976        4      72
    ##  8  2010     513      729                      797        5      62
    ##  9  2011     499      733                      764        4      56
    ## 10  2012     495      693                      647        4      53
    ## 11  2013     561      874                      810        4      64
    ## 12  2014     578      853                      789        3      66
    ## 13  2015     560      711                      692        3      67
    ## 14  2016     483      560                      558        3      52

    #Identifying year with the greatest number of delays due to each reasons for delay
    round(delays_reason_year[which.max(delays_reason_month$National_Aviation_System),])

    ## # A tibble: 1 x 6
    ##    Year Carrier Aircraft National_Aviation_System Security Weather
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>
    ## 1  2014     578      853                      789        3      66

    round(delays_reason_year[which.max(delays_reason_month$Aircraft),])

    ## # A tibble: 1 x 6
    ##    Year Carrier Aircraft National_Aviation_System Security Weather
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>
    ## 1  2009     501      710                      976        4      72

    round(delays_reason_year[which.max(delays_reason_month$Carrier),])

    ## # A tibble: 1 x 6
    ##    Year Carrier Aircraft National_Aviation_System Security Weather
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>
    ## 1  2014     578      853                      789        3      66

    round(delays_reason_year[which.max(delays_reason_month$Weather),])

    ## # A tibble: 1 x 6
    ##    Year Carrier Aircraft National_Aviation_System Security Weather
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>
    ## 1  2008     624      881                     1173        5      90

    round(delays_reason_year[which.max(delays_reason_month$Security),])

    ## # A tibble: 1 x 6
    ##    Year Carrier Aircraft National_Aviation_System Security Weather
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>
    ## 1  2014     578      853                      789        3      66

-   <b>2014</b> has the most delays happen due to the National Aviation
    System, Carrier and Security.
-   <b>2009</b> has the most delays due to Aircraft.
-   <b>2008</b> has the most delays due to Weather.

# Delay Duration

## Average Duration of Delay per Month by Reason

The average duration of delay because of carrier, aircraft, national
aviation system, security and weather delays between 2003-2016.

    #Average duration of delay per month since 2003 delayed because of carriers
    avg_flights_carriers <- mean(delays_duration$Statistics.Minutes.Delayed.Carrier)

    #Average duration of delay per month since 2003 delayed because of late arriving aircraft
    avg_flights_aircraft <- mean(delays_duration$Statistics.Minutes.Delayed.Late.Aircraft)

    #Average duration of delay per month since 2003 delayed because of national aviation system
    avg_flights_nas <- mean(delays_duration$Statistics.Minutes.Delayed.National.Aviation.System)

    #Average duration of delay per month since 2003 delayed because of security delays
    avg_flights_security <- mean(delays_duration$Statistics.Minutes.Delayed.Security)

    #Average duration of delay per month since 2003 delayed because of weather
    avg_flights_weather <- mean(delays_duration$Statistics.Minutes.Delayed.Weather)

    #Creating a Bar Plot with values displayed on top of bars
    duration_values = c(avg_flights_carriers,avg_flights_aircraft,avg_flights_nas, avg_flights_security, avg_flights_weather)
    duration_values = round(duration_values)
    duration_labels = c("Carrier","Late Aircraft","National Aviation System","Security","Weather")

    ## Make the duration values numbers (rather than factors)
    duration_values <- as.numeric(as.character(duration_values))

    ## Find a range of y's that will leave sufficient space above the tallest bar
    ylim <- c(0, 1.1*max(duration_values))

    ## Plot, and store x-coordinates of bars in xx
    xx <- barplot(duration_values,main ="Average Duration of Delay per Month by Reason", col=rainbow(length(duration_values)), ylim = ylim)

    ## Add text at top of bars
    text(x = xx, y = duration_values, label = duration_values, pos = 3, cex = 0.8, col = "red")

    ## Add x-axis labels 
    axis(1, at=xx, labels=duration_labels, tick=FALSE, las=2, line=-0.5, cex.axis=0.5)

![](airport_delays_files/figure-markdown_strict/unnamed-chunk-17-1.png)
The longest delays were from three main sources:

-   Late Aircraft resulted in the longest delays, averaging a total of
    49,410 minutes each month.
-   National Aviation System resulted in delays averaging a total of
    45,077 minutes each month.
-   Carriers resulted in delays averaging a total of 35,021 minutes each
    month.

## Delay Duration by Month of Year

    #Grouping by month
    month <- delays_duration %>% group_by(Time.Month)

    #Creating a data frame to store the summarized values of flight delayed because of carriers
    delays_duration_month <- month %>% summarise(Statistics.Minutes.Delayed.Carrier = mean(Statistics.Minutes.Delayed.Carrier))

    #Renaming the columns
    colnames(delays_duration_month)[which(names(delays_duration_month) == "Time.Month")] <- "Month"
    colnames(delays_duration_month)[which(names(delays_duration_month) == "Statistics.Minutes.Delayed.Carrier")] <- "Carrier"

    #Summarizing by flights delayed because of late aircraft
    month_aircraft <- month %>% summarise(Statistics.Minutes.Delayed.Late.Aircraft = mean(Statistics.Minutes.Delayed.Late.Aircraft))

    #Adding the column to delays_flights_year
    delays_duration_month$Aircraft <-month_aircraft$Statistics.Minutes.Delayed.Late.Aircraft

    #Summarizing by flights delayed because of national aviation system
    month_nas <- month %>% summarise(Statistics.Minutes.Delayed.National.Aviation.System=mean(Statistics.Minutes.Delayed.National.Aviation.System))
    delays_duration_month$National_Aviation_System<-month_nas$Statistics.Minutes.Delayed.National.Aviation.System

    #Summarizing by flights delayed because of security
    month_security <- month %>% summarise(Statistics.Minutes.Delayed.Security = mean(Statistics.Minutes.Delayed.Security))
    delays_duration_month$Security<-month_security$Statistics.Minutes.Delayed.Security

    #Summarizing by flights delayed because of weather
    month_weather <- month %>% summarise(Statistics.Minutes.Delayed.Weather = mean(Statistics.Minutes.Delayed.Weather))
    delays_duration_month$Weather<-month_weather$Statistics.Minutes.Delayed.Weather

    #Summarizing by total delay
    month_total <- month %>% summarise(Statistics.Minutes.Delayed.Total = mean(Statistics.Minutes.Delayed.Total))
    delays_duration_month$Total<-month_total$Statistics.Minutes.Delayed.Total

    #Display yearly averages for numbers of flights cancelled, delayed, diverted and on time
    round(delays_duration_month) 

    ## # A tibble: 12 x 7
    ##    Month Carrier Aircraft National_Aviation_System Security Weather  Total
    ##    <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>  <dbl>
    ##  1     1   35825    48043                    43494      228    7519 135109
    ##  2     2   32396    45667                    42320      180    6849 127412
    ##  3     3   36008    52064                    46296      201    5568 140138
    ##  4     4   31593    43923                    41179      180    4559 121434
    ##  5     5   32885    47559                    46354      154    6160 133112
    ##  6     6   43110    66186                    56875      236    9208 175614
    ##  7     7   44547    67893                    55365      211    8691 176707
    ##  8     8   39115    55387                    46652      338    7089 148580
    ##  9     9   26455    31320                    33340      158    3690  94962
    ## 10    10   28391    36938                    39162      158    3752 108400
    ## 11    11   26853    34542                    37044      188    3735 102362
    ## 12    12   42523    62753                    52525      299    8354 166455

    #Identifying month with the greatest duration of delays due to each reason
    round(delays_duration_month[which.max(delays_duration_month$Total),])

    ## # A tibble: 1 x 7
    ##   Month Carrier Aircraft National_Aviation_System Security Weather  Total
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>  <dbl>
    ## 1     7   44547    67893                    55365      211    8691 176707

    round(delays_duration_month[which.max(delays_duration_month$National_Aviation_System),])

    ## # A tibble: 1 x 7
    ##   Month Carrier Aircraft National_Aviation_System Security Weather  Total
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>  <dbl>
    ## 1     6   43110    66186                    56875      236    9208 175614

    round(delays_duration_month[which.max(delays_duration_month$Aircraft),])

    ## # A tibble: 1 x 7
    ##   Month Carrier Aircraft National_Aviation_System Security Weather  Total
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>  <dbl>
    ## 1     7   44547    67893                    55365      211    8691 176707

    round(delays_duration_month[which.max(delays_duration_month$Carrier),])

    ## # A tibble: 1 x 7
    ##   Month Carrier Aircraft National_Aviation_System Security Weather  Total
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>  <dbl>
    ## 1     7   44547    67893                    55365      211    8691 176707

    round(delays_duration_month[which.max(delays_duration_month$Weather),])

    ## # A tibble: 1 x 7
    ##   Month Carrier Aircraft National_Aviation_System Security Weather  Total
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>  <dbl>
    ## 1     6   43110    66186                    56875      236    9208 175614

    round(delays_duration_month[which.max(delays_duration_month$Security),])

    ## # A tibble: 1 x 7
    ##   Month Carrier Aircraft National_Aviation_System Security Weather  Total
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>  <dbl>
    ## 1     8   39115    55387                    46652      338    7089 148580

Overall, <b>July</b> has the longest delays.

-   <b>June</b> has the longest delays due to the National Aviation
    System and Weather.
-   <b>July</b> has the longest delays due to Aircraft and Carrier.
-   <b>August</b> has the longest delays due to Security.

## Delay Duration by Year

    #Grouping by year
    year <- delays_duration %>% group_by(Time.Year)

    #Creating a data frame to store the summarized values of flight delayed because of carriers
    delays_duration_year <- year %>% summarise(Statistics.Minutes.Delayed.Carrier = mean(Statistics.Minutes.Delayed.Carrier))

    #Renaming the columns
    colnames(delays_duration_year)[which(names(delays_duration_year) == "Time.Year")] <- "Year"
    colnames(delays_duration_year)[which(names(delays_duration_year) == "Statistics.Minutes.Delayed.Carrier")] <- "Carrier"

    #Summarizing by flights delayed because of late aircraft
    year_aircraft <- year%>% summarise(Statistics.Minutes.Delayed.Late.Aircraft = mean(Statistics.Minutes.Delayed.Late.Aircraft))
    delays_duration_year$Aircraft <-year_aircraft$Statistics.Minutes.Delayed.Late.Aircraft

    #Summarizing by flights delayed because of national aviation system
    year_nas <- year %>% summarise(Statistics.Minutes.Delayed.National.Aviation.System=mean(Statistics.Minutes.Delayed.National.Aviation.System))
    delays_duration_year$National_Aviation_System<-year_nas$Statistics.Minutes.Delayed.National.Aviation.System

    #Summarizing by flights delayed because of security
    year_security <- year %>% summarise(Statistics.Minutes.Delayed.Security = mean(Statistics.Minutes.Delayed.Security))
    delays_duration_year$Security<-year_security$Statistics.Minutes.Delayed.Security

    #Summarizing by flights delayed because of weather
    year_weather <- year %>% summarise(Statistics.Minutes.Delayed.Weather = mean(Statistics.Minutes.Delayed.Weather))
    delays_duration_year$Weather<-year_weather$Statistics.Minutes.Delayed.Weather

    #Summarizing by total delay
    year_total <- year %>% summarise(Statistics.Minutes.Delayed.Total = mean(Statistics.Minutes.Delayed.Total))
    delays_duration_year$Total<-year_total$Statistics.Minutes.Delayed.Total

    #Display yearly averages for numbers of flights cancelled, delayed, diverted and on time
    round(delays_duration_year) 

    ## # A tibble: 14 x 7
    ##     Year Carrier Aircraft National_Aviation_System Security Weather  Total
    ##    <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>  <dbl>
    ##  1  2003   24198    29963                    44153      263    5786 104362
    ##  2  2004   30136    41868                    54051      346    7533 133934
    ##  3  2005   34897    47239                    54387      230    7097 143851
    ##  4  2006   39688    57667                    58372      383    7676 163786
    ##  5  2007   46285    67367                    63368      305    9292 186617
    ##  6  2008   39092    56628                    59102      196    7620 162638
    ##  7  2009   30864    43480                    46178      139    5792 126452
    ##  8  2010   31248    44006                    36484      182    4921 116842
    ##  9  2011   31484    45919                    34854      143    4701 117101
    ## 10  2012   32049    43990                    28883      135    4305 109362
    ## 11  2013   36354    55300                    38217      197    5272 135339
    ## 12  2014   37021    54090                    36680      115    5695 133601
    ## 13  2015   37524    47770                    32628      147    5842 123913
    ## 14  2016   34136    36748                    24176      132    4652  99845

    #Identifying year with the greatest duration of delays due to each reason
    round(delays_duration_year[which.max(delays_duration_year$Total),])

    ## # A tibble: 1 x 7
    ##    Year Carrier Aircraft National_Aviation_System Security Weather  Total
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>  <dbl>
    ## 1  2007   46285    67367                    63368      305    9292 186617

    round(delays_duration_year[which.max(delays_duration_year$National_Aviation_System),])

    ## # A tibble: 1 x 7
    ##    Year Carrier Aircraft National_Aviation_System Security Weather  Total
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>  <dbl>
    ## 1  2007   46285    67367                    63368      305    9292 186617

    round(delays_duration_year[which.max(delays_duration_year$Aircraft),])

    ## # A tibble: 1 x 7
    ##    Year Carrier Aircraft National_Aviation_System Security Weather  Total
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>  <dbl>
    ## 1  2007   46285    67367                    63368      305    9292 186617

    round(delays_duration_year[which.max(delays_duration_year$Carrier),])

    ## # A tibble: 1 x 7
    ##    Year Carrier Aircraft National_Aviation_System Security Weather  Total
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>  <dbl>
    ## 1  2007   46285    67367                    63368      305    9292 186617

    round(delays_duration_year[which.max(delays_duration_year$Weather),])

    ## # A tibble: 1 x 7
    ##    Year Carrier Aircraft National_Aviation_System Security Weather  Total
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>  <dbl>
    ## 1  2007   46285    67367                    63368      305    9292 186617

    round(delays_duration_year[which.max(delays_duration_year$Security),])

    ## # A tibble: 1 x 7
    ##    Year Carrier Aircraft National_Aviation_System Security Weather  Total
    ##   <dbl>   <dbl>    <dbl>                    <dbl>    <dbl>   <dbl>  <dbl>
    ## 1  2006   39688    57667                    58372      383    7676 163786

Overall, <b>2007</b> has the longest delays.

-   <b>2007</b> has the longest delays due to the National Aviation
    System, Aircraft, Carrier and Weather.
-   <b>2006</b> has the longest delays due to Security.

# Summary of Data Analysis

On average, <b>77.8%</b> of flights were On Time each month and
<b>20.2%</b> of flights were Delayed.

The three biggest reasons for flight delays are:

-   National Aviation System accounts for <b>39.7%</b> of all delays,
    averaging a total of 45,077 minutes each month.
-   Late Aircraft accounts for <b>32.8%</b> of all delays, averaging a
    total of 49,410 minutes each month, which is the <b>longest</b>
    delay.
-   Carrier accounts for <b>23.9%</b> of all delays, averaging a total
    of 35,021 minutes each month.

The most delays occur in the month of <b>December</b>, which can be
accounted towards the National Aviation System, Carrier and Security.

The longest delays occur in the month of <b>July</b>, which can be
accounted towards the Aircraft and Carrier.

The most delays occur in the year <b>2007.</b>

-   These delays can be accounted towards the National Aviation System,
    Aircraft, Carrier and Weather.
-   This is also the year with the longest delays overall.

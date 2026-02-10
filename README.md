# Summary of Data Analysis

## Dataset

The data was downloaded from CORGIS Dataset Project: [Original Dataset](https://think.cs.vt.edu/corgis/csv/airlines/)

This dataset is all about flights in the United States, including information about the number, length, and type of delays between 2003 and 2016. The data is reported for individual months at every major airport for every carrier. Additional information is available: http://www.rita.dot.gov/bts/help/aviation/html/understanding.html

### Attributes

- Airport.Code: The 3 letter code for this airport, assigned by IATA. 
- Airport.Name:	The full name of this airport.
- Time.Label: The "year/month" reported as a string, to make it easier to sort by time periods.	
- Time.Month: The reported month as a number. 0 is January, 1 is February, etc.	
- Time.Month Name: Name of Month
- Time.Year: The reported year as a 4-digit number.	
- Statistics.# of Delays.Carrier: The number of delays and cancellations due to circumstances within the airline's control (e.g. maintenance or crew problems, aircraft cleaning, baggage loading, fueling, etc.) in this month.	
- Statistics.# of Delays.Late Aircraft: The number of delays and cancellations caused by a previous flight with the same aircraft arriving late, causing the present flight to depart late in this month.	
- Statistics.# of Delays.National Aviation System	Integer	The number of delays and cancellations attributable to the national aviation system that refer to a broad set of conditions, such as non-extreme weather conditions, airport operations, heavy traffic volume, and air traffic control in this month.
- Statistics.# of Delays.Security	Integer	Number of delays or cancellations caused by evacuation of a terminal or concourse, re-boarding of aircraft because of security breach, inoperative screening equipment and/or long lines in excess of 29 minutes at screening areas in this month.	17
- Statistics.# of Delays.Weather	Integer	Number of delays or cancellations caused by significant meteorological conditions (actual or forecasted) that, in the judgment of the carrier, delays or prevents the operation of a flight such as tornado, blizzard or hurricane in this month.	328
- Statistics.Carriers.Names: The full names of the carriers that reported in.	
- Statistics.Carriers.Total	Integer	The number of carriers that reported flight information during this time period and at this location.	11
- Statistics.Flights.Cancelled:	The number of flights that were cancelled in this month.	
- Statistics.Flights.Delayed:	The number of flights that were delayed in this month.
- Statistics.Flights.Diverted:	The number of flights that were diverted in this month.	
- Statistics.Flights.On Time:	The number of flights that were on time in this month.	
- Statistics.Flights.Total: The total number of flights in this month.	
- Statistics.Minutes Delayed.Carrier: The number of minutes delayed due to circumstances within the airline's control (e.g. maintenance or crew problems, aircraft cleaning, baggage loading, fueling, etc.) in this month.
- Statistics.Minutes Delayed.Late Aircraft	Integer	The number of minutes delayed caused by a previous flight with the same aircraft arriving late, causing the present flight to depart late in this month.
Statistics.Minutes Delayed.National Aviation System: The number of minutes delayed attributable to the national aviation system that refer to a broad set of conditions, such as non-extreme weather conditions, airport operations, heavy traffic volume, and air traffic control in this month.
- Statistics.Minutes Delayed.Security: Number of minutes delayed caused by evacuation of a terminal or concourse, re-boarding of aircraft because of security breach, inoperative screening equipment and/or long lines in excess of 29 minutes at screening areas in this month.
- Statistics.Minutes Delayed.Total
- Statistics.Minutes Delayed.Weather:	Number of of minutes delayed caused by significant meteorological conditions (actual or forecasted) that, in the judgment of the carrier, delays or prevents the operation of a flight such as tornado, blizzard or hurricane in this month.

#### See this analysis in Kaggle: 
https://www.kaggle.com/priankravichandar/airport-delays-data-analysis

### Tools

R

## Insights

On average, **77.8%** of flights were On Time each month and **20.2%** of flights were Delayed.

The three biggest reasons for flight delays are:

- National Aviation System accounts for **39.7%** of all delays, averaging a total of 45,077 minutes each month.
- Late Aircraft accounts for **32.8%** of all delays, averaging a total of 49,410 minutes each month, which is the **longest** delay.
- Carrier accounts for **23.9%** of all delays, averaging a total of 35,021 minutes each month.
- The most delays occur in **December**, which can be accounted for by the National Aviation System, Carrier, and Security.
- The longest delays occur in **July**, which can be accounted for by the Aircraft and Carrier.
- The most delays occur in the year **2007.**
    - These delays can be accounted for by the National Aviation System, Aircraft, Carrier, and Weather.
    - This is also the year with the longest delays overall.


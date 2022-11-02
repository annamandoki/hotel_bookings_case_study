Hotel Bookings Case Study
================
Anna Mándoki
2022-11-02

## 1. Introduction

This case study was inspired by a series of exercises related to the
‘hotel_bookings’ dataset I worked through while I was doing the Google
Data Analytics Professional Certificate course. The dataset contains
booking information for a city hotel and a resort hotel.

My goal with this project is to dive deeper into the data.

I am assuming the role of a junior data analyst working on the marketing
analytics team at an imaginary hotel booking company.

I am going to perform different data cleaning tasks and conduct
exploratory data analysis (EDA) on the dataset.

## 2. Ask Phase

### 2.1 Business Objective

Identify trends in hotel bookings to help shape the future marketing
strategy of the company.

The following stakeholder goals and assumptions will guide the analysis:

- Goal: Marketing campaign to target people who book early. Assumption:
  People with children have to book in advance.
- Goal: increase weekend bookings, an important source of revenue for
  the hotel. What group of guests book the most weekend nights?
  Assumption: Guests without children book the most weekend nights.
- Goal: Develop promotions based on different booking distributions. How
  many of the transactions are occurring for each different distribution
  type?
- Is the number of bookings for each distribution type different
  depending on whether or not there was a deposit or what market segment
  they represent?
- Goal: Promotion to families that make online bookings for city hotels.
  The online segment is the fastest growing segment, and families tend
  to spend more at city hotels than other types of guests. Your
  stakeholder asks if you can create a plot that shows the relationship
  between lead time and guests traveling with children for online
  bookings at city hotels. This will give her a better idea of the
  specific timing for the promotion.
- Prevent cancellations. What types of bookings are likely to get
  cancelled?

Descriptive analytics can be employed to further understand patterns,
trends, and anomalies in data; Used to perform research in different
problems like: bookings cancellation prediction, customer segmentation,
customer satiation, seasonality, among others;

Questions: What is the month with the most guest arrivals? How long do
guests tend to stay at the hotel? How many reservations were made by
repeated guests? What is the Average Daily Rate (ADR) throughout the
year? How many reservations were cancelled out of total? What is the
most frequent deposit type for cancelled reservations? Which countries
do customers come from? What types of customers are most common in each
hotel? What is their preferred meal plan? Which hotel is preferred by
adults with children? What is the strongest market segment and
distribution channel?

### 2.2 Stakeholders

In a similar real-life scenario stakeholders would include:

- Head of Marketing: a person responsible for the development of
  marketing campaigns
- Marketing Analytics Team: a team responsible for collecting, analyzing
  and reporting data that helps guide the company’s marketing strategy
- Executive Team: company executives who make the final decision on the
  recommended marketing strategy

## 3. Prepare Phase

### 3.1 About the dataset

The dataset consists of one csv file: ‘hotel_bookings.csv’

It contains information on bookings due to arrive between the 1st of
July of 2015 and the 31st of August 2017, including bookings that
effectively arrived and bookings that were canceled.

The file contains 32 columns with information such as when the booking
was made, length of stay, the number of adults, children, and/or babies,
and the number of available parking spaces, among other things.

### 3.2 Dataset location & licence

The dataset was made available on Kaggle: [Hotel booking
demand](https://www.kaggle.com/datasets/jessemostipak/hotel-booking-demand)
by Jesse Mostipak.

The data is originally from the article [Hotel Booking Demand
Datasets](https://www.sciencedirect.com/science/article/pii/S2352340918315191),
written by Nuno Antonio, Ana Almeida, and Luis Nunes for Data in Brief,
Volume 22, February 2019.

The data was downloaded and cleaned by Thomas Mock and Antoine Bichat
for [\#TidyTuesday during the week of February 11th,
2020](https://github.com/rfordatascience/tidytuesday/blob/master/data/2020/2020-02-11/readme.md)

The data was released under this
[licence](https://creativecommons.org/licenses/by/4.0/)

Since this is real hotel data, all data elements pertaining hotel or
costumer identification were deleted.

### 3.3 Data dictionary

Detailed description of the variables used in the dataset:

- hotel: type of hotel - Resort hotel or City Hotel
- is_canceled: value indicating if the booking was canceled (1) or not
  (0)
- lead_time: number of days that elapsed between the entering date of
  the booking into the PMS and the arrival date
- arrival_date_year: year of arrival date
- arrival_date_month: month of arrival date
- arrival_date_week_number: week number for arrival date
- arrival_date_day_of_month: day of the month of the arrival date
- stays_in_weekend_nights: number of weekend nights (Saturday or Sunday)
  the guest stayed or booked to stay at the hotel
- stays_in_week_nights: number of week nights (Monday to Friday) the
  guest stayed or booked to stay at the hotel
- adults: number of adults in the booking
- children: number of children
- babies: number of babies
- meal: type of meal booked. Categories are presented in standard
  hospitality meal packages:
  - Undefined/SC – no meal package
  - BB – Bed & Breakfast
  - HB – Half board (breakfast and one other meal – usually dinner)
  - FB – Full board (breakfast, lunch and dinner)
- country: country of origin. Categories are represented in the [ISO
  3166–3:2013 format](https://www.iso.org/obp/ui/#search)
- market_segment: market segment designation
  - TA = Travel Agents
  - TO = Tour Operators
- distribution_channel: booking distribution channel
  - TA = Travel Agents
  - TO = Tour Operators
- is_repeated_guest: value indicating if the booking name was from a
  repeated guest (1) or not (0)
- previous_cancellations: number of previous bookings that were
  cancelled by the customer prior to the current booking
- previous_bookings_not_canceled: number of previous bookings not
  cancelled by the customer prior to the current booking
- reserved_room_type: code of room type reserved. Code is presented
  instead of designation for anonymity reasons.
- assigned_room_type: code for the type of room assigned to the booking.
  Sometimes the assigned room type differs from the reserved room type
  due to hotel operation reasons (e.g. overbooking) or by customer
  request. Code is presented instead of designation for anonymity
  reasons.
- booking_changes: number of changes/amendments made to the booking from
  the moment the booking was entered on the PMS until the moment of
  check-in or cancellation
- deposit_type: indication on if the customer made a deposit to
  guarantee the booking. Three categories;
  - No Deposit – no deposit was made
  - Non Refund – a deposit was made in the value of the total stay cost
  - Refundable – a deposit was made with a value under the total cost of
    stay.
- agent: ID of the travel agency that made the booking
- company: ID of the company/entity that made the booking or responsible
  for paying the booking. ID is presented instead of designation for
  anonymity reasons
- days_in_waiting_list: number of days the booking was in the waiting
  list before it was confirmed to the customer
- customer_type: type of booking, assuming one of four categories:
  - Contract - when the booking has an allotment or other type of
    contract associated to it
  - Group – when the booking is associated to a group
  - Transient – when the booking is not part of a group or contract, and
    is not associated to other transient (temporary) booking
  - Transient-party – when the booking is transient (temporary), but is
    associated to at least other transient booking
- adr: Average Daily Rate as defined by dividing the sum of all lodging
  transactions by the total number of staying nights
- required_car_parking_spaces: number of car parking spaces required by
  the customer
- total_of_special_requests: Number of special requests made by the
  customer (e.g. twin bed or high floor)
- reservation_status: Reservation last status, assuming one of three
  categories:
  - Canceled – booking was canceled by the customer
  - Check-Out – customer has checked in but already departed
  - No-Show – customer did not check-in and did inform the hotel of the
    reason why
- reservation_status_date: date at which the last status was set. This
  variable can be used in conjunction with the ‘ReservationStatus’ to
  understand when was the booking canceled or when did the customer
  checked-out of the hotel

### 3.4 Credibility, bias and privacy

- Reliable: The data is reliable and fit for use as it is real hotel
  booking data.
- Original: The data originates from real hotels, however pre-processing
  has been made, two datasets were merged into one.
- Comprehensive: The is comprehensive, contains all critical
  information.
- Current: The data is not current, it is 7 years old as of November
  2022.
- Cited: The data is cited, the name of the authors of the original
  article is mentioned.

Data privacy is ensured: all personally identifying information has been
removed from the data.

### 3.5 Is the data helpful in answering the question in the business task?

The dataset contains all critical information to identify patterns in
bookings.

### 3.6 Key steps taken in the Prepare Phase

- Downloaded and stored data on computer
- Identified how the data is organized
- Explored data dictionary
- Took a first look at the data using LibreOffice Calc
- Determined credibility of the data

## 4. Process Phase

### 4.1 Tools

After taking a first look at the data in LibreOffice Calc, I switched to
RStudio Desktop.

### 4.2 Setting up my environment

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
    ## ✔ ggplot2 3.3.6      ✔ purrr   0.3.4 
    ## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
    ## ✔ tidyr   1.2.1      ✔ stringr 1.4.1 
    ## ✔ readr   2.1.2      ✔ forcats 0.5.2 
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
library(janitor)
```

    ## 
    ## Attaching package: 'janitor'
    ## 
    ## The following objects are masked from 'package:stats':
    ## 
    ##     chisq.test, fisher.test

``` r
library(skimr)
library(lubridate)
```

    ## 
    ## Attaching package: 'lubridate'
    ## 
    ## The following objects are masked from 'package:base':
    ## 
    ##     date, intersect, setdiff, union

### 4.3 Data importing

``` r
hotel_bookings <- read.csv("hotel_bookings.csv")
```

### 4.4 Viewing the data frame

``` r
glimpse(hotel_bookings)
```

    ## Rows: 119,390
    ## Columns: 32
    ## $ hotel                          <chr> "Resort Hotel", "Resort Hotel", "Resort…
    ## $ is_canceled                    <int> 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, …
    ## $ lead_time                      <int> 342, 737, 7, 13, 14, 14, 0, 9, 85, 75, …
    ## $ arrival_date_year              <int> 2015, 2015, 2015, 2015, 2015, 2015, 201…
    ## $ arrival_date_month             <chr> "July", "July", "July", "July", "July",…
    ## $ arrival_date_week_number       <int> 27, 27, 27, 27, 27, 27, 27, 27, 27, 27,…
    ## $ arrival_date_day_of_month      <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ stays_in_weekend_nights        <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ stays_in_week_nights           <int> 0, 0, 1, 1, 2, 2, 2, 2, 3, 3, 4, 4, 4, …
    ## $ adults                         <int> 2, 2, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ children                       <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ babies                         <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ meal                           <chr> "BB", "BB", "BB", "BB", "BB", "BB", "BB…
    ## $ country                        <chr> "PRT", "PRT", "GBR", "GBR", "GBR", "GBR…
    ## $ market_segment                 <chr> "Direct", "Direct", "Direct", "Corporat…
    ## $ distribution_channel           <chr> "Direct", "Direct", "Direct", "Corporat…
    ## $ is_repeated_guest              <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ previous_cancellations         <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ previous_bookings_not_canceled <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ reserved_room_type             <chr> "C", "C", "A", "A", "A", "A", "C", "C",…
    ## $ assigned_room_type             <chr> "C", "C", "C", "A", "A", "A", "C", "C",…
    ## $ booking_changes                <int> 3, 4, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ deposit_type                   <chr> "No Deposit", "No Deposit", "No Deposit…
    ## $ agent                          <chr> "NULL", "NULL", "NULL", "304", "240", "…
    ## $ company                        <chr> "NULL", "NULL", "NULL", "NULL", "NULL",…
    ## $ days_in_waiting_list           <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ customer_type                  <chr> "Transient", "Transient", "Transient", …
    ## $ adr                            <dbl> 0.00, 0.00, 75.00, 75.00, 98.00, 98.00,…
    ## $ required_car_parking_spaces    <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ total_of_special_requests      <int> 0, 0, 0, 0, 1, 1, 0, 1, 1, 0, 0, 0, 3, …
    ## $ reservation_status             <chr> "Check-Out", "Check-Out", "Check-Out", …
    ## $ reservation_status_date        <chr> "2015-07-01", "2015-07-01", "2015-07-02…

``` r
head(hotel_bookings)
```

    ##          hotel is_canceled lead_time arrival_date_year arrival_date_month
    ## 1 Resort Hotel           0       342              2015               July
    ## 2 Resort Hotel           0       737              2015               July
    ## 3 Resort Hotel           0         7              2015               July
    ## 4 Resort Hotel           0        13              2015               July
    ## 5 Resort Hotel           0        14              2015               July
    ## 6 Resort Hotel           0        14              2015               July
    ##   arrival_date_week_number arrival_date_day_of_month stays_in_weekend_nights
    ## 1                       27                         1                       0
    ## 2                       27                         1                       0
    ## 3                       27                         1                       0
    ## 4                       27                         1                       0
    ## 5                       27                         1                       0
    ## 6                       27                         1                       0
    ##   stays_in_week_nights adults children babies meal country market_segment
    ## 1                    0      2        0      0   BB     PRT         Direct
    ## 2                    0      2        0      0   BB     PRT         Direct
    ## 3                    1      1        0      0   BB     GBR         Direct
    ## 4                    1      1        0      0   BB     GBR      Corporate
    ## 5                    2      2        0      0   BB     GBR      Online TA
    ## 6                    2      2        0      0   BB     GBR      Online TA
    ##   distribution_channel is_repeated_guest previous_cancellations
    ## 1               Direct                 0                      0
    ## 2               Direct                 0                      0
    ## 3               Direct                 0                      0
    ## 4            Corporate                 0                      0
    ## 5                TA/TO                 0                      0
    ## 6                TA/TO                 0                      0
    ##   previous_bookings_not_canceled reserved_room_type assigned_room_type
    ## 1                              0                  C                  C
    ## 2                              0                  C                  C
    ## 3                              0                  A                  C
    ## 4                              0                  A                  A
    ## 5                              0                  A                  A
    ## 6                              0                  A                  A
    ##   booking_changes deposit_type agent company days_in_waiting_list customer_type
    ## 1               3   No Deposit  NULL    NULL                    0     Transient
    ## 2               4   No Deposit  NULL    NULL                    0     Transient
    ## 3               0   No Deposit  NULL    NULL                    0     Transient
    ## 4               0   No Deposit   304    NULL                    0     Transient
    ## 5               0   No Deposit   240    NULL                    0     Transient
    ## 6               0   No Deposit   240    NULL                    0     Transient
    ##   adr required_car_parking_spaces total_of_special_requests reservation_status
    ## 1   0                           0                         0          Check-Out
    ## 2   0                           0                         0          Check-Out
    ## 3  75                           0                         0          Check-Out
    ## 4  75                           0                         0          Check-Out
    ## 5  98                           0                         1          Check-Out
    ## 6  98                           0                         1          Check-Out
    ##   reservation_status_date
    ## 1              2015-07-01
    ## 2              2015-07-01
    ## 3              2015-07-02
    ## 4              2015-07-02
    ## 5              2015-07-03
    ## 6              2015-07-03

### 4.5 Data cleaning & transformation

As I start cleaning and transforming the dataset, I create a new data
frame to represent the changes: **‘hotel_bookings_v2’** I can always
refer back to the original data frame if needed.

#### 4.5.1 Check duplicated values if any

Count duplicates with `sum()` and `duplicated()`.

``` r
sum(duplicated(hotel_bookings))
```

    ## [1] 31994

#### 4.5.2 Remove duplicates

Remove duplicates using the `distinct()` function.

``` r
hotel_bookings_v2 <- hotel_bookings %>%
  distinct()

glimpse(hotel_bookings_v2)
```

    ## Rows: 87,396
    ## Columns: 32
    ## $ hotel                          <chr> "Resort Hotel", "Resort Hotel", "Resort…
    ## $ is_canceled                    <int> 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, …
    ## $ lead_time                      <int> 342, 737, 7, 13, 14, 0, 9, 85, 75, 23, …
    ## $ arrival_date_year              <int> 2015, 2015, 2015, 2015, 2015, 2015, 201…
    ## $ arrival_date_month             <chr> "July", "July", "July", "July", "July",…
    ## $ arrival_date_week_number       <int> 27, 27, 27, 27, 27, 27, 27, 27, 27, 27,…
    ## $ arrival_date_day_of_month      <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ stays_in_weekend_nights        <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ stays_in_week_nights           <int> 0, 0, 1, 1, 2, 2, 2, 3, 3, 4, 4, 4, 4, …
    ## $ adults                         <int> 2, 2, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ children                       <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, …
    ## $ babies                         <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ meal                           <chr> "BB", "BB", "BB", "BB", "BB", "BB", "FB…
    ## $ country                        <chr> "PRT", "PRT", "GBR", "GBR", "GBR", "PRT…
    ## $ market_segment                 <chr> "Direct", "Direct", "Direct", "Corporat…
    ## $ distribution_channel           <chr> "Direct", "Direct", "Direct", "Corporat…
    ## $ is_repeated_guest              <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ previous_cancellations         <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ previous_bookings_not_canceled <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ reserved_room_type             <chr> "C", "C", "A", "A", "A", "C", "C", "A",…
    ## $ assigned_room_type             <chr> "C", "C", "C", "A", "A", "C", "C", "A",…
    ## $ booking_changes                <int> 3, 4, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, …
    ## $ deposit_type                   <chr> "No Deposit", "No Deposit", "No Deposit…
    ## $ agent                          <chr> "NULL", "NULL", "NULL", "304", "240", "…
    ## $ company                        <chr> "NULL", "NULL", "NULL", "NULL", "NULL",…
    ## $ days_in_waiting_list           <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ customer_type                  <chr> "Transient", "Transient", "Transient", …
    ## $ adr                            <dbl> 0.00, 0.00, 75.00, 75.00, 98.00, 107.00…
    ## $ required_car_parking_spaces    <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ total_of_special_requests      <int> 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 0, 3, 1, …
    ## $ reservation_status             <chr> "Check-Out", "Check-Out", "Check-Out", …
    ## $ reservation_status_date        <chr> "2015-07-01", "2015-07-01", "2015-07-02…

#### 4.5.3 Check NA values

Count NA values using the `is.na()` function.

``` r
sum(is.na(hotel_bookings_v2))
```

    ## [1] 4

Find out in which column(s) the NA values are using `map()`

``` r
map(hotel_bookings_v2, ~sum(is.na(.)))
```

    ## $hotel
    ## [1] 0
    ## 
    ## $is_canceled
    ## [1] 0
    ## 
    ## $lead_time
    ## [1] 0
    ## 
    ## $arrival_date_year
    ## [1] 0
    ## 
    ## $arrival_date_month
    ## [1] 0
    ## 
    ## $arrival_date_week_number
    ## [1] 0
    ## 
    ## $arrival_date_day_of_month
    ## [1] 0
    ## 
    ## $stays_in_weekend_nights
    ## [1] 0
    ## 
    ## $stays_in_week_nights
    ## [1] 0
    ## 
    ## $adults
    ## [1] 0
    ## 
    ## $children
    ## [1] 4
    ## 
    ## $babies
    ## [1] 0
    ## 
    ## $meal
    ## [1] 0
    ## 
    ## $country
    ## [1] 0
    ## 
    ## $market_segment
    ## [1] 0
    ## 
    ## $distribution_channel
    ## [1] 0
    ## 
    ## $is_repeated_guest
    ## [1] 0
    ## 
    ## $previous_cancellations
    ## [1] 0
    ## 
    ## $previous_bookings_not_canceled
    ## [1] 0
    ## 
    ## $reserved_room_type
    ## [1] 0
    ## 
    ## $assigned_room_type
    ## [1] 0
    ## 
    ## $booking_changes
    ## [1] 0
    ## 
    ## $deposit_type
    ## [1] 0
    ## 
    ## $agent
    ## [1] 0
    ## 
    ## $company
    ## [1] 0
    ## 
    ## $days_in_waiting_list
    ## [1] 0
    ## 
    ## $customer_type
    ## [1] 0
    ## 
    ## $adr
    ## [1] 0
    ## 
    ## $required_car_parking_spaces
    ## [1] 0
    ## 
    ## $total_of_special_requests
    ## [1] 0
    ## 
    ## $reservation_status
    ## [1] 0
    ## 
    ## $reservation_status_date
    ## [1] 0

We have 4 NA values in the ‘children’ column. This represents a very
small portion of the dataset so I am removing the rows with the missing
values.

#### 4.5.4 Remove NA values

``` r
hotel_bookings_v2 <- hotel_bookings_v2[!is.na(hotel_bookings_v2$children),]

glimpse(hotel_bookings_v2)
```

    ## Rows: 87,392
    ## Columns: 32
    ## $ hotel                          <chr> "Resort Hotel", "Resort Hotel", "Resort…
    ## $ is_canceled                    <int> 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, …
    ## $ lead_time                      <int> 342, 737, 7, 13, 14, 0, 9, 85, 75, 23, …
    ## $ arrival_date_year              <int> 2015, 2015, 2015, 2015, 2015, 2015, 201…
    ## $ arrival_date_month             <chr> "July", "July", "July", "July", "July",…
    ## $ arrival_date_week_number       <int> 27, 27, 27, 27, 27, 27, 27, 27, 27, 27,…
    ## $ arrival_date_day_of_month      <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ stays_in_weekend_nights        <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ stays_in_week_nights           <int> 0, 0, 1, 1, 2, 2, 2, 3, 3, 4, 4, 4, 4, …
    ## $ adults                         <int> 2, 2, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ children                       <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, …
    ## $ babies                         <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ meal                           <chr> "BB", "BB", "BB", "BB", "BB", "BB", "FB…
    ## $ country                        <chr> "PRT", "PRT", "GBR", "GBR", "GBR", "PRT…
    ## $ market_segment                 <chr> "Direct", "Direct", "Direct", "Corporat…
    ## $ distribution_channel           <chr> "Direct", "Direct", "Direct", "Corporat…
    ## $ is_repeated_guest              <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ previous_cancellations         <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ previous_bookings_not_canceled <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ reserved_room_type             <chr> "C", "C", "A", "A", "A", "C", "C", "A",…
    ## $ assigned_room_type             <chr> "C", "C", "C", "A", "A", "C", "C", "A",…
    ## $ booking_changes                <int> 3, 4, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, …
    ## $ deposit_type                   <chr> "No Deposit", "No Deposit", "No Deposit…
    ## $ agent                          <chr> "NULL", "NULL", "NULL", "304", "240", "…
    ## $ company                        <chr> "NULL", "NULL", "NULL", "NULL", "NULL",…
    ## $ days_in_waiting_list           <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ customer_type                  <chr> "Transient", "Transient", "Transient", …
    ## $ adr                            <dbl> 0.00, 0.00, 75.00, 75.00, 98.00, 107.00…
    ## $ required_car_parking_spaces    <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ total_of_special_requests      <int> 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 0, 3, 1, …
    ## $ reservation_status             <chr> "Check-Out", "Check-Out", "Check-Out", …
    ## $ reservation_status_date        <chr> "2015-07-01", "2015-07-01", "2015-07-02…

#### 4.5.5 Check ‘NULL’ values

I noticed a significant number or ‘NULL’ values in the ‘agent’ and
‘company’ columns and some in the ‘country’ column.

``` r
print(paste("NULL in agent: ", sum(hotel_bookings_v2$agent == "NULL")))
```

    ## [1] "NULL in agent:  12191"

``` r
print(paste("NULL in company: ", sum(hotel_bookings_v2$company == "NULL")))
```

    ## [1] "NULL in company:  82133"

``` r
print(paste("NULL in country: ", sum(hotel_bookings_v2$country == "NULL")))
```

    ## [1] "NULL in country:  452"

The original
[article](https://www.sciencedirect.com/science/article/pii/S2352340918315191)
states the following:

*The PMS assured no missing data exists in its database tables. However,
in some categorical variables like Agent or Company, “NULL” is presented
as one of the categories. This should not be considered a missing value,
but rather as “not applicable”. For example, if a booking “Agent” is
defined as “NULL” it means that the booking did not came from a travel
agent.*

For now I leave it as is.

#### 4.5.6 Check categories

Let’s review the columns with specific categories to see if there are
any inconsistencies / typos or redundant data. I am also creating some
quick plots to get an idea about the occurrence of the different
categories. This might provide some directions for further exploration.

- **hotel**

We should have two categories for hotel: City Hotel and Resort Hotel

``` r
unique(hotel_bookings_v2$hotel)
```

    ## [1] "Resort Hotel" "City Hotel"

Create plot for a quick visual representation.

``` r
ggplot(data = hotel_bookings_v2) +
  geom_bar(mapping = aes(x = hotel, fill = hotel)) +
  labs(title = "Hotel types", x = " ", y = " ") +
  theme(legend.position = "none")
```

![](hotel_bookings_case_study_files/figure-gfm/bar%20chart%20hotel%20categories-1.png)<!-- -->

- **meal**

  - Undefined/SC – no meal package
  - BB – Bed & Breakfast
  - HB – Half board (breakfast and one other meal – usually dinner)
  - FB – Full board (breakfast, lunch and dinner)

``` r
unique(hotel_bookings_v2$meal)
```

    ## [1] "BB"        "FB"        "HB"        "SC"        "Undefined"

‘SC’ and ‘Undefined’ both mean no meal package so they can be
categorized as ‘SC’ = Self-catering. I am replacing ‘Undefined’ with
‘SC’ across the column.

``` r
hotel_bookings_v2 <- hotel_bookings_v2 %>%
  mutate(meal = str_replace(meal,"Undefined", "SC"))

unique(hotel_bookings_v2$meal)
```

    ## [1] "BB" "FB" "HB" "SC"

Create visual.

``` r
ggplot(data = hotel_bookings_v2) +
  geom_bar(mapping = aes(x = meal, fill = meal)) +
  labs(title = "Meal types", x = " ", y = " ") +
  theme(legend.position = "none")
```

![](hotel_bookings_case_study_files/figure-gfm/bar%20chart%20meal-1.png)<!-- -->

- **market_segment**
  - TA = Travel Agents
  - TO = Tour Operators

``` r
unique(hotel_bookings_v2$market_segment)
```

    ## [1] "Direct"        "Corporate"     "Online TA"     "Offline TA/TO"
    ## [5] "Complementary" "Groups"        "Aviation"

``` r
ggplot(data = hotel_bookings_v2) +
  geom_bar(mapping = aes(x = market_segment, fill = market_segment)) +
  labs(title = "Market segments", x = " ", y = " ") +
  theme(legend.position = "none") +
  coord_flip()
```

![](hotel_bookings_case_study_files/figure-gfm/bar%20chart%20market%20segment-1.png)<!-- -->

- **distribution_channel**

  - TA = Travel Agents
  - TO = Tour Operators

``` r
unique(hotel_bookings_v2$distribution_channel)
```

    ## [1] "Direct"    "Corporate" "TA/TO"     "Undefined" "GDS"

Note: GDS = Global Distribution Systems *Global distribution systems
(GDS) are an important distribution channel for connecting with travel
agents. Travel agents use this system to browse hotels, view rates, and
check availability.*
([Reference](https://www.cvent.com/en/blog/hospitality/hotel-distribution-channels))

``` r
ggplot(data = hotel_bookings_v2) +
  geom_bar(mapping = aes(x = distribution_channel, fill = distribution_channel)) +
  labs(title = "Distribution channels", x = " ", y = " ") +
  theme(legend.position = "none")
```

![](hotel_bookings_case_study_files/figure-gfm/unnamed-chunk-1-1.png)<!-- -->

- **deposit_type**

  - No Deposit – no deposit was made
  - Non Refund – a deposit was made in the value of the total stay cost
  - Refundable – a deposit was made with a value under the total cost of
    stay.

``` r
unique(hotel_bookings_v2$deposit_type)
```

    ## [1] "No Deposit" "Refundable" "Non Refund"

``` r
ggplot(data = hotel_bookings_v2) +
  geom_bar(mapping = aes(x = deposit_type, fill = deposit_type)) +
  labs(title = "Deposit types", x = " ", y = " ") +
  theme(legend.position = "none")
```

![](hotel_bookings_case_study_files/figure-gfm/bar%20chart%20deposit%20type-1.png)<!-- -->

- **customer_type**

  - Contract
  - Group
  - Transient
  - Transient-party

``` r
unique(hotel_bookings_v2$customer_type)
```

    ## [1] "Transient"       "Contract"        "Transient-Party" "Group"

``` r
ggplot(data = hotel_bookings_v2) +
  geom_bar(mapping = aes(x = customer_type, fill = customer_type)) +
  labs(title = "Customer types", x = " ", y = " ") +
  theme(legend.position = "none")
```

![](hotel_bookings_case_study_files/figure-gfm/bar%20chart%20customer%20type-1.png)<!-- -->

- **reservation_status**

  - Canceled
  - Check-Out
  - No-Show

``` r
unique(hotel_bookings_v2$reservation_status)
```

    ## [1] "Check-Out" "Canceled"  "No-Show"

``` r
ggplot(data = hotel_bookings_v2) +
  geom_bar(mapping = aes(x = reservation_status, fill = reservation_status)) +
  labs(title = "Reservation status", x = " ", y = " ") +
  theme(legend.position = "none")
```

![](hotel_bookings_case_study_files/figure-gfm/bar%20chart%20reservation%20status-1.png)<!-- -->

I modified the ‘Undefined’ category in the ‘meal’ column by merging it
into the category ‘SC’. Categories in the other columns were fine.

#### 4.5.7 Check countries & create column for continents

It would be convenient for our analysis later if we had a column with
whole country names and a column for continents.

Let’s start with checking the ‘country’ column that contains country ISO
3166-1 alphe 3 codes. All code should be 3 digits long.

``` r
unique(hotel_bookings_v2$country)
```

    ##   [1] "PRT"  "GBR"  "USA"  "ESP"  "IRL"  "FRA"  "NULL" "ROU"  "NOR"  "OMN" 
    ##  [11] "ARG"  "POL"  "DEU"  "BEL"  "CHE"  "CN"   "GRC"  "ITA"  "NLD"  "DNK" 
    ##  [21] "RUS"  "SWE"  "AUS"  "EST"  "CZE"  "BRA"  "FIN"  "MOZ"  "BWA"  "LUX" 
    ##  [31] "SVN"  "ALB"  "IND"  "CHN"  "MEX"  "MAR"  "UKR"  "SMR"  "LVA"  "PRI" 
    ##  [41] "SRB"  "CHL"  "AUT"  "BLR"  "LTU"  "TUR"  "ZAF"  "AGO"  "ISR"  "CYM" 
    ##  [51] "ZMB"  "CPV"  "ZWE"  "DZA"  "KOR"  "CRI"  "HUN"  "ARE"  "TUN"  "JAM" 
    ##  [61] "HRV"  "HKG"  "IRN"  "GEO"  "AND"  "GIB"  "URY"  "JEY"  "CAF"  "CYP" 
    ##  [71] "COL"  "GGY"  "KWT"  "NGA"  "MDV"  "VEN"  "SVK"  "FJI"  "KAZ"  "PAK" 
    ##  [81] "IDN"  "LBN"  "PHL"  "SEN"  "SYC"  "AZE"  "BHR"  "NZL"  "THA"  "DOM" 
    ##  [91] "MKD"  "MYS"  "ARM"  "JPN"  "LKA"  "CUB"  "CMR"  "BIH"  "MUS"  "COM" 
    ## [101] "SUR"  "UGA"  "BGR"  "CIV"  "JOR"  "SYR"  "SGP"  "BDI"  "SAU"  "VNM" 
    ## [111] "PLW"  "QAT"  "EGY"  "PER"  "MLT"  "MWI"  "ECU"  "MDG"  "ISL"  "UZB" 
    ## [121] "NPL"  "BHS"  "MAC"  "TGO"  "TWN"  "DJI"  "STP"  "KNA"  "ETH"  "IRQ" 
    ## [131] "HND"  "RWA"  "KHM"  "MCO"  "BGD"  "IMN"  "TJK"  "NIC"  "BEN"  "VGB" 
    ## [141] "TZA"  "GAB"  "GHA"  "TMP"  "GLP"  "KEN"  "LIE"  "GNB"  "MNE"  "UMI" 
    ## [151] "MYT"  "FRO"  "MMR"  "PAN"  "BFA"  "LBY"  "MLI"  "NAM"  "BOL"  "PRY" 
    ## [161] "BRB"  "ABW"  "AIA"  "SLV"  "DMA"  "PYF"  "GUY"  "LCA"  "ATA"  "GTM" 
    ## [171] "ASM"  "MRT"  "NCL"  "KIR"  "SDN"  "ATF"  "SLE"  "LAO"

I noticed we have “CN” for China, instead of “CHN”. Let’s fix that.

``` r
hotel_bookings_v2 <- hotel_bookings_v2 %>%
  mutate(country = str_replace(country,"CN", "CHN"))

unique(hotel_bookings_v2$country)
```

    ##   [1] "PRT"  "GBR"  "USA"  "ESP"  "IRL"  "FRA"  "NULL" "ROU"  "NOR"  "OMN" 
    ##  [11] "ARG"  "POL"  "DEU"  "BEL"  "CHE"  "CHN"  "GRC"  "ITA"  "NLD"  "DNK" 
    ##  [21] "RUS"  "SWE"  "AUS"  "EST"  "CZE"  "BRA"  "FIN"  "MOZ"  "BWA"  "LUX" 
    ##  [31] "SVN"  "ALB"  "IND"  "MEX"  "MAR"  "UKR"  "SMR"  "LVA"  "PRI"  "SRB" 
    ##  [41] "CHL"  "AUT"  "BLR"  "LTU"  "TUR"  "ZAF"  "AGO"  "ISR"  "CYM"  "ZMB" 
    ##  [51] "CPV"  "ZWE"  "DZA"  "KOR"  "CRI"  "HUN"  "ARE"  "TUN"  "JAM"  "HRV" 
    ##  [61] "HKG"  "IRN"  "GEO"  "AND"  "GIB"  "URY"  "JEY"  "CAF"  "CYP"  "COL" 
    ##  [71] "GGY"  "KWT"  "NGA"  "MDV"  "VEN"  "SVK"  "FJI"  "KAZ"  "PAK"  "IDN" 
    ##  [81] "LBN"  "PHL"  "SEN"  "SYC"  "AZE"  "BHR"  "NZL"  "THA"  "DOM"  "MKD" 
    ##  [91] "MYS"  "ARM"  "JPN"  "LKA"  "CUB"  "CMR"  "BIH"  "MUS"  "COM"  "SUR" 
    ## [101] "UGA"  "BGR"  "CIV"  "JOR"  "SYR"  "SGP"  "BDI"  "SAU"  "VNM"  "PLW" 
    ## [111] "QAT"  "EGY"  "PER"  "MLT"  "MWI"  "ECU"  "MDG"  "ISL"  "UZB"  "NPL" 
    ## [121] "BHS"  "MAC"  "TGO"  "TWN"  "DJI"  "STP"  "KNA"  "ETH"  "IRQ"  "HND" 
    ## [131] "RWA"  "KHM"  "MCO"  "BGD"  "IMN"  "TJK"  "NIC"  "BEN"  "VGB"  "TZA" 
    ## [141] "GAB"  "GHA"  "TMP"  "GLP"  "KEN"  "LIE"  "GNB"  "MNE"  "UMI"  "MYT" 
    ## [151] "FRO"  "MMR"  "PAN"  "BFA"  "LBY"  "MLI"  "NAM"  "BOL"  "PRY"  "BRB" 
    ## [161] "ABW"  "AIA"  "SLV"  "DMA"  "PYF"  "GUY"  "LCA"  "ATA"  "GTM"  "ASM" 
    ## [171] "MRT"  "NCL"  "KIR"  "SDN"  "ATF"  "SLE"  "LAO"

Now let’s create new column for country names. To do this, we need to
load the ‘countrycode’ package.

``` r
library(countrycode)
```

Create new column ‘country_name’

``` r
hotel_bookings_v2$country_name <- countrycode(hotel_bookings_v2$country, origin = "iso3c", destination = "country.name")
```

    ## Warning in countrycode_convert(sourcevar = sourcevar, origin = origin, destination = dest, : Some values were not matched unambiguously: NULL, TMP

Create new column continent

``` r
hotel_bookings_v2$continent <- countrycode(hotel_bookings_v2$country, origin = "iso3c", destination = "continent")
```

    ## Warning in countrycode_convert(sourcevar = sourcevar, origin = origin, destination = dest, : Some values were not matched unambiguously: ATA, ATF, NULL, TMP, UMI

``` r
glimpse(hotel_bookings_v2)
```

    ## Rows: 87,392
    ## Columns: 34
    ## $ hotel                          <chr> "Resort Hotel", "Resort Hotel", "Resort…
    ## $ is_canceled                    <int> 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, …
    ## $ lead_time                      <int> 342, 737, 7, 13, 14, 0, 9, 85, 75, 23, …
    ## $ arrival_date_year              <int> 2015, 2015, 2015, 2015, 2015, 2015, 201…
    ## $ arrival_date_month             <chr> "July", "July", "July", "July", "July",…
    ## $ arrival_date_week_number       <int> 27, 27, 27, 27, 27, 27, 27, 27, 27, 27,…
    ## $ arrival_date_day_of_month      <int> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, …
    ## $ stays_in_weekend_nights        <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ stays_in_week_nights           <int> 0, 0, 1, 1, 2, 2, 2, 3, 3, 4, 4, 4, 4, …
    ## $ adults                         <int> 2, 2, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ children                       <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, …
    ## $ babies                         <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ meal                           <chr> "BB", "BB", "BB", "BB", "BB", "BB", "FB…
    ## $ country                        <chr> "PRT", "PRT", "GBR", "GBR", "GBR", "PRT…
    ## $ market_segment                 <chr> "Direct", "Direct", "Direct", "Corporat…
    ## $ distribution_channel           <chr> "Direct", "Direct", "Direct", "Corporat…
    ## $ is_repeated_guest              <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ previous_cancellations         <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ previous_bookings_not_canceled <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ reserved_room_type             <chr> "C", "C", "A", "A", "A", "C", "C", "A",…
    ## $ assigned_room_type             <chr> "C", "C", "C", "A", "A", "C", "C", "A",…
    ## $ booking_changes                <int> 3, 4, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, …
    ## $ deposit_type                   <chr> "No Deposit", "No Deposit", "No Deposit…
    ## $ agent                          <chr> "NULL", "NULL", "NULL", "304", "240", "…
    ## $ company                        <chr> "NULL", "NULL", "NULL", "NULL", "NULL",…
    ## $ days_in_waiting_list           <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ customer_type                  <chr> "Transient", "Transient", "Transient", …
    ## $ adr                            <dbl> 0.00, 0.00, 75.00, 75.00, 98.00, 107.00…
    ## $ required_car_parking_spaces    <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ total_of_special_requests      <int> 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 0, 3, 1, …
    ## $ reservation_status             <chr> "Check-Out", "Check-Out", "Check-Out", …
    ## $ reservation_status_date        <chr> "2015-07-01", "2015-07-01", "2015-07-02…
    ## $ country_name                   <chr> "Portugal", "Portugal", "United Kingdom…
    ## $ continent                      <chr> "Europe", "Europe", "Europe", "Europe",…

We have some unmatched values for ‘country_name’ and for ‘continent’ as
well. Let’s see how many missing values this means.

``` r
sum(is.na(hotel_bookings_v2$country_name))
```

    ## [1] 455

``` r
sum(is.na(hotel_bookings_v2$continent))
```

    ## [1] 459

This is something we have to keep in mind.

#### 4.5.8 Create new column ‘arrival_date_full’

The ‘arrival_date_year’ and ‘arrival_date_day_of_month’ values are
integers, while ‘arrival_date_month’ values are characters.

Make them consistent to be able to unite them: convert the year and day
values to characters.

``` r
hotel_bookings_v2$arrival_date_year <- as.character(hotel_bookings_v2$arrival_date_year)

hotel_bookings_v2$arrival_date_day_of_month <- as.character(hotel_bookings_v2$arrival_date_day_of_month)

glimpse(hotel_bookings_v2)
```

    ## Rows: 87,392
    ## Columns: 34
    ## $ hotel                          <chr> "Resort Hotel", "Resort Hotel", "Resort…
    ## $ is_canceled                    <int> 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, …
    ## $ lead_time                      <int> 342, 737, 7, 13, 14, 0, 9, 85, 75, 23, …
    ## $ arrival_date_year              <chr> "2015", "2015", "2015", "2015", "2015",…
    ## $ arrival_date_month             <chr> "July", "July", "July", "July", "July",…
    ## $ arrival_date_week_number       <int> 27, 27, 27, 27, 27, 27, 27, 27, 27, 27,…
    ## $ arrival_date_day_of_month      <chr> "1", "1", "1", "1", "1", "1", "1", "1",…
    ## $ stays_in_weekend_nights        <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ stays_in_week_nights           <int> 0, 0, 1, 1, 2, 2, 2, 3, 3, 4, 4, 4, 4, …
    ## $ adults                         <int> 2, 2, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ children                       <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, …
    ## $ babies                         <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ meal                           <chr> "BB", "BB", "BB", "BB", "BB", "BB", "FB…
    ## $ country                        <chr> "PRT", "PRT", "GBR", "GBR", "GBR", "PRT…
    ## $ market_segment                 <chr> "Direct", "Direct", "Direct", "Corporat…
    ## $ distribution_channel           <chr> "Direct", "Direct", "Direct", "Corporat…
    ## $ is_repeated_guest              <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ previous_cancellations         <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ previous_bookings_not_canceled <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ reserved_room_type             <chr> "C", "C", "A", "A", "A", "C", "C", "A",…
    ## $ assigned_room_type             <chr> "C", "C", "C", "A", "A", "C", "C", "A",…
    ## $ booking_changes                <int> 3, 4, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, …
    ## $ deposit_type                   <chr> "No Deposit", "No Deposit", "No Deposit…
    ## $ agent                          <chr> "NULL", "NULL", "NULL", "304", "240", "…
    ## $ company                        <chr> "NULL", "NULL", "NULL", "NULL", "NULL",…
    ## $ days_in_waiting_list           <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ customer_type                  <chr> "Transient", "Transient", "Transient", …
    ## $ adr                            <dbl> 0.00, 0.00, 75.00, 75.00, 98.00, 107.00…
    ## $ required_car_parking_spaces    <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ total_of_special_requests      <int> 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 0, 3, 1, …
    ## $ reservation_status             <chr> "Check-Out", "Check-Out", "Check-Out", …
    ## $ reservation_status_date        <chr> "2015-07-01", "2015-07-01", "2015-07-02…
    ## $ country_name                   <chr> "Portugal", "Portugal", "United Kingdom…
    ## $ continent                      <chr> "Europe", "Europe", "Europe", "Europe",…

Now we can combine the three columns together to get a full arrival
date: ‘arrival_date_full’.

``` r
hotel_bookings_v2 <- hotel_bookings_v2 %>%
  unite("arrival_date_full", arrival_date_year,arrival_date_month,arrival_date_day_of_month, sep = "-", remove = FALSE)

hotel_bookings_v2 <- hotel_bookings_v2 %>%
  mutate(arrival_date_full = ymd(arrival_date_full))

glimpse(hotel_bookings_v2)
```

    ## Rows: 87,392
    ## Columns: 35
    ## $ hotel                          <chr> "Resort Hotel", "Resort Hotel", "Resort…
    ## $ is_canceled                    <int> 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, …
    ## $ lead_time                      <int> 342, 737, 7, 13, 14, 0, 9, 85, 75, 23, …
    ## $ arrival_date_full              <date> 2015-07-01, 2015-07-01, 2015-07-01, 20…
    ## $ arrival_date_year              <chr> "2015", "2015", "2015", "2015", "2015",…
    ## $ arrival_date_month             <chr> "July", "July", "July", "July", "July",…
    ## $ arrival_date_week_number       <int> 27, 27, 27, 27, 27, 27, 27, 27, 27, 27,…
    ## $ arrival_date_day_of_month      <chr> "1", "1", "1", "1", "1", "1", "1", "1",…
    ## $ stays_in_weekend_nights        <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ stays_in_week_nights           <int> 0, 0, 1, 1, 2, 2, 2, 3, 3, 4, 4, 4, 4, …
    ## $ adults                         <int> 2, 2, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, …
    ## $ children                       <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, …
    ## $ babies                         <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ meal                           <chr> "BB", "BB", "BB", "BB", "BB", "BB", "FB…
    ## $ country                        <chr> "PRT", "PRT", "GBR", "GBR", "GBR", "PRT…
    ## $ market_segment                 <chr> "Direct", "Direct", "Direct", "Corporat…
    ## $ distribution_channel           <chr> "Direct", "Direct", "Direct", "Corporat…
    ## $ is_repeated_guest              <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ previous_cancellations         <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ previous_bookings_not_canceled <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ reserved_room_type             <chr> "C", "C", "A", "A", "A", "C", "C", "A",…
    ## $ assigned_room_type             <chr> "C", "C", "C", "A", "A", "C", "C", "A",…
    ## $ booking_changes                <int> 3, 4, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, …
    ## $ deposit_type                   <chr> "No Deposit", "No Deposit", "No Deposit…
    ## $ agent                          <chr> "NULL", "NULL", "NULL", "304", "240", "…
    ## $ company                        <chr> "NULL", "NULL", "NULL", "NULL", "NULL",…
    ## $ days_in_waiting_list           <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ customer_type                  <chr> "Transient", "Transient", "Transient", …
    ## $ adr                            <dbl> 0.00, 0.00, 75.00, 75.00, 98.00, 107.00…
    ## $ required_car_parking_spaces    <int> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, …
    ## $ total_of_special_requests      <int> 0, 0, 0, 0, 1, 0, 1, 1, 0, 0, 0, 3, 1, …
    ## $ reservation_status             <chr> "Check-Out", "Check-Out", "Check-Out", …
    ## $ reservation_status_date        <chr> "2015-07-01", "2015-07-01", "2015-07-02…
    ## $ country_name                   <chr> "Portugal", "Portugal", "United Kingdom…
    ## $ continent                      <chr> "Europe", "Europe", "Europe", "Europe",…

### 4.6 Key steps take in the Process Phase

- Set up RStudio Desktop environment, loaded the necessary packages
- Imported csv file, created data frame ‘hotel_bookings’
- Viewed data with `glimpse()`, `head()`
- Cleaned and transformed data:
  - created new data frame ‘hotel_bookings_v2’
  - checked and removed duplicates
  - checked NA values, removed affected rows
  - checked NULL values
  - checked categories, merged ‘SC’ and ‘Undefined’ in ‘meal’
  - created columns ‘country_name’ and ‘continent’ from ‘country’, noted
    unmatched values
  - created column ‘arrival_date_full’

## 5. Analyze Phase

### 5.1 Summary statistics

``` r
hotel_bookings_v2 %>%
  select(lead_time, stays_in_weekend_nights, stays_in_week_nights,adults,children,babies,previous_cancellations,previous_bookings_not_canceled,booking_changes,days_in_waiting_list,adr,required_car_parking_spaces,total_of_special_requests) %>%
  summary()
```

    ##    lead_time      stays_in_weekend_nights stays_in_week_nights     adults      
    ##  Min.   :  0.00   Min.   : 0.000          Min.   : 0.000       Min.   : 0.000  
    ##  1st Qu.: 11.00   1st Qu.: 0.000          1st Qu.: 1.000       1st Qu.: 2.000  
    ##  Median : 49.00   Median : 1.000          Median : 2.000       Median : 2.000  
    ##  Mean   : 79.89   Mean   : 1.005          Mean   : 2.625       Mean   : 1.876  
    ##  3rd Qu.:125.00   3rd Qu.: 2.000          3rd Qu.: 4.000       3rd Qu.: 2.000  
    ##  Max.   :737.00   Max.   :19.000          Max.   :50.000       Max.   :55.000  
    ##     children           babies         previous_cancellations
    ##  Min.   : 0.0000   Min.   : 0.00000   Min.   : 0.00000      
    ##  1st Qu.: 0.0000   1st Qu.: 0.00000   1st Qu.: 0.00000      
    ##  Median : 0.0000   Median : 0.00000   Median : 0.00000      
    ##  Mean   : 0.1386   Mean   : 0.01082   Mean   : 0.03042      
    ##  3rd Qu.: 0.0000   3rd Qu.: 0.00000   3rd Qu.: 0.00000      
    ##  Max.   :10.0000   Max.   :10.00000   Max.   :26.00000      
    ##  previous_bookings_not_canceled booking_changes   days_in_waiting_list
    ##  Min.   : 0.000                 Min.   : 0.0000   Min.   :  0.0000    
    ##  1st Qu.: 0.000                 1st Qu.: 0.0000   1st Qu.:  0.0000    
    ##  Median : 0.000                 Median : 0.0000   Median :  0.0000    
    ##  Mean   : 0.184                 Mean   : 0.2716   Mean   :  0.7496    
    ##  3rd Qu.: 0.000                 3rd Qu.: 0.0000   3rd Qu.:  0.0000    
    ##  Max.   :72.000                 Max.   :21.0000   Max.   :391.0000    
    ##       adr          required_car_parking_spaces total_of_special_requests
    ##  Min.   :  -6.38   Min.   :0.00000             Min.   :0.0000           
    ##  1st Qu.:  72.00   1st Qu.:0.00000             1st Qu.:0.0000           
    ##  Median :  98.10   Median :0.00000             Median :0.0000           
    ##  Mean   : 106.34   Mean   :0.08423             Mean   :0.6985           
    ##  3rd Qu.: 134.00   3rd Qu.:0.00000             3rd Qu.:1.0000           
    ##  Max.   :5400.00   Max.   :8.00000             Max.   :5.0000
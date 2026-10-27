# Hotel Booking Performance Dashboard

I built this project to explore hotel bookings and see how often guests completed their stays, canceled, or did not show up. I inspected the data in Excel, cleaned it in Google Colab, and used DAX measures in Power BI to analyze the results and build the dashboard.

<img width="1346" height="751" alt="Screenshot (86)" src="https://github.com/user-attachments/assets/24b805c4-a504-4ad0-8ffc-a265cf7ba349" />


## About the project

The dashboard looks at bookings for City Hotels and Resort Hotels. It includes booking totals, reservation outcomes, comparisons by country and hotel type, and booking counts by arrival month.

questions asked:

- How many bookings are in the dataset?
- How many resulted in a completed stay, a cancellation, or a no-show?
- Do City Hotels and Resort Hotels have different booking and cancellation patterns?
- Which countries and arrival months have the highest booking counts?

## Tools I used

- **Excel** to inspect the dataset.
- **Google Colab** to clean the data.
- **Power BI** to create DAX measures and build the dashboard.

## How I worked on the project

### Data inspection

I opened the dataset in Excel and reviewed its columns and records before starting the analysis.

I checked for: missing values, duplicates, inconsistent labels, or incorrect data types.

### Data cleaning

I used Google Colab to prepare the data for Power BI.

The steps I took were: 

I loaded the dataset into Google Colab and checked it for missing values, duplicate records, and data type issues. The data did not require cleaning, so I kept the records unchanged for the analysis.
The cleaned file is called: `hotel bookings`

### Analysis and dashboard

I imported the cleaned data into Power BI and wrote DAX measures for the dashboard. The report includes summary cards, charts, a hotel-type comparison, a reservation-status breakdown, a table, and filters for country and customer segment.

The measures I created include: 

## Measures and Calculations

I created DAX measures in Power BI to summarize bookings and reservation outcomes. The measures use the `reservation_status` field in the `Cleaned_Data` table. Each row is assumed to represent one booking.

### Total Bookings

Counts all booking records.

```DAX
Total Bookings =
COUNTROWS('Cleaned_Data')
```

### Completed Stays 

```DAX
CALCULATE(
    [Total Bookings],
    'Cleaned_Data'[reservation_status] = "Check-Out")
```

### Canceled and No-Show Bookings

```DAX 
CALCULATE(
    [Total Bookings],
    'Cleaned_Data'[reservation_status] IN {"Canceled", "No-Show"})
```

### non completion Rate 
```DAX
DIVIDE(
    [Canceled and No-Show Bookings],[Total Bookings])
```

### Completed Stay Rate 

```DAX
DIVIDE(
    [Completed Stays],
    [Total Bookings],
    0)
```

### No-Show Bookings 

```DAX
CALCULATE(
    [Total Bookings],
    'Cleaned_Data'[reservation_status] = "No-Show")
```


### No-Show Rate 

```DAX
DIVIDE(
    [No-Show Bookings],
    [Total Bookings],0)
```


## What I found

The dashboard shows **119,208 bookings** in total.

| Reservation outcome | Bookings | Share of bookings |
|---|---:|---:|
| Completed stay | 75,010 | 62.92% |
| Canceled | 42,992 | 36.06% |
| No-show | 1,206 | 1.01% |
| **Total** | **119,208** | **100%** |

The hotel-type breakdown is:

| Hotel type | Total bookings | Canceled | Completed stays | No-shows |
|---|---:|---:|---:|---:|
| City Hotel | 79,162 | 32,163 | 46,084 | 915 |
| Resort Hotel | 40,046 | 10,829 | 28,926 | 291 |
| **Total** | **119,208** | **42,992** | **75,010** | **1,206** |

Based on these table values, about **40.6% of City Hotel bookings** and **27.0% of Resort Hotel bookings** were canceled.

Portugal (`PRT`) has the longest bar in the country chart. August has the highest booking count shown in the arrival-month chart, while January has the lowest.

## What the results suggest

More bookings in this dataset were for City Hotels than Resort Hotels. City Hotels also had a higher cancellation rate in the table. That makes City Hotel cancellations a good place to look more closely, but the dashboard alone doesn’t tell us why the rates differ.

Portugal has the highest booking count among the countries shown. This is a count from the dataset; it doesn’t account for the number of hotels or rooms available in each country.

## Recommendations

- **Focus cancellation-reduction efforts on City Hotels.** The dashboard records 32,163 canceled City Hotel bookings, compared with 10,829 for Resort Hotels. The cancellation rate based on each hotel type’s booking total is about 40.6% for City Hotels and 27.0% for Resort Hotels. City Hotel managers should review their booking and cancellation process and consider sending guests confirmation messages and reminders before arrival.

- **Plan hotel resources around booking volume.** City Hotels account for 79,162 bookings and Resort Hotels for 40,046. Managers can use these volumes when planning staffing, room availability, and guest services, while reviewing each hotel type separately because their booking patterns differ.

- **Prepare for higher August demand.** August has the highest booking count shown in the arrival-month chart, while January has the lowest. Hotels could plan staffing and room availability for the busier period and consider promotions or packages during the quieter period.

- **Maintain attention on no-shows.** The dashboard records 1,206 no-shows. Hotels could use pre-arrival reminders and booking confirmations to help guests confirm their plans and reduce unused rooms.

- **Plan for demand from Portugal.** Portugal (`PRT`) has the highest booking count among the countries shown. Hotels could make sure their booking information and guest services are accessible to this customer market, while using booking counts together with room capacity when planning.

## Dataset information

- **Dataset name:** hotel booking
- **Source:** The data is originally from the article Hotel Booking Demand Datasets, written by Nuno Antonio, Ana 
Almeida, and Luis Nunes for Data in Brief, Volume 22, February 2019


**✈️ AeroInsights – Airline On-Time Performance Dashboard (Power BI Case Study)**

📌 Project Overview

The objective is to design an executive-level Power BI dashboard to help aviation leadership answer critical business questions:
Which routes have the worst on-time performance?
Which pilots consistently depart or arrive late?
How much delay is caused by weather conditions?
Which airports act as operational bottlenecks?
Are evening/night flights more delayed than daytime flights?
This project demonstrates advanced skills in:
Data Cleaning & Transformation (Power Query)
Data Modeling & Relationships
DAX Measures & Time Intelligence
KPI Design & Executive Reporting
Aviation Operations Analytics

📂 Dataset
File: Airline_OnTime_CaseStudy.xlsx
The dataset contains:
Flight details (Flight ID, Route, Airline)
Departure & Arrival times
Delay minutes
Pilot information
Weather condition flags
Airport details
Date & time fields

🛠 Tools & Technologies
Power BI Desktop
Power Query (ETL)
DAX (Data Analysis Expressions)
Excel (initial data review)

🔄 Data Preparation (Power Query)
1️⃣ Data Cleaning
Removed null/duplicate flight records
Standardized date & time formats
Converted delay columns to numeric
Created calculated columns:
OnTimeFlag
DepartureDelayCategory
ArrivalDelayCategory
TimeOfDayBucket (Morning/Afternoon/Evening/Night)

2️⃣ Data Transformation
Extracted:
Hour of departure
Day of week
Month
Split route into:
Origin Airport
Destination Airport

🧠 Data Model Design
Star schema approach:
Fact Table
Flights
Dimension Tables
Pilots
Airports
Date
Weather
Airlines

Relationships:
Flights → Pilots (Many-to-One)
Flights → Airports (Origin/Destination)
Flights → Date
Flights → Airlines
This ensures:
Accurate aggregations
Efficient filtering
Scalable performance

📊 Key DAX Measures
Total Flights = COUNT(Flights[FlightID])

Total Departure Delay = SUM(Flights[DepartureDelayMinutes])

Total Arrival Delay = SUM(Flights[ArrivalDelayMinutes])

On-Time % =
DIVIDE(
    CALCULATE(COUNT(Flights[FlightID]), Flights[OnTimeFlag] = "On-Time"),
    [Total Flights]
)

Weather Delay Minutes =
CALCULATE(
    SUM(Flights[ArrivalDelayMinutes]),
    Flights[WeatherFlag] = "Yes"
)

Avg Delay Per Flight =
DIVIDE([Total Arrival Delay], [Total Flights])

📈 Dashboard Pages & Insights
🛫 1. Route Performance Analysis

Visuals:
Bar chart: Average delay by route
Matrix: Route vs On-Time %
KPI card: Worst performing route

Insights Generated:
Identified routes with lowest on-time %
Highlighted consistently underperforming city pairs
Detected high-volume routes with systemic delays

👨‍✈️ 2. Pilot Performance Dashboard
Visuals:
Ranking table by average delay
Top 10 worst departure delays
Variance from airline average

Insights Generated:
Pilots consistently exceeding average delay
Patterns in specific shift timings
Identification of retraining candidates

🌦 3. Weather Impact Analysis
Visuals:
Weather vs Non-weather delay comparison
% of total delay caused by weather
Monthly weather delay trends

Insights Generated:
Quantified true operational vs uncontrollable delays
Seasonal delay spikes
Weather contribution to total delay (% impact)

🏢 4. Airport Bottleneck Analysis
Visuals:
Average departure delay by origin airport
Average arrival delay by destination
Heatmap of delay concentration

Insights Generated:
Identified bottleneck airports
Congestion patterns
Correlation between airport traffic and delay

🌙 5. Time-of-Day Analysis
Visuals:

Delay by time bucket (Morning/Afternoon/Evening/Night)
Line chart: Delay trend by hour

Insights Generated:
Evening and night flights show higher average delays
Late-day cascading delay effect
Operational scheduling improvement opportunities

🎯 Business Impact
This dashboard enables leadership to:
Improve route scheduling decisions
Optimize pilot performance management
Separate controllable vs uncontrollable delays
Identify infrastructure bottlenecks
Improve customer satisfaction metrics
Reduce operational costs

📌 Key Takeaways

Built a fully relational data model
Designed executive-level KPIs
Applied advanced DAX logic
Transformed raw aviation data into actionable insights
Delivered business-focused storytelling

📸 Dashboard Preview

<img width="2090" height="1158" alt="Airline_Case_Study_Dashboard" src="https://github.com/user-attachments/assets/bfe8793c-8c55-45f5-96c6-01fae952d69c" />



🚀 Future Enhancements

Predictive delay modeling (Machine Learning)
Weather severity index scoring
Crew pairing optimization analysis
Cost impact of delays
Real-time dashboard integration

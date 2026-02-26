**📊 Marketing Analytics Dashboard — Power BI Project**

📌 Project Overview

This project showcases a fully developed Marketing Performance Dashboard built in Microsoft Power BI using a multi-table relational dataset.
As a Marketing Data Analyst at a digital media agency, the objective was to:
Clean and transform raw marketing data
Build a proper star-schema data model
Create advanced performance metrics using DAX
Implement a bridge table (many-to-many relationship)
Design a professional, executive-ready dashboard
The final output is a one-page interactive dashboard built for leadership review.

📁 Dataset Information
File Used: marketing_assignment_dataset.xlsx

The dataset contains 5 sheets:
Table	Type	Description
MarketingCampaignData	Fact Table	Campaign performance metrics
CampaignMaster	Dimension	Campaign details
ChannelMaster	Dimension	Channel information
RegionTargets	Dimension	Revenue & conversion targets
Bridge_ChannelCampaign	Bridge	Many-to-many mapping between campaigns and channels

🔹 Part 1 — Data Preparation (Power Query)
✅ Load Data

Imported Excel file into Power BI Desktop
Loaded all 5 sheets as separate tables

✅ Data Type Validation

MarketingCampaignData
CampaignID → Whole Number
CampaignName / Channel / Region → Text
Impressions / Clicks / Conversions → Whole Number
Spend / Revenue → Decimal
Date → Date
Other Tables
Keys (CampaignID, BridgeID) → Whole Number
Text fields → Text

✅ Data Cleaning

Performed in Power Query:
Removed rows where:
Impressions = 0
Clicks = 0
Conversions = 0
Spend = 0
Removed duplicates (CampaignID + Date)
Trimmed & cleaned text fields
Standardized Region to UPPERCASE

✅ Custom Columns (Power Query)

TR = [Clicks] / [Impressions]
CPC = [Spend] / [Clicks]
CPA = [Spend] / [Conversions]
ROAS = [Revenue] / [Spend]

✅ Date Enhancements

Added:
Year
Month Number
Month Name
Week of Year

Closed & Applied changes.

🔹 Part 2 — Data Modeling

📅 Date Table (DAX)

DateTable =
ADDCOLUMNS(
    CALENDAR(MIN(MarketingCampaignData[Date]), MAX(MarketingCampaignData[Date])),
    "Year", YEAR([Date]),
    "Month", FORMAT([Date], "MMM"),
    "MonthNumber", MONTH([Date]),
    "Quarter", QUARTER([Date]),
    "Week", WEEKNUM([Date])
)

Marked as Date Table.

🔗 Relationships Created

From	Column	To	Column	Type
CampaignMaster	CampaignID	MarketingCampaignData	CampaignID	1:M
RegionTargets	Region	MarketingCampaignData	Region	1:M
DateTable	Date	MarketingCampaignData	Date	1:M
ChannelMaster	Channel	Bridge_ChannelCampaign	Channel	1:M
CampaignMaster	CampaignID	Bridge_ChannelCampaign	CampaignID	1:M
Bridge_ChannelCampaign	CampaignID	MarketingCampaignData	CampaignID	Inactive

⚠ The last relationship is intentionally inactive and activated via DAX.

🔹 Part 3 — DAX Measures

📊 Base Measures

Total Impressions = SUM(MarketingCampaignData[Impressions])
Total Clicks = SUM(MarketingCampaignData[Clicks])
Total Spend = SUM(MarketingCampaignData[Spend])
Total Conversions = SUM(MarketingCampaignData[Conversions])
Total Revenue = SUM(MarketingCampaignData[Revenue])

📈 Performance Metrics

CTR = DIVIDE([Total Clicks], [Total Impressions])
Conversion Rate = DIVIDE([Total Conversions], [Total Clicks])
CPC = DIVIDE([Total Spend], [Total Clicks])
CPA = DIVIDE([Total Spend], [Total Conversions])
ROI = DIVIDE([Total Revenue] - [Total Spend], [Total Spend])
ROAS = DIVIDE([Total Revenue], [Total Spend])

🔄 Bridge Table Activation (Advanced)

Spend by Channel =
CALCULATE(
    [Total Spend],
    USERELATIONSHIP(Bridge_ChannelCampaign[CampaignID], MarketingCampaignData[CampaignID])
)

🎯 Target Achievement Measures

Revenue Target % =
DIVIDE(
    [Total Revenue],
    AVERAGE(RegionTargets[TargetRevenue])
)

Conversion Target % =
DIVIDE(
    [Total Conversions],
    AVERAGE(RegionTargets[TargetConversions])
)

🔹 Part 4 — Dashboard Design

📌 KPI Cards

Total Spend
Total Revenue
ROI
Revenue Target %
Conversion Target %
Total Conversions
CTR

📊 Visuals Included

1️⃣ Channel Performance Matrix

Rows: Channel
Values: Spend, Revenue, Conversions, CPA, CTR

2️⃣ ROI by Channel

Column Chart
Axis: Channel
Value: ROI

3️⃣ Spend vs Revenue by Region

Clustered Bar Chart
Axis: Region
Values: Total Spend, Total Revenue

4️⃣ Revenue & Spend Trend

Line Chart
Axis: Date
Values: Total Revenue, Total Spend

5️⃣ Campaign Funnel

Funnel Visual
Impressions → Clicks → Conversions

6️⃣ Campaign Detail Table

Campaign details from CampaignMaster
Performance measures

🎛 Required Slicers

Channel
Region
Campaign Owner
Month

🔹 Part 5 — Professional Formatting

🎨 Theme

Primary: Dark Blue
Secondary: Teal
Accent: Orange
Font: Segoe UI

🏷 Page Header

Marketing Performance Dashboard
Font Size: 28
Bold
Background: Primary Color
Text: White
Center aligned

📦 KPI Card Styling

Category Label: ON (Size 12)
Value Size: 28
Background: White (15% transparency)
Border: ON
Shadow: ON

📊 Chart Formatting

Title: ON (Size 16, Bold, Primary Color)
Data Labels: ON
Legend: OFF (unless required)
Line markers: ON

🎨 Conditional Formatting

ROI > 0 → Green
ROI ≤ 0 → Red

CPA → Green to Red color scale

🧠 Tooltip Page

Created dedicated tooltip page including:
CTR
CPC
CPA
ROI

Tooltip enabled and assigned to visuals.

📈 Key Skills Demonstrated

Data Cleaning with Power Query
Star Schema Data Modeling
Many-to-Many Relationship Handling
Advanced DAX (USERELATIONSHIP)
KPI & Performance Metric Development
Executive Dashboard Design
Conditional Formatting
Tooltip Customization

🚀 Business Value

This dashboard enables leadership to:
Evaluate marketing efficiency across channels
Monitor ROI and target achievement
Compare regional performance
Identify high-performing campaigns
Track trends over time

🛠 Tools Used

Microsoft Power BI Desktop
Power Query
DAX

📌 How to Use

Open Power BI Desktop
Load marketing_assignment_dataset.xlsx
Follow transformation steps
Build relationships
Add DAX measures
Construct dashboard
Apply formatting

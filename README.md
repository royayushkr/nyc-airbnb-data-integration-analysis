# NYC Airbnb Market: Data Integration & Analysis

## 📌 Project Overview
This project analyzes the New York City Airbnb market using data from 2019. A key challenge addressed in this analysis is the integration of disparate data sources—listing prices stored in CSV, room types in Excel, and review history in TSV formats. The goal is to clean, merge, and aggregate this data to provide a snapshot of the market, focusing on pricing trends and the availability of private rooms.

## 🚀 Key Business Questions
* **Market Activity:** What is the active timeframe for the most recent reviews in the dataset?
* **Inventory Analysis:** How many listings are strictly "Private Rooms" compared to other accommodation types?
* **Pricing Strategy:** What is the average nightly price for an Airbnb listing in NYC?

## 🛠️ Technical Stack
* **Language:** Python 3.x
* **Libraries:**
    * **Pandas:** Advanced I/O (reading .csv, .tsv, .xlsx), string manipulation, and aggregation.
    * **NumPy:** Numerical operations.
* **Data Sources:** `airbnb_price.csv`, `airbnb_room_type.xlsx`, `airbnb_last_review.tsv`.

## 📊 Methodology & Insights

### 1. Multi-Format Data Ingestion
The analysis begins by loading data from three distinct file formats, demonstrating the capability to handle heterogeneous data systems:
* **Pricing:** Loaded from CSV.
* **Room Descriptions:** Loaded from Excel.
* **Reviews:** Loaded from TSV (Tab Separated Values).

### 2. Data Cleaning & Transformation
Raw data required significant preprocessing to be usable:
* **Date Normalization:** The `last_review` column was converted to datetime objects to extract the earliest and latest review dates.
* **String Sanitization:** Listing prices contained non-numeric characters (e.g., "225 dollars"). These were stripped and converted to floating-point numbers.
* **Categorical Standardization:** Room type descriptions were normalized to lowercase to ensure accurate counting of "private room" listings.

### 3. Aggregated Market Metrics
* **Review Window:** The dataset covers reviews from **January 1, 2019** to **July 9, 2019**.
* **Inventory Count:** There are **11,356** private rooms available, indicating a significant market for shared-space accommodations.
* **Average Cost:** The average listing price is approximately **$141.78** per night.

## 💻 Code Highlight: Data Cleaning & Aggregation
The project efficiently processes string data and performs aggregations to build a summary table.

```python
# Cleaning price data and converting to numeric
price['price'] = price['price'].str.replace('dollars', '').astype(float)
avg_price = round(price['price'].mean(), 2)

# Normalizing room types and counting specific categories
room_type['room_type'] = room_type['room_type'].str.lower()
nb_private_rooms = (room_type['room_type'] == 'private room').sum()

# Creating a summary DataFrame
review_dates = pd.DataFrame({
    'first_reviewed': first_reviewed,
    'last_reviewed': last_reviewed,
    'nb_private_rooms': nb_private_rooms,
    'avg_price': avg_price
}, index=[0])

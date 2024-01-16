# Data Analysis Summary

## Introduction
This data analysis project explores the dataset containing information about taxi data data. The analysis covers data collection, cleaning, and exploratory data analysis (EDA).

## Data Overview
The dataset consists of the following columns:
### yellow trip data

The dataset contains the following columns:
- **VendorID**:
        Code indicating the TPEP provider.
        Values: 1 = Creative Mobile Technologies, LLC; 2 = VeriFone Inc.

- **tpep_pickup_datetime**:
        Date and time when the meter was engaged.

- **tpep_dropoff_datetime**:
        Date and time when the meter was disengaged.

- **Passenger_count**:
        Number of passengers in the vehicle.
        Driver-entered value.

- **Trip_distance**:
        Elapsed trip distance in miles reported by the taximeter.

- **PULocationID**:
        TLC Taxi Zone where the taximeter was engaged.

- **DOLocationID**:
        TLC Taxi Zone where the taximeter was disengaged.

- **RateCodeID**:
        Final rate code at the end of the trip.
        Values: 1 = Standard rate, 2 = JFK, 3 = Newark, 4 = Nassau or Westchester, 5 = Negotiated fare, 6 = Group ride.

- **Store_and_fwd_flag**:
        Flag indicating whether the trip record was stored and forwarded.
        Values: Y = store and forward trip, N = not a store and forward trip.

- **Payment_type**:
        Numeric code signifying how the passenger paid for the trip.
        Values: 1 = Credit card, 2 = Cash, 3 = No charge, 4 = Dispute, 5 = Unknown, 6 = Voided trip.

- **Fare_amount**:
        Time-and-distance fare calculated by the meter.

- **Extra**:
        Miscellaneous extras and surcharges, including rush hour and overnight charges.

- **MTA_tax**:
        $0.50 MTA tax triggered based on the metered rate.

- **Improvement_surcharge**:
        $0.30 improvement surcharge for trips at the flag drop, initiated since 2015.

- **Tip_amount**:
        Tip amount, automatically populated for credit card tips. Cash tips not included.

- **Tolls_amount**:
        Total amount of all tolls paid during the trip.

- **Total_amount**:
        Total amount charged to passengers, excluding cash tips.

- **Congestion_Surcharge**:
        Total amount collected for the NYS congestion surcharge.

- **Airport_fee**:
        Field for airport fees.
 ### taxi zone data

- **LocationID:** Unique identifier for a specific location or taxi zone.
- **Borough:** Administrative division of the location (e.g., Manhattan, Brooklyn).
- **Zone:** Specific area or zone within the borough.
- **service_zone:** Additional categorization related to the service provided in the zone.


# Data Modeling
    fact tables and dimension tables are key components of a star schema or snowflake schema design. These concepts are commonly used in data modeling to organize and structure data for efficient querying and analysis. Let me explain each:
## Fact Table:
    A fact table contains quantitative data (facts) that can be analyzed. It typically consists of numeric measures, often called metrics, and foreign keys that link to dimension tables.
    Fact tables are usually large and contain transactional data.
    In the context of your taxi trip data, a fact table might contain measures like trip_distance, fare_amount, tip_amount, etc.

## Dimension Table:
    A dimension table contains descriptive attributes that provide context to the data in the fact table.
    Dimension tables are usually smaller in size compared to fact tables.
    They contain categorical data and are often used for filtering and grouping in analysis.
    In the context of your taxi trip data, dimension tables might include tables for Vendor, Location (pickup and dropoff locations), RateCode, PaymentType, etc.

    Dimension Tables:

        Time Dimension:
            time_id (primary key)
            pickup_datetime (from tpep_pickup_datetime)
            dropoff_datetime (from tpep_dropoff_datetime)

        
        Location Dimension:

            location_id (primary key)
            location_name (derived from the "Zone" column in the reference table)
            borough (derived from the "Borough" column in the reference table)
            service_zone (derived from the "service_zone" column in the reference table)

        Payment Type Dimension:
            payment_type_id (primary key)
            payment_type_name (from payment_type)

        Rate Code Dimension:
            rate_code_id (primary key)
            rate_code_description (from RatecodeID)

        Vendor Dimension:
            vendor_id (primary key)
            vendor_name (from VendorID)

    Fact Table:

        Trip Fact:
            trip_id (primary key)
            time_id (foreign key referencing Time Dimension)
            location_pickup_id (foreign key referencing Location Dimension for pickup)
            location_dropoff_id (foreign key referencing Location Dimension for dropoff)
            passenger_count
            trip_distance
            rate_code_id (foreign key referencing Rate Code Dimension)
            store_and_fwd_flag
            payment_type_id (foreign key referencing Payment Type Dimension)
            fare_amount
            extra
            mta_tax
            tip_amount
            tolls_amount
            improvement_surcharge
            total_amount
            congestion_surcharge
            airport_fee

This dimensional model follows a star schema, where the fact table (Trip Fact) is surrounded by dimension tables. Each dimension table contains descriptive attributes related to a specific aspect of the data, and the fact table contains quantitative data that can be analyzed.

## Key Findings

### Main Caegory Distribution
![Main Category Distribution Plot](figures/main_category_product_distribution.png)



Based on the results, we can gather the following insights:

- The top three main categories are Electronics, Computers & Accessories, and Home & Kitchen. This shows that these categories are popular among customers.

- The number of products in the other main categories is quite low, indicating that these categories are not as popular as the top three.

- Office Products, Musical Instruments, Home Improvement, Toys & Games, Car & Motorbike, and Health & Personal Care have a very small number of products, which may suggest that these categories have less demand.

- Overall, the data can help businesses understand the current market trends and identify potential opportunities for growth in specific categories.



### Sub Category Distribution
![Sub Category Distribution Plot](figures/last_category_product_distribution.png)

Based on the results, we can gather the following insights:

- The top six subcategories are USB cables, smartwatches, smartphones, smart televisions, in-ear headphones, and remote controls. These are the most popular subcategories, and businesses could focus on providing products in these categories to attract customers.

- Other popular subcategories include mixer grinders, HDMI cables, dry irons, mice, and instant water heaters. These subcategories may be less popular than the top six, but they still have a significant number of products, indicating that there is demand for them.

- The data shows that there is a diverse range of subcategories in the top 30, including kitchen appliances, home electronics, and personal accessories. This highlights the importance of offering a variety of products to cater to different customer needs and preferences.

- Overall, the data can help businesses identify the most popular subcategories and adjust their product offerings to meet customer demand. By focusing on these subcategories, businesses could increase their sales and improve their competitiveness in the market.

### Top main and sub-category by rating Distribution
![Top main and sub-category by rating](figures/top_main_category_product_distribution.png)


The majority of customer ratings fall within the 3-4 and 4-5 range, with a total of 1453 reviews.

There is a noticeable increase in the number of reviews in the 2-3 range compared to the lower 0-1 and 1-2 ranges.

The lowest number of reviews is found in the 0-1 range, indicating that there may be room for improvement in terms of customer satisfaction.

Overall, the distribution of customer ratings suggests that most customers are satisfied with the products, but there may be opportunities for improvement to increase the number of positive ratings.

![Top main and sub-category by rating](figures/top_sub_category_product_distribution.png)


Looking at the table, we can see the top and bottom sub-categories in terms of customer ratings.

It's great to see that the "Tablets" sub-category is at the top with a rating of 4.6, which indicates that customers are satisfied with their purchase.

However, there are some sub-categories at the bottom, such as "DustCovers" and "ElectricGrinders", which have lower ratings, implying that customers are not very happy with these products.

Insights like these can help businesses focus on improving the quality of their products and enhancing the overall customer experience. It's important to keep track of customer feedback to identify areas for improvement and continue to meet their needs and expectations.

### Review positive and negative sentiment Distribution
![Review positive sentiment](figures/review_word_analaysis.png)
![Review negative sentiment](figures/review_negative_word_analaysis.png)

The code generates a word cloud based on the reviews text in the dataset, allowing us to visually analyze the most common words used in the reviews. The larger the word in the cloud, the more frequently it appears in the reviews. This can provide insights into the overall sentiment of the customers, the most frequently mentioned product features or issues, and other important information that can help businesses improve their products and services. In the following example, you can see the word cloud for products with a rating greater than 4

### Additional Insights
- 
## Conclusion
This analysis provides a basic understanding of the dataset, highlighting key statistics and trends. Further analysis and modeling could be pursued based on these initial findings.

For more details, refer to the full Jupyter Notebooks in the `notebooks/` directory.

---

*Note: This is a template, and you should customize it based on the specifics of your analysis and findings.*

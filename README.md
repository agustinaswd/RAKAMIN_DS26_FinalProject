# Hello, We are BlueCode 

We're from Bootcamp Data Science Batch 26 Rakamin Academy, and this is our final project. 
Hotel booking cancellation is the lucky dataset that caught our attention. 

## Where to look for detail
You can find our dataset on [Kaggle](https://www.kaggle.com/datasets/mojtaba142/hotel-booking)

More detail about our dataset's variable description on [Google Docs](https://bit.ly/hotel_booking_variable_desc)

# Business Understanding
## Problem
"Cancellations are a key aspect of hotel revenue management because of their impact on room reservation systems" (Sánchez-Medina dkk, 2020).
"Rigid cancellation policies and  overbooking strategies can also have a negative influence on revenue and reputation" (Antonio dkk, 2017).
The number of cancellations of hotel orders becomes issue of concern to the management team
because it is directly related to revenue. Proper cancellation of policies is required somewhat
customers do not run to competitors

## Goal, Obj, Business Metric
- Goal : Decrease hotel cancellation rate
- Objective : Machine learning models to predict whether the customer will do cancelled or not, so the hotel can approach with that customer predicted to be cancelled
- Business Metric : cancellation rate

# Exploratory Data Analysis
- [Market Segment & Cancellation](https://user-images.githubusercontent.com/116469338/204178531-b6eddcd9-e73f-4002-85ef-ff92feecc5b7.jpg)
The customer likely makes a booking through an online travel agent. But, online travel agents (OTA) have the most booking cancellation
- [Arrival Month & Cancellation](https://user-images.githubusercontent.com/116469338/204179140-06422b09-8d5a-4bc2-a138-d6fb627d641e.png)
August has the most booking occurs. Peak summer in Portugal happen in August
- [Lead Time & Cancellation](https://user-images.githubusercontent.com/116469338/204179449-1c4ac343-bcf0-4236-8e47-ea4ae655f4bf.png)
Customers who have longer lead times have a higher cancellation rate
- [Deposit Type & Cancellation](https://user-images.githubusercontent.com/116469338/204179611-0357613f-a341-42df-b350-186fb73fca89.png)
Hotel booking by type non-refund deposits have the most significant cancellation rate  reach 99%. One of the reason is that no refunds have the biggest median lead times

# Data Preprocessing
- Data Cleansing
    - Handling missing value & duplicate
    - Drop personal data colums
    - Change 'undefined' value
    - Drop aduls = 0
    - Adjust data type
    - handle outlier
- Data Treatment
    - Log Transformation & Normalization
- Dataframe
    We have 3 dataframe:
    - df1 : not handling data cleansing, not handling feature transformation, not handling outliers with the Z-Score method
    - df2 : handling data cleansing, handling feature transformation, not handling outliers with the Z-Score method
    - df3 : handling data cleansing, handling feature transformation, handling outliers with the Z-Score method
- Class Imbalance
Our dataframe is balanced
- Feature Extraction
    - reserved_vs_assigned 
    - season
    - origin_type
    
# Modeling & Evaluation
- Split Data Train & Test
    - 70% data train
    - 30% data test
- Modeling Candidate
    - Logistic Regression
    - kNN
    - Decision Tree
    - GaussiaNB
    - Random Forest
    - XGBoost
    - CatBoost
    - AdaBoost
- Evaluation Model
We used **recall**
- Modeling
    - Modeling 1: used all feature (overfit / recall still low)
    - Modeling 2: feature selection with **featurewiz**
- Modeling Result
    - df3 is the best-fit model
    - With **hyperparameter tuning** we manage to increase recall from 75% become 76%
- [SHAP Value](https://user-images.githubusercontent.com/116469338/204266381-62792f0a-e3e1-4b62-bfa5-5d58c8056ccd.png) & 
[Summary Plot](https://user-images.githubusercontent.com/116469338/204266454-d1138938-f4ec-4102-85a6-dee4af205445.png)

# Business Recommendation
- Origin Type
    - Make special promos for local tourists like time-limited offer only can be claimed in time certain
    - Special promo for local tourists also done with hotel campaigns use google ads with location targeting Portuguese geography
- Market Segment
Cooperate with various online travel platforms agents, like doing promotions specifically for customers who book hotels through an online travel agent 
- Lead Time
Make a new strategy 60 days before the day of arrival to get various special promos. It will also make it easier for the hotel to apply room pricing dynamically depending on the event that will occur on the date booked by the consumer
- Deposit Type
Make new regulations; 60 days before arrival day is the maximum for no deposits type. The non-refund type will be applied to the customer who makes a booking with more than 60 days

# Simulation
- [Flowchart Hotel PMS Before ML](https://user-images.githubusercontent.com/116469338/204268657-aa1a49ac-6dd5-4c55-9e99-5b14f6eb741f.png)
- [Flowchart Hotel PMS After Integrate With ML](https://user-images.githubusercontent.com/116469338/204268674-b66e20c6-0b12-4614-844a-259e59b417d1.png)
- Simulation of Canceled Prediction 
[Assumption with 37% cancellation rate](https://user-images.githubusercontent.com/116469338/204269166-ffb5918e-cf69-4973-a86a-044f6afac78d.png)
With our model, we can predict 2812 customer who "will cancel" their booking, and we can give offers for them to prevent their cancel
- [Business Simulation for Revenue](https://user-images.githubusercontent.com/116469338/204269914-4219afe4-c5f9-4f55-853b-ab07ebc1b220.png)

We can increase hotel's revenue by 39.450.000 € 
- Wireframe UI/UX (OTA)
    - [Lead time](https://user-images.githubusercontent.com/116469338/204270693-ad2fe554-65fd-4c9d-b0de-c69085123b2b.png)
    - [Special promo for local tourists](https://user-images.githubusercontent.com/116469338/204276550-4cf913ed-0de3-4e2a-b200-96b662e7db18.png)
- Business Recommendation (additional)
    - Adding features (travel purpose, age, price) to improve model performance.
    - Gave recommendations for pricing the best room on the lead time of 24-26 days before the peak event/festival in Portugal (from external sources are known to most traveler in Spain the neighboring of Portugal, book their hotel 25 days before arrival).
    - Offer the right offer according to segmentation compiled from insight and modeling (category of offers can be seen in [Google Docs](https://bit.ly/offers_category))

# Reference
Antonio, N., de Almeida, A., & Nunes, L. (2019). Hotel Booking Demand Datasets. Data in Brief, 22, 41–49.
https://doi.org/10.1016/J.DIB.2018.11.126

Antonio, N., Almeida, A. de, & Nunes, L. (2017). Predicting Hotel Booking Cancellations to Decrease
Uncertainty and Increase Revenue. Tourism & Management Studies, 13(2), 25–39.
https://doi.org/10.18089/tms.2017.13203

Antonio, N., de Almeida, A., & Nunes, L. (2017). Predicting Hotel bookings Cancellation With a Machine
Learning Classification Model. Proceedings - 16th IEEE International Conference on Machine Learning
and Applications, ICMLA 2017, 2017-December, 1049–1054. https://doi.org/10.1109/ICMLA.2017.00-11

Boost Hotel bookings by optimizing your Booking Lead Time, (March 10, 2020).
https://blog.experience-hotel.com/boost-hotel-bookings-by-optimizing-your-booking-lead-time/

How Online Hotel Distribution Changing Is In Europe, (October 4, 2019).
https://www.d-edge.com/how-online-hotel-distribution-is-changing-in-europe/

Sánchez-Medina, A. J., & C-Sánchez, E. (2020). Using Machine Learning and Big Data for Efficient Forecasting
of Hotel Booking Cancellations. International Journal of Hospitality Management, 89, 102546.
https://doi.org/10.1016/J.IJHM.2020.102546

SiteMinder. (n.d.). How Far do Hotel Guests Book in Advance? Retrieved November 20, 2022, from
https://www.siteminder.com/r/hotel-distribution/hotel-revenue-management/hotel-guests-book-advance/
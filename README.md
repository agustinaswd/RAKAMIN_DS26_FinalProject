# Hello, We are BlueCode 

We're from Bootcamp Data Science Batch 26 Rakamin Academy, and this is our final project. 
Hotel booking cancellation is the lucky dataset that caught our attention. You can find our dataset on [Kaggle] (https://www.kaggle.com/datasets/mojtaba142/hotel-booking)

## This is our variable's description:
- hotel : Type of hotel
- is_canceled :  Value indicating if the booking was canceled (1) or not (0)
- lead_time : Number of days that elapsed between the entering date of the booking into the PMS and the arrival date
- arrival_date_year : Year of arrival date
- arrival_date_month : Month of arrival date with 12 categories: 
    “January” to “December”
- arrival_date_week_number : Week number of the arrival date
- arrival_date_day_of_month : Day of the month of the arrival date
- stays_in_weekend_nights : Number of weekend nights (Saturday or Sunday) the guest stayed or booked to stay at the hotel  
- stays_in_week_nights : Number of week nights (Monday to Friday) the guest stayed or booked to stay at the hotel
- adults : Number of adults
- children : Number of children
- babies :  Number of babies
- meal :  Type of meal booked. Categories are presented in standard hospitality meal packages: 
    - Undefined/SC: no meal package 
    - BB : Bed & Breakfast 
    - HB : Half board (breakfast and one other meal – usually dinner) 
    - FB : Full board (breakfast, lunch and dinner)
- country : Country of origin. Categories are represented in the ISO 3155–3:2013
- market_segment :  Market segment designation. In categories, the term “TA” means “Travel Agents” and “TO” means “Tour Operators”
- distribution_channel :  Booking distribution channel. The term “TA” means “Travel Agents” and “TO” means “Tour Operators”
- is_repeated_guest :  Value indicating if the booking name was from a repeated guest (1) or not (0)
- previous_cancellations : Number of previous bookings that were cancelled by the customer prior to the current booking
- previous_bookings_not_canceled : Number of previous bookings not cancelled by the customer prior to the current booking
- reserved_room_type : Code of room type reserved. Code is presented instead of designation for anonymity reasons
- assigned_room_type :  Code for the type of room assigned to the booking. Sometimes the assigned room type differs from the reserved room type due to hotel operation reasons (e.g. overbooking) or by customer request. Code is presented instead of designation for anonymity reasons
- booking_changes : Number of changes/amendments made to the booking from the moment the booking was entered on the PMS until the moment of check-in or cancellation
- deposit_type :  Indication on if the customer made a deposit to guarantee the booking. This variable can assume three categories: 
    - No Deposit : no deposit was made or  no payments were found 
    - Non Refund : a deposit was made in the value of the total stay cost 
    - Refundable : a deposit was made with a value under the total cost of stay.
- agent :  ID of the travel agency that made the bookinga
- company :  ID of the company/entity that made the booking or responsible for paying the booking. ID is presented instead of designation for anonymity reasons
- days_in_waiting_list :  Number of days the booking was in the waiting list before it was confirmed to the customer
- customer_type : Type of booking, assuming one of four categories: 
    - BO and BL Contract : when the booking has an allotment or other type of contract associated to it
    - Group : when the booking is associated to a group 
    - Transient : when the booking is not part of a group or contract, and is not associated to other transient booking
    - Transient-party : when the booking is transient, but is associated to at least other transient booking
- adr : ( Average Daily Rate) Calculated by dividing the sum of all lodging transactions by the total number of staying nights
- required_car_parking_spaces : Number of previous bookings that were cancelled by the customer prior to the current booking
- total_of_special_requests : Number of special requests made by the customer (e.g. twin bed or high floor)
- reservation_status : Reservation last status, assuming one of three categories: 
    - Canceled : booking was canceled by the customer 
    - Check-Out : customer has checked in but already departed 
    - No-Show : customer did not check-in and did inform the hotel of the reason why
- reservation_status_date :  Date at which the last status was set. This variable can be used in conjunction with the -Reservation_Status to understand when was the booking canceled or when did the customer checked-out of the hotel
- name : Name of the Guest (Not Real)
- email : Credit Card Number (not Real)
- phone-number :Phone number (not real)
- credit_card : Credit Card Number (not Real)

# Summary EDA
- Terdapat kolom yang masih dengan tipe data yang kurang sesuai.
*Meski bukan masalah besar karena perbedaannya adalah yang semula float64 akan kami ubah menjadi int64*
- Tidak terdapat duplikat di dataset kami namun masih ada kolom yang kosong. Handling null value atau kolom kosong akan dilakukan di tahap selanjutnya 
*so stay tune:)
- Kami menemukan beberapa keanehan pada summary dataset kami. Handling keanehan-keanehan tersebut akan di lakukan di tahap selanjutnya. 

# Summary Data Preprocessing
- Drop null value di kolom ‘children’ : ada 4 baris yang di drop. Sehingga dataset memiliki 119386 entries
- Drop kolom ‘company’ & ‘agent‘
- Mengisi missing values di kolom ‘country’ dengan mode 
- Mengubah minus value di kolom 'adr' menjadi nol (0)
- Handle Outlier pada fitur 'adr' menggunakan ZScore
- Strategi encoding
    - Hotel, origin_type : label encoding
    - meal, market_segment, distribution_channel, deposit_type, customer_type, season : One Hot Encoding
Kolom 'meal', 'market_segment', 'distribution_channel', 'deposit_type', 'customer_type', 'season' akan di drop karena di-encoding dengan One Hot Encoding.
Kolom ‘season’ dan ‘origin_type’ adalah kolom baru yang dibuat di tahap Feature Engineering
- Perbandingan antar kelas fitur target (is_canceled) masih dalam proporsi yang seimbang dan belum masuk kategori imbalance. Jadi tidak perlu melakukan undersampling atau oversampling
- Beberapa kolom yang memiliki redundan (korelasi antar fitur > 0.70) akan didrop, yaitu :
    - arrival_date_year dengan reservation status_date (kedua nya akan didrop)
    - arrival date week juga akan di drop
    - reservation_status akan didrop
    - market_segment_direct dengan distribution_channel_direct (akan di drop salah satu, yaitu distribution_channel_direct)
    - distribution_channelTA/TO dengan market_segment_direct (distribution_channelTA/TO akan di drop)
    - customer_type_Transient dengan customer_type_Transient-Party (customer_type_Transient-Party akan didrop)
    - deposit_type_No Deposit dengan deposit_type_Non Refund (deposit_type_Non Refund akan didrop)
    - sisanya kolom - kolom yang outdated akan di drop (kolom yang sudah dilakukan transformasi)
- Jadi kolom akhir yang akan digunakan adalah 
'hotel', 'is_canceled', 'arrival_date_week_number', 'arrival_date_day_of_month', 'stays_in_weekend_nights', 'stays_in_week_nights', 'adults', 'children', 'babies', 'country', 'is_repeated_guest', 'previous_cancellations', 'previous_bookings_not_canceled', 'booking_changes', 'days_in_waiting_list', 'required_car_parking_spaces', 'lead_time_norm', 'adr_norm', 'total_of_special_requests_norm', 'meal_BB', 'meal_FB', 'meal_HB', 'meal_SC', 'meal_Undefined', 'market_segment_Aviation', 'market_segment_Complementary', 'market_segment_Corporate', 'market_segment_Direct', 'market_segment_Groups', 'market_segment_Offline TA/TO', 'market_segment_Online TA', 'distribution_channel_Corporate', 'distribution_channel_GDS', 'deposit_type_No Deposit', 'deposit_type_Refundable', 'customer_type_Contract', 'customer_type_Group', 'customer_type_Transient', 'reserved_vs_assigned', 'season', 'season_autumn', 'season_spring', 'season_summer', 'season_winter', 'origin_type'
- Fitur tambahan yang sekiranya bisa ditambah untuk pemodelan di masa depan adalah weather, tags, rating, tipe kasur, price of 2 people

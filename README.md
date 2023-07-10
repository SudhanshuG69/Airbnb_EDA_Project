<h1 align = 'center'> Airbnb Data Analysis </h1>

![ ](https://daoinsights.com/wp-content/uploads/2020/12/Hacker-Noon-.png)

# About Data set:

Airbnb, Inc is an American company that operates an online marketplace for lodging, primarily homestays for vacation rentals, and tourism activities. Based in San Francisco, California, the platform is accessible via a website and mobile app. Airbnb does not own any of the listed properties; instead, it profits by receiving commission from each booking. The company was founded in 2008. Airbnb is a shortened version of its original name, AirBedandBreakfast.com.

Since 2008, guests and hosts have used Airbnb to travel in a more unique, personalized way. As part of the Airbnb Inside initiative, this dataset describes the listing activity of homestays in New York City

[Kaggle link](https://www.kaggle.com/datasets/arianazmoudeh/airbnbopendata)

# Data Dictionary
Data dictionaries are used to provide detailed information about the contents of a dataset or database, such as the names of measured variables, their data types or formats, and text descriptions. A data dictionary provides a concise guide to understanding and using the data.

**id:** Airbnb's unique identifier for the listing.

**NAME:** The name or title of the listing.

**host id:** Airbnb's unique identifier for the host/user of the listing.

**host name:** The name of the host, usually just the first name(s).

**neighbourhood group:** The geocoded neighborhood group based on latitude and longitude, using open or public digital shapefiles.

**neighbourhood:** The neighborhood where the listing is located.

**latitude:** The latitude coordinate of the listing's location using the WGS84 projection.

**longitude:** The longitude coordinate of the listing's location using the WGS84 projection.

**country:** The country where the listing is located.

**country code:** The country code of the listing's location.

**instant_bookable:** Indicates whether the guest can automatically book the listing without the host requiring to accept their booking request (true/false).

**cancellation_policy:** The policy set by the host for cancellations.

**room_type:** The type of room or accommodation available (e.g., Entire home/apt, Private room, Shared room, Hotel).

**Construction year:** The year when the property was constructed.

**price:** The daily price of the listing in the local currency.

**service fee:** The additional fee charged for the service.

**minimum_nights:** The minimum number of nights required for booking the listing.

**number_of_reviews:** The total number of reviews the listing has received.

**last_review:** The date of the last/newest review.

**reviews_per_month:** The average number of reviews per month for the listing.

**availability_365:** The number of days the listing is available for booking within the next 365 days.

**house_rules:** The rules set by the host for guests staying at the listing.

**license:** The license/permit/registration number associated with the listing.

**Check out :-**

[Notebook](https://github.com/SudhanshuG69/Airbnb_EDA_Project/blob/eb318220f78ea2648b534e7a04cfba5cf482ca55/Airbnb_data_analysis_EDA-project%20.ipynb)<br>
[Power BI Dashboard Pbix File](https://github.com/SudhanshuG69/Airbnb_EDA_Project/blob/eb318220f78ea2648b534e7a04cfba5cf482ca55/Airbnb_Dashboard.pbix)<br>

## Airbnb's Analysis
<img width = "845" alt = "D1" src = "https://github.com/SudhanshuG69/Airbnb_EDA_Project/assets/128242327/bf18908b-ef08-4bad-b619-18a6fad31462">

## Location Analysis
<img width = "845" alt = "D1" src = "https://github.com/SudhanshuG69/Airbnb_EDA_Project/assets/128242327/35a458b1-2e73-4131-9134-709669ee1ce1">
<img width = "845" alt = "D1" src = "https://github.com/SudhanshuG69/Airbnb_EDA_Project/assets/128242327/10b835cb-4b39-4ac9-962f-2174f1aaffe7">

## Time-Series Analysis
<img width = "845" alt = "D1" src= "https://github.com/SudhanshuG69/Airbnb_EDA_Project/assets/128242327/b65eac4d-aabc-46db-84c3-0a89c721344a">
# Data Understanding
- Here we have a DataFrame with 102,599 rows and 26 columns.

- We have identified the presence of null values in various columns of the DataFrame.

- In the 'minimum nights' column, there are outliers such as a minimum value of -1223 and a maximum value of 5645. These extreme values could be potential errors or data entry issues that need to be investigated further.

- Similarly, in the 'availability 365' column, there is a negative value of -10, which seems incorrect since availability should typically be a positive value representing the number of days an accommodation is available. It would be necessary to examine and address this issue to ensure data integrity.

- To handle null values in different columns, we will apply appropriate methods such as dropping rows/columns, imputing missing values, or ignoring irrelevant columns.

- To correct wrong data types in different columns, we will perform data type conversion using pandas functions.

# Data Cleaning Description
- Create a Woking_df with all the essential columns we requried for analysis.

- "id" which is our "Primary Key" columns has duplicates. so we drop all the duplicated values .

- "Host_identify_verified" has 289 null Values and 2 unique value i.e 'unconfirmed' And 'confirmed'. Assuming that the null values host are unconfirmed ones, we replace the null values with "unconfirmed".

- "Neighbourhood Group((States))" has 29 null values. We find the Neighbourhood((Cites)) w.r.t to each Null Neighbourhood Group and for that city we find the states they are belongings to and replace the null values with the corresponding states.

- "Neighbourhood" has 16 Null values. For this we follow the same approch of finding the stastes w.r.t them and then replace it with the highest repeated values. Both "Lat" and "Long" has 8 null values for the same index number. we took and the cities w.r.t to the null values and find their corresponding lat and long . once we get the values we replace the null values with them.

- "Intant_bookable" has 105 null values and the column contains only boolean values. We corelate "Instant_bookable" with "Minimum Nights" in a way that the airbnb having high mininum nights values are prebooked and has less chances to available for instant booking. For most of the null values the minimum night is less than 30. So we replace the null values in this with "False" .

- "Cancellation Policy" has 76 null values and 3 unique values i.e "Moderate","Strict", & "Flexible". We find the instant booking feature values wrt to 76 null values and find out that for all values "Instant Booking" is False. Then we find out that for "False" instant booking moslty the cancellation properties are "moderate" , so we replace the null values with the "moderate".

- "Construction Year" has 214 null values. We replace all the null values with "Not Available".

- "Service Fee" has 273 null values. we replace all the null values with Mean value of "service fee"

- "Price" has 214 null values. we replace all the null values with Mean value of "price".

- "Minimum Nights" has 409 null values. We replace null values with mode of minimum nights i.e 1.

- "Number of Reviews" has 183 null values. we replace all the null values with "Median" value of reviews as it a highly skewed data and in such data it's advised to replace null with median.

- "Last review" has 15893 null values and the only column which we can use for datetime analysis. we use interpolation method to replace all the null values in it. To treat the null values of date columns "interpolation" is good technique to used.

- "Review Per month" 15879 null values . We replace the null values the mean value of the field.

# Conlusion
**Manhattan is the most popular neighborhood on Airbnb, followed by Brooklyn.**

**Bedford-Stuyvesant has the highest number of Airbnb listings, while Williamsburg is the second highest.**

**There is a strong positive correlation (1) between the price of listings and the associated service fees.**

**A moderate positive correlation (0.59) exists between the number of reviews a listing has received and the average number of reviews per month.**

**The highest average prices were observed between 2012 and 2014, followed by a significant decrease after 2014.**

**The most prevalent property type in Manhattan is the entire room/apartment, while private rooms are more common in Brooklyn.**

**The pricing of listings depends on factors such as room type, neighborhood, and minimum number of bookings.**

**There are 102,052 unique host IDs for the given reviews, with one host (ID: 20032806094) having the highest average reviews per month at 90.00. The top two neighborhood groups based on reviews per month are Brooklyn (46,866.76) and Manhattan (45,222.96), while the top two neighborhood groups based on the number of reviews are Brooklyn (1,189,991.0) and Manhattan (1,050,741.0).**

**Hotel rooms tend to be more expensive than apartment or house rentals.**

**Certain neighborhoods like "New Dorp," "Fort Wadsworth," and "Chelsea, Staten Island" have higher Airbnb rates compared to "Rossville," "Spuyten Duyvil," and "Lighthouse Hill."**

**Listings with a minimum booking requirement of more than a year generally have higher prices.**

**Approximately 49.7% of customers use Instant booking, while 50.3% do not.**

**The cancellation policy distribution shows that 33.5% have a moderate policy, and 33.2% have either strict or flexible policies.**

**The highest value counts for construction year occur in 2014, while the minimum counts are in 2016.**

**The most popular property type is "Home away from home," followed by "Hillside Hotel."**


**Among hosts, the most popular name is Michael, followed by David.**



# Message to stackholder:

- **Manhattan is the most popular neighborhood on Airbnb, followed by Brooklyn. Bedford-Stuyvesant has the highest number of listings, while Williamsburg is the second highest.**
- **Prices of listings have a strong positive correlation with service fees, indicating higher-priced listings tend to have higher associated fees.**
- **Listings with more reviews tend to receive a higher average number of reviews per month, indicating popular listings attract ongoing attention from guests.**
- **The highest average prices were observed between 2012 and 2014, followed by a significant decrease after 2014.**
- **The most prevalent property type in Manhattan is the entire room/apartment, while private rooms are more common in Brooklyn.**

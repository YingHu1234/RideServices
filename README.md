# RideServices

<p align="center">
  <a href="" rel="noopener">
 <img width=200px height=200px src="https://i.imgur.com/6wj0hh6.jpg" alt="Project logo"></a>
</p>

<h3 align="center">:zap: :rocket: Ride Services analysis </h3>


---

<p align="center">
Find insights from the dataset for ride service. 
    <br> 
</p>

## 📝 Table of Contents
- [About](#about)
- [Data Clearning](#data_leaning)
- [General Picture](#GeneralPicture)
- [Other  Insights ](#OtherInsights)
- [Conclusion](#conclusion)


## 🧐 About <a name = "about"></a>
Understand the dataset, estimate the charged rate, identify patterns, and determine the best locations for drivers to pick up customers to achieve a higher charge rate.

<img src="https://media1.giphy.com/media/v1.Y2lkPTc5MGI3NjExenp5NnVnMmdrczF1enJuOTlzMWdncWw3d2p2dWtkamh6bTg0am1ydiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/CnQ6jjqggL2Ar23XtQ/giphy.gif" width="450" />

### Prerequisites
SQL, Tableau, Python or Jupyter Notebook 


## 🔖 Data Cleaning <a name = "data_leaning"></a>

Basic information of the dataset (please refer to Appendices on the page 10, 11 and 12)

    a.	Original record: 1337759 rows, 20 columns
  
    b.	Data: continuous data (regression models)
  
    c.	Duplicates: No duplicates
  
    d.	Outliners: 17997 rows were removed
  
        i.	Three rows (RateCodeID=99, which were not explained on the data dictionary)
        ii.	17994 rows (Trip distance was 0, but the fare amount was more than $100)
    e.	Null values: 1337759 counts on the “Ehail_fee” column.
    
        i.	The null values were updated into 0 
        
    f.	Final record: 1319765 rows, 20 columns

Tools were used for this project: Python, MySQL, and Tableau

    a.	Viewed the dataset and imported it into Mysql: Python 
    
    b.	Data cleaning and queries: Mysql
    
    c.	Data analysis and visualization: Tableau


![image](https://github.com/YingHu1234/RideServices/blob/main/RideService/12.png)
![image](https://github.com/YingHu1234/RideServices/blob/main/RideService/13.png)
![image](https://github.com/YingHu1234/RideServices/blob/main/RideService/14.png)
![image](https://github.com/YingHu1234/RideServices/blob/main/RideService/15.png)


## 🌱 General Picture <a name = "GeneralPicture)"></a> 


1.	Which vendor had the most trips? How many trips were taken?

    Vendor #2 VeriFone Inc had the most and 1036551 were taken. 
    (Please refer to the below screenshot)
  	
    ![image](https://github.com/YingHu1234/RideServices/blob/main/RideService/1.png)
   
     
3.	Please pull the records with the highest fare or passenger_count by date (day)’

    Please refer to the below screenshot:
  	
     ![image](https://github.com/YingHu1234/RideServices/blob/main/RideService/2.png)


4.	Estimate the charged rate for each RateCodeID. (For this question, assume rates are only charged based on distance. )

    •	Forecast model is applied to predict the charged rate
  	
    •	It is for the next week from July 1st, 2014, to July 12th, 2014.
  	
    •	The orange/red line is the trend of the charged rate. Please refer to the below screenshot:
  	
    ![image](https://github.com/YingHu1234/RideServices/blob/main/RideService/3.png)


6.	What was the average difference between the driven distance and the haversine distance of the trip?

    The average difference was 8 miles:
  	
        •	Calculations for two points: Pickup point & Dropoff point
  	
              o	Pickup Point=MAKEPOINT([Pickup latitude],[Pickup longitude])
              o	Dropoff point=MAKEPOINT([Dropoff latitude],[Dropoff longitude])
  	
        •	Calculation for Haversine distance: 15,185,531 miles.
  	
              o	Haversine distance=Distance([Pickup Point],[Dropoff Point],'mi')
  	
        •	Average difference calculation: 8 miles
  	
              o	AVG([Haversine distance]-[Trip distance])
  	
        •	Please refer to the below screenshot

   ![image](https://github.com/YingHu1234/RideServices/blob/main/RideService/4.png)


  5.	Are there any patterns with tipping over time? If you find one, please provide a possible explanation!

      These Patterns are based on the trip type #1 Street-hail:
      
           1.	The tipping rate has weekly seasonality:
           
                o	Every week, the tipping rate is slowly going up from Monday to Saturday, and Saturday has the highest tipping rate, then it goes down slowly to the bottom on Monday. 
      
           2.	There is the highest tipping rate from Saturday at 11:00 PM to Sunday at 00:00 AM:
           
                o	The reason of the tipping rate has a significant jump on the Saturday and Sunday:
                    	Friends and family gatherings, trips, church, etc. 

     ![image](https://github.com/YingHu1234/RideServices/blob/main/RideService/5.png)
     ![image](https://github.com/YingHu1234/RideServices/blob/main/RideService/6.png)


  6.	Can you predict the length of the trip based on factors that are known at pick-up? How might you use this information?

        Yes, the length of the trip would be predicted:
    	
              •	Trip time calculation for the data from each trip
    	
                    o	DATEDIFF ('hour',[Lpep Pickup Datetime],[Lpep_dropoff_datetime])
    	
              •	Trip time and trip distance data were applied to the Quantile model
    	
                    o	MODEL_QUANTILE(0.5, ATTR([trip_time]), ATTR([Trip distance]))
    	
                          For example, the drivers will get the information on the trip distance before they pick up customers. If the distance is around 17.9 miles, the length of the trip                              will be more than an hour, which make sense since the traffic is heavy in New York, and the travel speed also needs to be considered.   (Please refer to the below                              screenshot)

        ![image](https://github.com/YingHu1234/RideServices/blob/main/RideService/7.png)


## 🌽 Other  Insights  <a name = "OtherInsights"></a>

  7.	Get creative! Present any interesting trends, patterns, or predictions that you notice about this dataset.

      The interesting facts are based on:

          Two vendors #1 Creative Mobile Tech (283,214 records) vs #2 VeriFone Inc (1,036,551 records)

          Differences:
          
          •	Vendor #2 VeriFone Inc has more trips than #1 Creative Mobile Tech; however, #1 Creative Mobile Tech has more no charge payments (based on RateCodeID=1 Standard rate charge & 5               Negotiated fare). (Please refer to the below screenshots)


          ![image](https://github.com/YingHu1234/RideServices/blob/main/RideService/8.png)
          ![image](https://github.com/YingHu1234/RideServices/blob/main/RideService/9.png)


          Similarities:

          •	Both vendors show the main customer charge comes from RateCodeID=1 Standard rate fare & 5 Negotiated fare. 
          
          •	Both data sets show the same pattern:
          
              o	There is a weekly seasonality
              
              	The customer charge rate reached the maximum on Saturday and the minimum on Monday.
               
              o	The peak charge rate occurs from Saturday at 11:00 PM to Sunday at 0:00 AM. 
              
              o	Both maps show the same area for more customers and a higher charge rate.

          ![image](https://github.com/YingHu1234/RideServices/blob/main/RideService/10.png)
          ![image](https://github.com/YingHu1234/RideServices/blob/main/RideService/11.png)



  ## 🎉 Conclusion <a name = "conclusion"></a>
  
The best date and hour for a driver to get more businesses and the peak charge rate from customers is from Saturday at 11:00 PM to Sunday at 0:00 AM, and the best locations are the common black area from both maps. (Please refer to the Q7 screenshots)


      
          



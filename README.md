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
- [Result of Classification](#result)
- [Topic_modeling](#topic_modeling)
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


5.	What was the average difference between the driven distance and the haversine distance of the trip?

    The average difference was 8 miles:
        •	Calculations for two points: Pickup point & Dropoff point
              o	Pickup Point=MAKEPOINT([Pickup latitude],[Pickup longitude])
              o	Dropoff point=MAKEPOINT([Dropoff latitude],[Dropoff longitude])
        •	Calculation for Haversine distance: 15,185,531 miles.
              o	Haversine distance=Distance([Pickup Point],[Dropoff Point],'mi')
        •	Average difference calculation: 8 miles
              o	AVG([Haversine distance]-[Trip distance])
        •	Please refer to the below screenshot

   ![image](https://github.com/YingHu1234/RideServices/blob/main/RideService/3.png)

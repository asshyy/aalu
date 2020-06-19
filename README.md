On sincere efforts of - Ashita Bajpai
Dated - 16 th of june 2020 

The Project Work On Data Analysis based on the profiling of yelp data sheet 


In the first part of the assignment u will be taken into the fact that you ask certain queries and answer them as per your choice profiling
and understanding as a data scientist what should be te proper coding and manifestation of what actually needs to be worked out in the most appropriate terms and in the most optimistc way ....


In the second part of the assignment we will be able to analysis the dataset , use the dataset in proper formatting and commenting on the 
worksheet using the appropriate text editor be it subime or any one of those with proper indentation which needs to be taken care of......



1. Yelp dataet profiling & interpretation;

1.Finding out the total no of records held in the table :
             SELECT COUNT(*)
             FROM table
    1.     Attribute table=10000
    2.   Business table=10000
    3.   Category table=10000
    4.   Checkin table=10000
    5.     elite_years table=10000
    6.   friend table=10000
    7.   hours table=100008
    8.   photo table=10000
    9.   review table=10000
    10.     tip table=10000
    11.  user table=10000
             
2.    List the cities with most reviews in ascending ordr:

 Sql code used to arrive at it are :
     SELECT city,
               SUM(review_count)AS reviews
     FROM business
     GOUP BY city
     ORDER BY reviews DESC
     
    The results are as listed :(Witten only first 5 for reference)
    
         city               review
         Las Vegas          82854
         Phoenix            34503
         Toronto            24113
         Scottsdale         20164
         Charlotte          12523
         
  Part 2: Inferences & analysis
  Group business based on the ones that are open andthe ones that are closed.What differences can you find between the ones that are still open and the ones that are closed? list at least 2 diffrences and the sql code toarrive at ur answer .
  
  
  1. Difference 1:
  
     The business that are open tend to have more reviews than ones that are closed on average.
         Open: AVG(review_count)=31.757
         Closd:AVG(review_count)=23.198
         
  2. Difference 2:
  
     The average star rating is higher for usiness that are open than business that are closed..
     
     Open: AVG(stars)=3.679
     Closed:AVG(srars)=3.520
     
     Sql code for analyis :
     SELECT COUNT(DISTINCT(id)),
           AVG(review_count),
           SUM(revew_count),
           AVG(stars),
           is_open
     FROM business
     GROUP BY is_open
     
     
Part 3:For the last part of the yelp data analysis to check whether a business should be open or close

1. In this case we will examine a business should be open or close.

2.
  in this part we will see the location what are the factors which come into existence, the city the state, postal_code,and address to make processing easier later on also i need t clarifty that is_open clarify business i open and which business have closed(not hours)bt permanently.
  
  
  
3. Considering the output of the yelp data set: (As a sample taken)
name                       address                             city         
Flaming Kitchen            3235 York Regional Road             Markham
Freeman's Car Stereo       4831 Suth Blvd                     Charlotte

SELECT B.id,
           B.name,
           B.address,
           B.city,
           B.state,
           B.postal_code,
           B.latitude,
           B.review_count,
           B.stars,
           MAX(CASE
           WHEN H.hours LIKE"%monday%" THEN TRIM(H.hours,'%TuesWednesThursFriSatSun|%')
           END) AS monday_hours,
           GROUP_CONCAT(DISTINCT(CCategory))AS categories,
           GROUP_CONCAT(DISTINCT(A.name) AS attributes,
           B.is_open
     FROM business B
     INNER JOIN hours H
     On B.id=H.business_id
     INNER JIN category C 
     On B.id=C.business_id
     INNER JOIN attribute A
     ON B.id=A.business_id
     GROUP BY B.id
 

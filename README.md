# NoSQL Challenge

## Instructions

The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating. You've been contracted by the editors of a food magazine, _Eat Safe, Love_, to evaluate some of the ratings data to help their journalists and food critics decide where to focus future articles.

### Part 1: Database and Jupyter Notebook Setup

Use code file NoSQL_setup.ipynb for this section of the challenge.

1. Import the data provided in the establishments.json file from your Terminal. Name the database uk_food and the collection establishments. Copy the text you used to import your data from your Terminal to a markdown cell in your notebook.
2. Within your notebook, import the libraries you need: PyMongo and Pretty Print (pprint).
3. Create an instance of the Mongo Client.
4. Confirm that you created the database and loaded the data properly:
    * List the databases you have in MongoDB. Confirm that uk_food is listed.
    * List the collection(s) in the database to ensure that establishments is there.
    * Find and display one document in the establishments collection using find_one and display with pprint.
5. Assign the establishments collection to a variable to prepare the collection for use.


_Part 1 Code and Output Screenshots_
![Screenshot 2025-01-19 at 21 56 39](https://github.com/user-attachments/assets/55422d3e-a703-4250-9c67-a6d3da4a763b)


### Part 2: Update the Database

Use code file NoSQL_setup.ipynb for this section of the challenge.

The magazine editors have some requested modifications for the database before you can perform any queries or analysis for them. Make the following changes to the establishments collection:
1. An exciting new halal restaurant just opened in Greenwich, but hasn't been rated yet. The magazine has asked you to include it in your analysis. Add the following information to the database:

   ```
   {
       "BusinessName":"Penang Flavours",
       "BusinessType":"Restaurant/Cafe/Canteen",
       "BusinessTypeID":"",
       "AddressLine1":"Penang Flavours",
       "AddressLine2":"146A Plumstead Rd",
       "AddressLine3":"London",
       "AddressLine4":"",
       "PostCode":"SE18 7DY",
       "Phone":"",
       "LocalAuthorityCode":"511",
       "LocalAuthorityName":"Greenwich",
       "LocalAuthorityWebSite":"http://www.royalgreenwich.gov.uk",
       "LocalAuthorityEmailAddress":"health@royalgreenwich.gov.uk",
       "scores":{
           "Hygiene":"",
           "Structural":"",
           "ConfidenceInManagement":""
       },
       "SchemeType":"FHRS",
       "geocode":{
           "longitude":"0.08384000",
           "latitude":"51.49014200"
       },
       "RightToReply":"",
       "Distance":4623.9723280747176,
       "NewRatingPending":True
   }
   ```

3. Find the BusinessTypeID for "Restaurant/Cafe/Canteen" and return only the BusinessTypeID and BusinessType fields.
4. Update the new restaurant with the BusinessTypeID you found.
5. The magazine is not interested in any establishments in Dover, so check how many documents contain the Dover Local Authority. Next, remove any establishments within the Dover Local Authority from the database, and check the number of documents to ensure they were deleted.
6. Some of the number values are stored as strings, when they should be stored as numbers.
    * Use update_many to convert latitude and longitude to decimal numbers.
    * Use update_many to convert RatingValue to integer numbers.

_Part 2 Code and Output Screenshots_
![Screenshot 2025-01-19 at 21 57 35](https://github.com/user-attachments/assets/69c4b2fd-9b8a-45d5-bd0c-9e4e9fbf720c)
![Screenshot 2025-01-19 at 21 57 54](https://github.com/user-attachments/assets/5815fc7b-8b0d-451f-a667-e804fc46eff5)
![Screenshot 2025-01-19 at 21 58 09](https://github.com/user-attachments/assets/77eff687-e5f1-42a2-b02d-272427e1202d)
![Screenshot 2025-01-19 at 21 58 34](https://github.com/user-attachments/assets/4b2d72c8-27fa-4691-b7ba-bcbbddb0ff0c)
![Screenshot 2025-01-19 at 21 58 51](https://github.com/user-attachments/assets/11336a22-d0a2-4dff-a669-c00aef2d7a9d)


### Part 3: Exploratory Analysis

_Eat Safe, Love_ has specific questions they want you to answer, which will help them find the locations they wish to visit and avoid.

Use code file NoSQL_analysis.ipynb for this section of the challenge.

Note:
* RatingValue refers to the overall rating decided by the Food Authority and ranges from 1-5. The higher the value, the better the rating. (This field also includes non-numeric values such as 'Pass', where 'Pass' means that the establishment passed their inspection but isn't given a number rating. We coerce non-numeric values to nulls during the database setup before converting ratings to integers.)
* The scores for Hygiene, Structural, and ConfidenceInManagement work in reverse: the higher the value, the worse the establishment is in these areas.

Use the following questions to explore the database, and find the answers, so you can provide them to the magazine editors.

Unless otherwise stated, for each question:
* Use count_documents to display the number of documents contained in the result.
* Display the first document in the results using pprint.
* Convert the result to a Pandas DataFrame, print the number of rows in the DataFrame, and display the first 10 rows.

1. Which establishments have a hygiene score equal to 20?
2. Which establishments in London have a RatingValue greater than or equal to 4?
  Hint: The London Local Authority has a longer name than "London" so use $regex as part of search.
3. What are the top 5 establishments with a RatingValue of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?
  Hint: Compare the geocode to find the nearest locations. Search within 0.01 degree on either side of the latitude and longitude.
4. How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to lowest, and print out the top ten local authority areas.
  Hint: Use the aggregation method.
  The first 5 rows of the resulting DataFrame should look something like this:
  ![Screenshot 2025-01-13 at 19 33 30](https://github.com/user-attachments/assets/ac5e6099-3a56-4815-a538-83a7daeddebb)

_Part 3 Code and Output Screenshots - Analyses only, screenshots truncate outputs for brevity_
![Screenshot 2025-01-19 at 22 06 37](https://github.com/user-attachments/assets/af330139-c4ed-4d35-b4a9-79150e58b44f)
![Screenshot 2025-01-19 at 22 06 56](https://github.com/user-attachments/assets/72ac7312-3e35-40b2-8d27-0f4a28e1001c)
![Screenshot 2025-01-19 at 22 07 48](https://github.com/user-attachments/assets/23e48e27-400b-482d-91a8-2b0675e38813)
![Screenshot 2025-01-19 at 22 08 15](https://github.com/user-attachments/assets/e6e8e176-77da-4b8a-b5d1-060e357a9549)
![Screenshot 2025-01-19 at 22 08 26](https://github.com/user-attachments/assets/94ad313f-d42c-4c4a-a2b8-b1e892fa8b15)


## Acknowledgements

UK Food Standards Agency (2022). UK food hygiene rating data API. https://ratings.food.gov.uk/open-data/en-GB. Contains public-sector information licensed under the Open Government Licence v3.0.
Accessed Sept 9, 2022 and Sept 12, 2022 with the establishment settings as follows: longitude=51.5072, latitude=-0.1276, maxdistancelimit=4567, pagesize=10000, sortoptionkey=distance, pagenumber=(1,2,3,4,5,6,7,8).


# NoSQL Challenge

## Instructions

The UK Food Standards Agency evaluates various establishments across the United Kingdom, and gives them a food hygiene rating. You've been contracted by the editors of a food magazine, _Eat Safe, Love_, to evaluate some of the ratings data to help their journalists and food critics decide where to focus future articles.

### Part 1: Database and Jupyter Notebook Setup

Use NoSQL_setup_starter.ipynb for this section of the challenge.
1. Import the data provided in the establishments.json file from your Terminal. Name the database uk_food and the collection establishments. Copy the text you used to import your data from your Terminal to a markdown cell in your notebook.
2. Within your notebook, import the libraries you need: PyMongo and Pretty Print (pprint).
3. Create an instance of the Mongo Client.
4. Confirm that you created the database and loaded the data properly:
    * List the databases you have in MongoDB. Confirm that uk_food is listed.
    * List the collection(s) in the database to ensure that establishments is there.
    * Find and display one document in the establishments collection using find_one and display with pprint.
5. Assign the establishments collection to a variable to prepare the collection for use.

### Part 2: Update the Database

Use NoSQL_setup_starter.ipynb for this section of the challenge.

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

### Part 3: Exploratory Analysis

_Eat Safe, Love_ has specific questions they want you to answer, which will help them find the locations they wish to visit and avoid.

Use NoSQL_analysis_starter.ipynb for this section of the challenge.

Some notes to be aware of while you are exploring the dataset:
* RatingValue refers to the overall rating decided by the Food Authority and ranges from 1-5. The higher the value, the better the rating.
  * Note: This field also includes non-numeric values such as 'Pass', where 'Pass' means that the establishment passed their inspection but isn't given a number rating. We will coerce non-numeric values to nulls during the database setup before converting ratings to integers.
* The scores for Hygiene, Structural, and ConfidenceInManagement work in reverse. Thus, the higher the value, the worse the establishment is in these areas.

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

## Acknowledgements

UK Food Standards Agency (2022). UK food hygiene rating data API. https://ratings.food.gov.uk/open-data/en-GB. Contains public-sector information licensed under the Open Government Licence v3.0.
Accessed Sept 9, 2022 and Sept 12, 2022 with the establishment settings as follows: longitude=51.5072, latitude=-0.1276, maxdistancelimit=4567, pagesize=10000, sortoptionkey=distance, pagenumber=(1,2,3,4,5,6,7,8).


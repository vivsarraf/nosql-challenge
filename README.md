# nosql-challenge Module-12


### Scenario

Using data obtained from the [UK Food Standards Agency](https://www.food.gov.uk/), create a NoSQL database in MongoDB, import the data and use the PyMongo module to complete additional tasks.

The challenge is split into three sections:

- Create the database and form a connection to the database and collection in a Jupyter Notebook.
- Update certain records and fields within the database collection.
- Perform some exploratory analysis on the documents within the database.

------

### [Database and Collection Creation](uk-food-agency/NoSQL_setup.ipynb)

Create, and import the data into, the database. Followed by connecting to the MongoDB a Jupyter Notebook and PyMongo:

- Using the [establishments.json](uk-food-agency/Resources/establishments.json) data file provided, use the 'mongoimport' function in a terminal to create a database named 'uk-food' and a collection 'establishments' to import the documents.
    - ``` mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json ```
- In a jupyter notebook, import the required libraries
    - PyMongo
    - Pretty Print (pprint)
- Create an instance of the Mongo Client.
- Confirm that you created the database and loaded the data properly:
    - List the databases you have in MongoDB. Confirm that 'uk_food' is listed.
    - List the collection(s) in the database to ensure that 'establishments' is there.
    - Find and display one document in the establishments collection using 'find_one' and display with 'pprint'.
- Assign the 'establishments' collection to a variable to prepare the collection for use.

------

### [Update Documents and Field Datatypes](uk-food-agency/NoSQL_setup.ipynb)

Within the jupyter notebook previously created, develop the code to add a new document, update fields, delete un-required documents and alter specific field's datatypes:

- Add a new document for a recently opened restaraunt using the following data:
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
- Find the 'BusinessTypeID' for "Restaurant/Cafe/Canteen" and return only the 'BusinessTypeID' and 'BusinessType' fields.
- Update the new restaurant with the 'BusinessTypeID' you found.
- The magazine is not interested in any establishments in "Dover", so check how many documents contain the "Dover" Local Authority. Then, remove any establishments within the "Dover" Local Authority from the database, and check the number of documents to ensure they were deleted.
- Some of the number values are stored as strings, when they should be stored as numbers.
    - Use 'update_many' to convert 'latitude' and 'longitude' to decimal numbers.
    - Use 'update_many' to convert 'RatingValue' to integer numbers.

------

### [Exploratory Analysis](uk-food-agency/NoSQL_analysis.ipynb)

With the database documents prepared, conduct some exploratory analysis on the database to provide some high level insights:

    For each question, provide the following information, unless stated otherwise (visible within the jupyter notebook):
        - Use 'count_documents' to display the number of documents contained in the result.
        - Display the first document in the results using 'pprint'.
        - Convert the result to a Pandas DataFrame, print the number of rows in the DataFrame, and display the first 10 rows.
    
    I've also output the results for each DataFrame into a CSV format for ease of access and distribution of the data.

- Which establishments have a hygiene score equal to 20?
    - CSV Output - [hygiene](uk-food-agency/csv_outputs/hygiene_df.csv)
- Which establishments in "London" have a 'RatingValue' greater than or equal to 4?
    - CSV Output - [london_rating](uk-food-agency/csv_outputs/london_rating.csv)
- What are the top 5 establishments with a 'RatingValue' of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?
    - CSV Output - [near_penang](uk-food-agency/csv_outputs/near_penang_df.csv)
- How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to lowest, and print out the top ten local authority areas.
    - CSV Output - [aggregate](uk-food-agency/csv_outputs/aggregate_df.csv)

--------

## References

| Reference Name | Description |
|----------------|-------------|
| [UK Food Standards Agency](https://www.food.gov.uk/) | UK food hygiene rating data API. [https://ratings.food.gov.uk/open-data/en-GB](https://ratings.food.gov.uk/open-data/en-GB).<br/> *Accessed Sept 9, 2022 and Sept 12, 2022 with the establishment settings as follows: longitude=51.5072, latitude=-0.1276, maxdistancelimit=4567, pagesize=10000, sortoptionkey=distance, pagenumber=(1,2,3,4,5,6,7,8)*.  |
| edX Boot Camps LLC | Obtaining the data/resources and developing the assignment instructions and starter files. |
| [StackOverflow - pd.json_normalize()](https://stackoverflow.com/a/40401365/21871037) | Code/Details on how to convert MongoDB into a flat pandas DataFrame |


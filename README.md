# Final Project: Build an AI Enriched Corporate Training Catalog

## Problem Definition

The company provides training opportunities for technical staff using a combination of internal and external sources. The company is a Microsoft Gold Certified Partner and also engages with Udacity to provide external training. In addition, the company maintains a library of select open-access journal articles relevant to their work and also provides their own internal Moodle site for training.

Currently, employees are having a hard time sifting through the disparate sources of training in order to find the right resource and HR has a plan to incorporate even more opportunities for the staff. To help people find the resources that are best for them, the company has decided to build an Azure Cognitive Search solution.

The company wants users to be able to search Course Data by keywords and phrases from descriptions and other fields and return meaningful results. In addition, the company wants users to be able to filter results based on relevant criteria such as course ratings or duration. The company has profiles for each of the course instructors for their own internal training and would like to have those returned in the search results even though they are not currently in the database. The company would like users to be able to facet information based on relevant fields such as source, skills, or role. Finally, the company wants users to be able to sort results by relevant fields.

In addition to the Course Data, the company wants to make available a curated set of open access journal articles in PDF form that are related to their big data work. These articles should be searchable by keywords and phrases, authors, and their associated institutions. In addition, the company wants users to be able to search using publication name, publisher, and publication date. Users should be provided the DOI (Digital Object Identifier) URL for the file as part of the search result.

The data available from each data source is outlined below:

### Course Data

* Title
* Description
* Duration
* Source [MS, Udacity, Internal]
* Type [Module, Nanodegree, Internal]
* Level
* Role
* Technology
* Popularity
* Rating
* Rating Count
* Url
* Review (Only for internal courses)
* Instructor (Only for internal courses)


### Curated Library

* Set of curated PDF articles


## Instructions

### General Submission Instructions

For most of the steps along the way, you will create a file: an image, a screenshot, a JSON file etc. You will label these according to the instructions and save them locally. When you are ready to submit your project, you will zip all of these files into a single submission zip file and upload them.

For at least one step, you will modify code that is in a GitHub repository. To submit those modifications, you will fork the repo, push your code changes and submit the URL for review.

Each step will include specific submission instructions so pay close attention.

### Instructions Summary

The project will follow the four steps outlined below:

* Design: For this step, you will think through the design and create a diagram as well as a list of specific requirements based on the project narrative.
* Import Data: For this step, you will log into the Azure Portal and import data from different data sources into Azure Cognitive Search. You will also demonstrate search queries based on this data.
* Enrichments: For this step, you will add additional enrichments to the data and demonstrate these using queries.
* Deployment: For this step, you will connect a simple search page to your Azure Cognitive Search solution so end users can have a user-friendly means of mining the data.

#### Step 1 Design

For this step, you will think through the design and create a a diagram as well as a list of specific requirements based on the project narrative. These requirements are what you might anticipate being asked to create at the beginning of a project and will require you to thoughtfully consider the goals of the project.

##### Architectural Diagram

Using your favorite diagramming tool, create a high-level architectural diagram of the system to be built. Assume two different data sources in Azure, and assume the final user interface is an Azure Static Web App.

You may use free tools such as Draw.io or Lucid Chart to complete this step if you would like.

##### Requirements

Make a detailed list of requirements for this solution based on the narrative provided in the Project Overview. You should read through the narrative and extrapolate specific requirements to build out in Azure Cognitive Search. These requirements should reflect what you learned about searching, filtering, faceting, and sorting. In addition, these requirements should include information related to data enrichments required (see the list of data elements in the Overview).

An example of a detailed search requirement might be: **"Users can facet Course Data by role, product, and level."**

An example of a detailed enrichment requirement might be: **"Users can search the Curated Library for papers by journal name."**

Read the Project Narrative carefully and you should be able to capture a dozen or more specific requirements.

##### Submission Materials

* Create a text document with a list of requirements in the form of "Users can...." Name the file "Step1_Requirements" (i.e., Step1_Requirements.docx or Step1_Requirements.txt).
* Save the architectural diagram to an image file or take a screenshot and name it: "Step1_Architecture" (i.e., Step1_Architecture.jpg or Step1_Architecture.png).

#### Step 2: Import Data

For this step, you will first import data from multiple datasets that have already been configured for you to import into your Azure environment, found in the Data folder of the Github repository. Importing data into Azure Cognitive Search creates a tremendous amount of functionality out of the box and by the end of this step, you will already be able to begin searching the data.

During this import step you will set up the initial skills, indexes, and indexers for these datasets. In later steps we will augment these enrichments but for now we will just use skills that come from the import wizard. Once the data are imported and indexes created, you will spend time learning how to query the data using the various features available.

##### Procedure

1. Use the Import data wizard to import each of the two datasets: "courses.csv" and the Library folder containing research papers (For "courses.csv" make sure you select the cognitive services you created, not the free tier. For the research papers, you can use the free tier since we have limited the dataset to only 19 papers.)
2. Select the appropriate enrichments to be added during import (refer back to your design requirements here)
3. Customize your target index based on your design requirements to select the appropriate fields for retrieval, filtering, sorting, faceting, and searching.
4. Using the Search Explorer interface, write query strings demonstrating at minimum the following from each index:
 - Search with correct fields returned from each dataset
 - Filtering, faceting, and sorting from each dataset (as appropriate)

##### Submission Materials

* Save a screenshot of the Data Sources tab in the Azure Portal. Name it: "Step2_Data-Sources"
* Save the Skillset Definition JSON file for each of the data sources and name them: "Step2_Skillset_Courses.json" and "Step2_Skillset_Library.json" respectively.
* Save the Index Definition JSON file for each of the data sources and name them: "Step2_Index_Courses.json" and "Step2_Index_Library.json" respectively.
* Save the Indexer Definition JSON file for each of the data sources and name them: "Step2_Indexer_Courses.json" and "Step2_Indexer_Library.json" respectively.
* Create a text file with at least two search query strings and resulting JSON from your searches. Make sure you have demonstrated the correct fields are returned from each data source based on requirements. Name the file "Step2_Queries".
* Create a text file with a number of search query strings and resulting JSON that demonstrate the different features outlined in the requirements section such as specific filtering, faceting, etc. You should have a minimum of five (5) queries in this file. Name the file "Step2_AdvancedQueries".

#### Step 3: Enrichments

You will now add some additional enrichments to the data. During the previous Import Data step, an initial skillset was created automatically for document cracking and out-of-the-box enrichments. This skillset (along with the index that was created) satisfies most of the user requirements, but now some additional enrichments are needed. You will add these enrichments and then demonstrate them using queries.

Remember from the Project Narrative: "The company has profiles for each of the course instructors for their own internal training and would like to have those returned in the search results even though they are not currently in the database." These profiles are in a JSON document in the GitHub repo called MoodleInstructorProfiles.json. You will use the built-in Custom Entity Lookup skill to enrich the dataset with this information.

Also, remember from the Project Narrative: "In addition the company wants users to be able to search using publication name, publisher, and publication date. Users should be provided the DOI (Digital Object Identifier) URL for the file as part of the search result." You will note that document cracking didn't give you this information in your index, so you will configure and use a custom skill built in an Azure Function to enrich the dataset.

##### Procedure

**Built-in Skill**

1. Modify your skillset definitions to add a built-in skill to enrich the data with descriptive information related to the entities listed in the MoodleInstructorProfiles.json file
1. Modify the index and indexer files to allow this enriched data to be used in queries

**Custom Skill**

1. First we need the credentials for the Springer API. This service is free and allows you to query the Springer API for information about articles in their database.
  * Visit the Springer API page https://dev.springernature.com/ and sign up for credentials (For organization, you can just use "personal")
  * Once you are signed up and signed in, you can visit the "Applications" page and copy your credential for use in the next step

1. Next, you need to deploy the Azure Function:
* From the GitHub starter code, open the "Function" folder in Visual Studio Code
* Modify the SpringerLookup.cs file to include the API key you created in Step #1
* Run the Function App by going to Run & Debug and running. This will restore packages and spin up the function locally. (See note below if you want to test this locally)
* Function inputs and outputs
  - This Function App takes in a single data element named: "ArticleName"
  - The Function App will return the following data elements for each ArticleName:
    - PublicationName
    - Publisher
    - DOI
    - PublicationDate

1. Finally, modify your Azure Cognitive Search to use the Azure Function
   * Modify your skillset definition to add the custom skill to enrich the data by passing the document title to the function
   * Modify the index and indexer files to allow this enriched data to be used in queries

Once you are done with both of the above, make sure you use the Search Explorer interface to write query strings demonstrating the data elements from each of these skills.

##### Submission Materials

* Make a JSON file from each of your skillset definitions. Name them "Step3_Courses_Skillset.json" and "Step3_Library_Skillset.json"
* Make a JSON file from each of your index definitions. Name them "Step3_Courses_Index.json" and "Step3_Library_Index.json"
* Make a JSON file from each of your indexer definitions. Name them "Step3_Courses_Indexer.json" and "Step3_Library_Indexer.json"
* Check-in your changes to the GitHub repo that contain your modified configuration for the Azure Function
* Create a text file with a number of search query strings and resulting JSON that demonstrate the different features outlined in the requirements section such as specific filtering, faceting, etc. You should have a minimum of five (5) queries in this file. Name the file "Step3_AdvancedQueries".

**Note: Optional Local Function Testing**

Azure Functions developed in Visual Studio Code can be run and tested locally. If you would like to try this, follow the instructions above to run the Function App locally and then use the procedure below to test.

* Download your favorite REST client (i.e., Postman or Advanced REST Client)
* Compose a POST message using the URL provided in the VS Code terminal
* Add a Content-Type header with the value "application/json"
* Add the following Body and submit

#### Step 4: Desployment

For the last step, you will deploy this service and consume it in a simple web application. This application represents a Minimum Viable Product (MVP) of what the company would like to show their employees. It's very basic but will demonstrate that you can consume the results of an Azure Cognitive Search service in a website and deliver meaningful results to end users.

For this step, we are providing you with a pre-built static website that was built using Vue.js. Instructions are below for how to deploy this into Azure so you can see the results. Your role for this step will be to configure the site so it is connected to the Azure Cognitive Search you created in the previous steps.

If you would like, once you get it up and running, you should spend some time looking at the code and see if you can modify it to add some additional features.

##### Procedure

1. First you need to create a Static Website on the storage account you created in Step #4 in Environments
    - Under settings go to Static Website
    - Click on "Enabled"
    - The URL from Primary endpoint is how you will access the test site
2. Find the index.html file from the "Website" folder in the GitHub repo
3. In the file, configure the api-key and service url from your Azure Cognitive Search instance
4. In your Storage Account, click on "Containers" and find the $web container
5. Upload your configured index.html file
6. After the website is deployed, use it to test out the various features and ensure it is functioning correctly. Perform a number of searches demonstrating different aspects of the interface

##### Submission Materials

1. Save, commit, and push the changes you made in the index.html file
1. Take screenshots of the Azure Portal to demonstrate:
    - Amount of storage used including number of documents
    - Number of indexes, indexers, and data sources deployed
    - Search performance metrics from your searches from the web application

#### Stand out suggestions

* Add an additional build-in skill. For example, you can add an enriched field so users can search by a boolean field called SelectCourses and set this based on some combination of popularity, ratings, and sentiment scores.
* Create your own Azure Function cognitive skill to do something interesting with the data. For example, for any named entities, search Twitter for the latest Tweets. (For this, you would need to create a Twitter API account)
* Update the pre-built search solution to add additional functionality such as another facet or some other pre-built filters

#### Final Check For Submission

There are many files to submit for this project. Please check the list below to make sure you have everything ready for submission:

 - [ ] Step1_Requirements.docx or .txt
 - [ ] Step1_Architecture.jpg or .png
 - [ ] Step2_Data-Sources.jpg or .png
 - [ ] Step2_Skillset_Courses.json and Step2_Skillset_Library.json
 - [ ] Step2_Index_Courses.json and Step2_Index_Library.json
 - [ ] Step2_Indexer_Courses.json and Step2_Indexer_Library.json
 - [ ] Step2_Queries.txt
 - [ ] Step2_AdvancedQueries.txt
 - [ ] Step3_Courses_Skillset.json and Step3_Library_Skillset.json
 - [ ] Step3_Courses_Index.json and Step3_Library_Index.json
 - [ ] Step3_Courses_Indexer.json and Step3_Library_Indexer.json
 - [ ] Step3_AdvancedQueries.txt
 - [ ] storage_used.jpg or .png
 - [ ] deployed_app(optional number).jpg or .png screenshots
 - [ ] performance_metrics.jpg or .png
 - [ ] Link to Github Repository with your code changes
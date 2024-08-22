# Weather-Data-Analysis-Project
***
## Project Overview
This project is an overview of an Event Driven Sales Data Projection data pipeline that Process the Orders data based on their Status and route towards DynamoDB or SQS as per the Business requirement rules.
An airline daily data ingestion project using S3, S3 Cloudtrail Notification, Event Bridge Pattern Rule, Glue Crawler, Glue Visual ETL, SNS, Redshift, and Step Function

***

## Architectural Diagram
![AirlineProject](https://github.com/yash872/Airline-Data-Ingestion-Project/blob/main/Images/AirlineProject.jpg)

***

## Key Steps
### 1. Create a S3 bucket
- we will create a S3 bucket "airflow-managed-yb" to store the airflow scripts under dags folder and requirement.txt.
![S3](https://github.com/yash872/Weather-Data-Analysis-Project/blob/main/Images/S3_before.JPG)


### 2. Create a Codebuild Project
- we will create a CodeBuild Project "weather-cicd" for the CICD setup which will copy the dags script and othe files to the S3 on the pull merge request.
![Codebuild](https://github.com/yash872/Weather-Data-Analysis-Project/blob/main/Images/CodeBuild.JPG)

### 3. Create a Airflow Environment
- we will create a managed Airflow Environment "airflow-cluster-1" to orchestrate our pipeline.
![Airflow](https://github.com/yash872/Weather-Data-Analysis-Project/blob/main/Images/Airflow.JPG)


### 4. Create a pull merge request on github
- we will create a pull merge request on github to pull scripts and related files from test to main.
with the pull merge request, CodeBuild will be triggerd and perform the actions mentioned in buildspec.yml
![codeBuilsSuccess](https://github.com/yash872/Weather-Data-Analysis-Project/blob/main/Images/codeBuilsSuccess.JPG)

    - copy dags python script in the S3 dags filder.
    - ![S3Dags](https://github.com/yash872/Weather-Data-Analysis-Project/blob/main/Images/S3Dags.JPG)

    - copy the requirement.txt file in the S3 bucket.
    - ![S3Req](https://github.com/yash872/Weather-Data-Analysis-Project/blob/main/Images/S3Req.JPG)

    - copy the Glue python script to the related glue S3 bucket.
    - ![S3GlueScript](https://github.com/yash872/Weather-Data-Analysis-Project/blob/main/Images/S3GlueScript.JPG)


### 5. Check the Dags in Airflow UI
- Both the Dags available in the S3 Dags folder should appear in the Airflow UI.
    - openweather_api_dag
    - transform_redshift_dag
![AirflowDags](https://github.com/yash872/Weather-Data-Analysis-Project/blob/main/Images/AirflowDags.JPG)
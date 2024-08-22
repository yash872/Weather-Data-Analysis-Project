# Weather-Data-Analysis-Project
***
## Project Overview
This project is an overview of an Weather Data Analysis Pipeline that extracts the weather data live from the weather APIs and load it into the Readshift after reuired transformation.
This Project is using the the AWS Services like S3, CodeBuild, Airflow, Glue, Redshift etc. 

***

## Architectural Diagram
![Weather-Data-Analysis](https://github.com/yash872/Weather-Data-Analysis-Project/blob/main/Images/Weather-Data-Analysis.jpg)


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

### 6. Trigger the Dags
- We will trigger the Dag "openweather_api_dag" and start the execution.
![DagsTrigger](https://github.com/yash872/Weather-Data-Analysis-Project/blob/main/Images/DagsTrigger.JPG)

this Dag will perform 3 Tasks
![dag1](https://github.com/yash872/Weather-Data-Analysis-Project/blob/main/Images/dag1.JPG)

- Extract weather data from API and store in xcom
    - ![xcom](https://github.com/yash872/Weather-Data-Analysis-Project/blob/main/Images/xcom.JPG)
    
    - Upload that data in S3 bucket "weather-data-yb" as weather_api_data.csv
    - ![S3Data](https://github.com/yash872/Weather-Data-Analysis-Project/blob/main/Images/S3Data.JPG)

    - Trigger the Transform Redshift Dag
    - ![dag2](https://github.com/yash872/Weather-Data-Analysis-Project/blob/main/Images/dag2.JPG)
        - Glue Job "glue_transform_task" will be created
        - ![glueJob](https://github.com/yash872/Weather-Data-Analysis-Project/blob/main/Images/glueJob.JPG)
        - Data will be transformed and load to Redshift table "public.weather_data"
        - ![Redshift](https://github.com/yash872/Weather-Data-Analysis-Project/blob/main/Images/Redshift.JPG)

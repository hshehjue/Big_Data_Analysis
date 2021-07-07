# Analysis of US Federal Election Data

## Project Summary
   * **Authors**
     - Seungheon Han
     - Weike Zhou
     - Youssef Ragab
     - Yiliang Xu
     - Qunzhe Ding
   * **Affiliation**
     - Master of Science in Business Analytics at The George Washington University
   * **Objective**
     - Final Project of the DNSC6212 - Data Management for Analytics
   * **Description**
     - By exploring the given five bulk data sets corresponding to 2016 and 2020 provided by FEC website, find proper answers to the questions discussed in an interview with a sponsor ([Dr. Ali Obaidi](https://www.coursicle.com/gwu/professors/Ali+Obaidi/)).
     - **Questions:**
       - 1. Did transaction amount influence the final results of the ballots in the swing states in the 2020 presidential election? 
       - 2. Compared with the Contribution Received from Party Committees and other Political Committees for Candidates and their Party, what can you conclude?
         - Sub-question: What’s the differences between the committee’s and individual contribution for candidates and their party?
       - 3. What is the total liabilities that candidates hold in 2020? How does it differ to 2016?
       - 4. What are the 10 seats that received the most contributions both for the Senate and the House of Representatives?
   * **Software/Languages**
     - **Enviornment**
       - Ubuntu
       - Amazon Web Service(AWS)
         - EC2
         - S3
     - **Data Wrangling & Analysis**
       - Trifacta
       - PySpark
       - Unix Command
       - CSVcut
       - PostgreSQL
       - sparkSQL
     - **Visualizing**
       - Tableau
## Data 
   * **Source**
     - [Federal Election Commision(FEC) Bulk Data](https://www.fec.gov/data/browse-data/?tab=bulk-data)
   
   * **Used Datasets**
     - *All candidates (2016, 2020)*
     - *Candidate master (2016, 2020)*
     - *Candidate-committee linkages (2016, 2020)*
     - *Committee master (2016, 2020)*
     - *Contributions by individuals (2016, 2020)*
     
   * **Data Wrangling**
     - **Tools:** *Trifacta* 
     - **Recipe**
       1. Rename the columns.
          - Note that we need to add header on before we do our project.

       2. Delete the columns we don't need and includes too many NA or blank value in it.
          - there is too many NA and missing value, we do not need that because that's not useful information.

       3. Join the dateset with candidate master and all_cand by cand_id, with committee master by cmte_id and then add more colunms we need and integrate into the final dataset we need.
          - We need to join our dataset in to one final dataset in order for better analyze.

       4. delte some of mismatching value in the column.
          - this is because some mismatch value will contain a mismatch problem with our dataset.

       5. We decide to delete all the transaction is null value because that's not useful information.
          - some transaction is null is not usfulful when we want to analyze the total transaction we do not need the value which is not match into ourdaset.

       6. when we clean the data, we find the most large debt from trump is delete by mistake, so we add a value 11339279.2 from trump at column debts_owned_by.
          - some value is missing because mismatch prime key, so delete some useful value, so we decide to add on this useful information.

       7. run our final dataset into csv file and upload into our bucker so we can acess wget from the bucket.
  
  * **Schema**
  <img src=https://github.com/hshehjue/Big_Data_Analysis/blob/main/US_Federal_Election/images/schema.png width=90% height=90%>
  
 ## Results
   * **1. Did transaction amount influence the final results of the ballots in the swing states in the 2020 presidential election?** 
     - *The total amount of transactions (the sum of absolute values) occurring between committees and candidates affiliated to either democratic or republican party by states in 2020*
     - The 2020 electoral college forecast map published by CNN
       <img src=https://github.com/hshehjue/Big_Data_Analysis/blob/main/US_Federal_Election/images/q1_1.png width=80% height=80%>
     - Parties with bigger amount of transactions with committees by states in 2020
       <img src=https://github.com/hshehjue/Big_Data_Analysis/blob/main/US_Federal_Election/images/q1_2.png width=80% height=80%>
     - Predicted Map Vs Resulting Map 
       <img src=https://github.com/hshehjue/Big_Data_Analysis/blob/main/US_Federal_Election/images/q1_3.png width=80% height=80%>
----   
   * **2. Compared with the Contribution Received from Party Committees and other Political Committees for Candidates and their Party, what can you conclude?**
     <img src=https://github.com/hshehjue/Big_Data_Analysis/blob/main/US_Federal_Election/images/q2-1.png width=80% height=80%>
     <img src=https://github.com/hshehjue/Big_Data_Analysis/blob/main/US_Federal_Election/images/q2-2.png width=80% height=80%>
      
     - Sub: What’s the differences between the committee’s and individual contribution for candidates and their party?
       <img src=https://github.com/hshehjue/Big_Data_Analysis/blob/main/US_Federal_Election/images/sub2-1.png width=80% height=80%>
       <img src=https://github.com/hshehjue/Big_Data_Analysis/blob/main/US_Federal_Election/images/sub2-2.png width=80% height=80%>



----
    
  

        


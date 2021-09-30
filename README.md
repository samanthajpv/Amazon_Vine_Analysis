# Amazon_Vine_Analysis
An analysis on Amazon product reviews using PySpark

## Project Overview
The purpose of this project was to perform the ETL process using PySpark, connect to an AWS RDS instance, and load the transformed data into pgAdmin. The second part focuses on using PySpark to determine whether or not Amazon Vine members are biased toward providing high product ratings.

### Resources
- Data Source: [Home Entertainment](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt)
- Language: PySpark (Python API for Spark)
- Software: pgAdmin, AWS, Google Colab
- Notebooks:
    - [ETL Process](https://github.com/samanthajpv/Amazon_Vine_Analysis/blob/2bb32ae84458af41279d6ab55b55706777c35618/Amazon_Reviews_ETL.ipynb)
    - [Vine Review Analysis](https://github.com/samanthajpv/Amazon_Vine_Analysis/blob/977b086ee3ae1411bad4fa0c2e042b0d6fd48cb7/Vine_Review_Analysis.ipynb)

## Results
### ETL Process
The category of the dataset chosen for this project was Home Entertainment. Below were the steps performed:

   1. Create an AWS RDS instance.
   2. Connect the instance created to pgAdmin and create a new database.
   3. Run query to create tables in pgAdmin. Refer to [challenge_schema.sql](https://github.com/samanthajpv/Amazon_Vine_Analysis/blob/977b086ee3ae1411bad4fa0c2e042b0d6fd48cb7/challenge_schema.sql).
   4. Using PySpark, extract and transform data into four different dataframes (```customers_table```, ```products_table```, ```review_id_table```, and ```vine_table```). 
   5. Make the connection to the AWS RDS instance and load the dataframes that were created in step 4.
<p align="middle">
    <img src="https://github.com/samanthajpv/Amazon_Vine_Analysis/blob/2bb32ae84458af41279d6ab55b55706777c35618/Images/ETL.gif" width="800" height="450"/>
    <h5 align="center">pgAdmin Query Results</h5>
</p>

### Vine Review Analysis
Members of the Amazon Vine Program are trusted product reviewers on Amazon (more on [Amazon Vine](https://www.amazon.com/gp/vine/help). Using the ```vine_table``` created in the ETL process, additional calculations were performed to provide insight on the question if there is a bias from the reviews given by Amazon Vine members.

*Note:*
- Data was filtered to rows where count of ```total_votes``` is greater than or equal to 20 to select the reviews that are more likely to be helpful.
- Data was again filtered to select only the rows where number of ```helpful_votes``` is greater than or equal to 50% of the ```total_votes```. This was done to capture the reviews that are considered to be helpful by Amazon shoppers for the purpose of this project.
- Dataframes for paid(Vine) and unpaid(non-Vine) reviews were joined for easier comparison.

<p align="middle">
    <img src="https://github.com/samanthajpv/Amazon_Vine_Analysis/blob/977b086ee3ae1411bad4fa0c2e042b0d6fd48cb7/Images/Vine%20Analysis.png" width="600" height="200"/>
    <h5 align="center">Summary of Paid vs Unpaid Reviews on Home Entertainment Amazon Products</h5>
</p>

Findings:
- There is a total of 24,301 reviews; 261 under paid reviews, and 24,040 for unpaid reviews. Only 1.07% were from Amazon Vine members. This number shows how Amazon gets really particular in choosing their Vine members. 
- There are 106 5-star reviews from the Vine members and 10,899 from unpaid reviewers. The 5-star reviews from Vine members are only 0.96% of all the 5-star ratings.
- Focusing on the percentage of 5-star ratings relative to the total number of reviews per category (paid vs unpaid), 40.61% of the Vine reviews were 5-stars, and 45.34% for non-Vine reviews. Although there is a small difference between the two, these numbers are comparatively the same. 

## Summary

Based on the result of the analysis, there is no positivity bias for reviews coming from Vine members. As a matter of fact, the percentage of 5-star ratings from non-Vine members is 4.73% higher than the Vine reviews. -additional analysis to support your statement

## Reference
(1) Trilogy Education Services. (2021, September). *Module 16 Challenge*. https://courses.bootcampspot.com/courses/626/assignments/13346?module_item_id=213635

(2) Gouerseaud, Pierre. (2018, August 1). Answer on the online question post *Pyspark:How to calculate avg and count in a single groupBy?*. Stack Overflow. Retrieved on September 27, 2021 from https://stackoverflow.com/questions/51632126/pysparkhow-to-calculate-avg-and-count-in-a-single-groupby

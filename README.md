# eda-sql
Assignment: SQL Notebook for Peer Assignment
Estimated time needed: 60 minutes.

Introduction
Using this Python notebook you will:

Understand the Spacex DataSet
Load the dataset into the corresponding table in a Db2 database
Execute SQL queries to answer assignment questions
Overview of the DataSet
SpaceX has gained worldwide attention for a series of historic milestones.

It is the only private company ever to return a spacecraft from low-earth orbit, which it first accomplished in December 2010. SpaceX advertises Falcon 9 rocket launches on its website with a cost of 62 million dollars wheras other providers cost upward of 165 million dollars each, much of the savings is because Space X can reuse the first stage.

Therefore if we can determine if the first stage will land, we can determine the cost of a launch.

This information can be used if an alternate company wants to bid against SpaceX for a rocket launch.

This dataset includes a record for each payload carried during a SpaceX mission into outer space.
Tasks
Now write and execute SQL queries to solve the assignment tasks.

Note: If the column names are in mixed case enclose it in double quotes For Example "Landing_Outcome"

Task 1
Display the names of the unique launch sites in the space mission
%sql SELECT DISTINCT "Launch_Site" FROM SPACEXTABLE;
Launch_Site
CCAFS LC-40
VAFB SLC-4E
KSC LC-39A
CCAFS SLC-40

Task 2
Display 5 records where launch sites begin with the string 'CCA'
%sql SELECT * FROM SPACEXTABLE WHERE "Launch_Site" LIKE 'CCA%' LIMIT 5;
Date	Time (UTC)	Booster_Version	Launch_Site	Payload	PAYLOAD_MASS__KG_	Orbit	Customer	Mission_Outcome	Landing_Outcome
2010-06-04	18:45:00	F9 v1.0 B0003	CCAFS LC-40	Dragon Spacecraft Qualification Unit	0	LEO	SpaceX	Success	Failure (parachute)
2010-12-08	15:43:00	F9 v1.0 B0004	CCAFS LC-40	Dragon demo flight C1, two CubeSats, barrel of Brouere cheese	0	LEO (ISS)	NASA (COTS) NRO	Success	Failure (parachute)
2012-05-22	7:44:00	F9 v1.0 B0005	CCAFS LC-40	Dragon demo flight C2	525	LEO (ISS)	NASA (COTS)	Success	No attempt
2012-10-08	0:35:00	F9 v1.0 B0006	CCAFS LC-40	SpaceX CRS-1	500	LEO (ISS)	NASA (CRS)	Success	No attempt
2013-03-01	15:10:00	F9 v1.0 B0007	CCAFS LC-40	SpaceX CRS-2	677	LEO (ISS)	NASA (CRS)	Success	No attempt

Task 3
Display the total payload mass carried by boosters launched by NASA (CRS)
%sql SELECT SUM("PAYLOAD_MASS__KG_") AS Total_Payload_Mass_kg FROM SPACEXTABLE WHERE "Customer" LIKE '%NASA (CRS)%';
Total_Payload_Mass_kg
48213

Task 4
Display average payload mass carried by booster version F9 v1.1
%sql SELECT AVG("PAYLOAD_MASS__KG_") AS Average_Payload_Mass_Kg FROM SPACEXTABLE WHERE "Booster_Version" = 'F9 v1.1';
Average_Payload_Mass_Kg
2928.4

Task 5
List the date when the first succesful landing outcome in groundCH hhc
%sql SELECT MIN("Date") AS First_Successful_Ground_Landing_Date FROM SPACEXTABLE WHERE "Landing_Outcome" = 'Success (ground pad)';
First_Successful_Ground_Landing_Date
2015-12-22

Task 6
List the names of the boosters which have success in drone ship and have payload mass greater than 4000 but less than 6000
%sql SELECT "Booster_Version", "PayloadMass__kg_", "Landing_Outcome" FROM SPACEXTABLE WHERE "Landing_Outcome" = 'Success (drone ship)';
%sql SELECT "Booster_Version", "PayloadMass__kg_", "Landing_Outcome" FROM SPACEXTABLE WHERE "Landing_Outcome" = 'Success (drone ship)' AND "PayloadMass__kg_" > 4000 AND "PayloadMass__kg_" < 6000;
Booster_Version	"PayloadMass__kg_"	Landing_Outcome

Task 7
List the total number of successful and failure mission outcomes
%sql SELECT TRIM("Mission_Outcome") AS Cleaned_Outcome, COUNT(*) AS Total_Count FROM SPACEXTABLE GROUP BY TRIM("Mission_Outcome");
Cleaned_Outcome	Total_Count
Failure (in flight)	1
Success	99
Success (payload status unclear)	1

Task 8
List all the booster_versions that have carried the maximum payload mass. Use a subquery.
%sql SELECT "Booster_Version", "PayloadMass__kg_" FROM SPACEXTABLE WHERE "PayloadMass__kg_" = ( SELECT MAX("PayloadMass__kg_") FROM SPACEXTABLE );
 * sqlite:///my_data1.db
Done.
Booster_Version	"PayloadMass__kg_"
F9 v1.0 B0003	PayloadMass__kg_
F9 v1.0 B0004	PayloadMass__kg_
F9 v1.0 B0005	PayloadMass__kg_
F9 v1.0 B0006	PayloadMass__kg_
F9 v1.0 B0007	PayloadMass__kg_
F9 v1.1 B1003	PayloadMass__kg_
F9 v1.1	PayloadMass__kg_
F9 v1.1	PayloadMass__kg_
F9 v1.1	PayloadMass__kg_
F9 v1.1	PayloadMass__kg_
F9 v1.1	PayloadMass__kg_
F9 v1.1 B1011	PayloadMass__kg_
F9 v1.1 B1010	PayloadMass__kg_
F9 v1.1 B1012	PayloadMass__kg_
F9 v1.1 B1013	PayloadMass__kg_
F9 v1.1 B1014	PayloadMass__kg_
F9 v1.1 B1015	PayloadMass__kg_
F9 v1.1 B1016	PayloadMass__kg_
F9 v1.1 B1018	PayloadMass__kg_
F9 FT B1019	PayloadMass__kg_
F9 v1.1 B1017	PayloadMass__kg_
F9 FT B1020	PayloadMass__kg_
F9 FT B1021.1	PayloadMass__kg_
F9 FT B1022	PayloadMass__kg_
F9 FT B1023.1	PayloadMass__kg_
F9 FT B1024	PayloadMass__kg_
F9 FT B1025.1	PayloadMass__kg_
F9 FT B1026	PayloadMass__kg_
F9 FT B1029.1	PayloadMass__kg_
F9 FT B1031.1	PayloadMass__kg_
F9 FT B1030	PayloadMass__kg_
F9 FT B1021.2	PayloadMass__kg_
F9 FT B1032.1	PayloadMass__kg_
F9 FT B1034	PayloadMass__kg_
F9 FT B1035.1	PayloadMass__kg_
F9 FT B1029.2	PayloadMass__kg_
F9 FT B1036.1	PayloadMass__kg_
F9 FT B1037	PayloadMass__kg_
F9 B4 B1039.1	PayloadMass__kg_
F9 FT B1038.1	PayloadMass__kg_
F9 B4 B1040.1	PayloadMass__kg_
F9 B4 B1041.1	PayloadMass__kg_
F9 FT B1031.2	PayloadMass__kg_
F9 B4 B1042.1	PayloadMass__kg_
F9 FT B1035.2	PayloadMass__kg_
F9 FT B1036.2	PayloadMass__kg_
F9 B4 B1043.1	PayloadMass__kg_
F9 FT B1032.2	PayloadMass__kg_
F9 FT B1038.2	PayloadMass__kg_
F9 B4 B1044	PayloadMass__kg_
F9 B4 B1041.2	PayloadMass__kg_
F9 B4 B1039.2	PayloadMass__kg_
F9 B4 B1045.1	PayloadMass__kg_
F9 B5 B1046.1	PayloadMass__kg_
F9 B4 B1043.2	PayloadMass__kg_
F9 B4 B1040.2	PayloadMass__kg_
F9 B4 B1045.2	PayloadMass__kg_
F9 B5B1047.1	PayloadMass__kg_
F9 B5B1048.1	PayloadMass__kg_
F9 B5 B1046.2	PayloadMass__kg_
F9 B5B1049.1	PayloadMass__kg_
F9 B5 B1048.2	PayloadMass__kg_
F9 B5 B1047.2	PayloadMass__kg_
F9 B5 B1046.3	PayloadMass__kg_
F9 B5B1050	PayloadMass__kg_
F9 B5B1054	PayloadMass__kg_
F9 B5 B1049.2	PayloadMass__kg_
F9 B5 B1048.3	PayloadMass__kg_
F9 B5B1051.1	PayloadMass__kg_
F9 B5B1056.1	PayloadMass__kg_
F9 B5 B1049.3	PayloadMass__kg_
F9 B5 B1051.2	PayloadMass__kg_
F9 B5 B1056.2	PayloadMass__kg_
F9 B5 B1047.3	PayloadMass__kg_
F9 B5 B1048.4	PayloadMass__kg_
F9 B5B1059.1	PayloadMass__kg_
F9 B5 B1056.3	PayloadMass__kg_
F9 B5 B1049.4	PayloadMass__kg_
F9 B5 B1046.4	PayloadMass__kg_
F9 B5 B1051.3	PayloadMass__kg_
F9 B5 B1056.4	PayloadMass__kg_
F9 B5 B1059.2	PayloadMass__kg_
F9 B5 B1048.5	PayloadMass__kg_
F9 B5 B1051.4	PayloadMass__kg_
F9 B5B1058.1	PayloadMass__kg_
F9 B5 B1049.5	PayloadMass__kg_
F9 B5 B1059.3	PayloadMass__kg_
F9 B5B1060.1	PayloadMass__kg_
F9 B5 B1058.2	PayloadMass__kg_
F9 B5 B1051.5	PayloadMass__kg_
F9 B5 B1049.6	PayloadMass__kg_
F9 B5 B1059.4	PayloadMass__kg_
F9 B5 B1060.2	PayloadMass__kg_
F9 B5 B1058.3	PayloadMass__kg_
F9 B5 B1051.6	PayloadMass__kg_
F9 B5 B1060.3	PayloadMass__kg_
F9 B5B1062.1	PayloadMass__kg_
F9 B5B1061.1	PayloadMass__kg_
F9 B5B1063.1	PayloadMass__kg_
F9 B5 B1049.7	PayloadMass__kg_
F9 B5 B1058.4	PayloadMass__kg_

Task 9
List the records which will display the month names, failure landing_outcomes in drone ship ,booster versions, launch_site for the months in year 2015.
Note: SQLLite does not support monthnames. So you need to use substr(Date, 6,2) as month to get the months and substr(Date,0,5)='2015' for year.

%sql SELECT  SUBSTR("Date", 6, 2) AS Month, "Landing_Outcome", "Booster_Version", "Launch_Site" FROM SPACEXTABLE WHERE SUBSTR("Date", 1, 4) = '2015' AND "Landing_Outcome" LIKE '%Failure%'  AND "Landing_Outcome" LIKE '%drone ship%';
 * sqlite:///my_data1.db
Done.
Month	Landing_Outcome	Booster_Version	Launch_Site
01	Failure (drone ship)	F9 v1.1 B1012	CCAFS LC-40
04	Failure (drone ship)	F9 v1.1 B1015	CCAFS LC-40

Task 10
Rank the count of landing outcomes (such as Failure (drone ship) or Success (ground pad)) between the date 2010-06-04 and 2017-03-20, in descending order.
%sql SELECT "Landing_Outcome", COUNT(*) AS Outcome_Count FROM SPACEXTABLE WHERE  "Date" >= '2010-06-04' AND "Date" <= '2017-03-20' GROUP BY "Landing_Outcome" ORDER BY Outcome_Count DESC;
 * sqlite:///my_data1.db
Done.
Landing_Outcome	Outcome_Count
No attempt	10
Success (drone ship)	5
Failure (drone ship)	5
Success (ground pad)	3
Controlled (ocean)	3
Uncontrolled (ocean)	2
Failure (parachute)	2
Precluded (drone ship)	1



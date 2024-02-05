# Taxi Database and Server Testing

**Project Overview:**

Chicago Taxi operates as a ride-sharing service that offers taxi rides in Chicago. Nevertheless, the service has experienced several glitches in its system, both on the remote server and in the data fetched from the database.

In my role as a QA engineer on this project, I was responsible for addressing these issues. This involved investigating the bugs by executing bash commands on the remote server and querying the database using SQL commands with PostgreSQL.

**Your Role and Contributions:**

In my capacity as a QA engineer on this project, my responsibilities included:
- Delving into and retrieving logs that contained error messages and details related to specific requests and responses.
- Generating reports on requested data using SQL queries, and subsequently comparing the results with the anticipated outcomes, particularly in cases where discrepancies arose concerning the expected number of available taxis for service.

**Project Deliverables:**

Anticipated deliverables encompass:
- Documents containing the requested information pertaining to error logs and request details.
- A comprehensive report presenting the sought-after results obtained through SQL queries against the database.

**Testing Approach:**

The testing approach predominantly centers on database testing, with a primary emphasis on ensuring data integrity. The main thrust of the testing effort is to guarantee that the data remains both up-to-date and accurate. This holds particular significance, given that ride-sharing services demand impeccable software quality, especially in the context of real-time applications.

**List of Tests Conducted:**

The system logs were scrutinized using the following bash commands, aiming to generate files that encapsulate the requested HTTP request information:

- Returning logs with a specific IP address
```
cd ~/logs/2019/12
grep -R -l "^233.201" .
```
- Creating files with 400 and 500 requests
```
mkdir ~/bug1
mkdir ~/bug1/events
grep '." [45]00 .' ~/logs/2019/12/apache_2019-12-30.txt > ~/bug1/main.txt
```
- Separating created file into two separate files detailing different responses
```
grep '." 400 .' ~/bug1/main.txt > ~/bug1/events/400.txt
grep '." 500 .' ~/bug1/main.txt > ~/bug1/events/500.txt

```

The requested data was obtained by executing the following SQL commands:

- SQL query fetching the total number of distinct cars in order to find the disparity between the expected number of cars
```
SELECT COUNT(DISTINCT vehicle_id) FROM cabs;
```
- SQL query fetching a list of companies with fewer than 100 taxis available
```
SELECT COUNT(vehicle_id), company_name
FROM cabs
GROUP BY company_name
HAVING COUNT(vehicle_id) < 100
ORDER BY COUNT(vehicle_id) DESC;
```

**Screenshot of Test Results:**
In terms of navigating the remote server, the commands focused on retrieving requests from a particular IP address yielded two results:
```
apache_2019-12-18.txt:233.201.188.154 - - [18/12/2019:21:46:01 +0000] "DELETE /events HTTP/1.1" 403 3971
apache_2019-12-21.txt:233.201.182.9 - - [21/12/2019:21:56:20 +0000] "PATCH /users HTTP/1.1" 400 4118
```
Regarding the exploration of requests with 400 and 500 response codes to investigate a system bug, we identified 172 requests with 400 response codes and 156 requests with 500 response codes.

In the database, the expected number of cars was set at 10,550. However, the results from the SQL queries indicated that only 5,500 cars were available.

Here is the requested list of companies with fewer than 100 cars:
```
count |             	company_name
-------+----------------------------------------------
	97 | Nova Taxi Affiliation Llc
	89 | Patriot Taxi Dba Peace Taxi Associat
	85 | Blue Diamond
	81 | Checker Taxi Affiliation
	80 | Chicago Medallion Management
	69 | Chicago Independents
	67 | 24 Seven Taxi
	60 | Checker Taxi
	55 | American United
	53 | Chicago Medallion Leasing INC
	49 | Top Cab Affiliation
	48 | KOAM Taxi Association
	38 | Chicago Taxicab
	34 | Norshore Cab
	20 | Gold Coast Taxi
	20 | Metro Group
	18 | Service Taxi Association
	14 | 5 Star Taxi
 	8 | American United Taxi Affiliation
 	8 | Metro Jet Taxi A
 	7 | Setare Inc
 	5 | Leonard Cab Co
 	1 | 4615 - 83503 Tyrone Henderson
 	1 | 5062 - 34841 Sam Mestas
 	1 | 4623 - 27290 Jay Kim
 	1 | 5997 - 65283 AW Services Inc.
 	1 | 2092 - 61288 Sbeih company
 	1 | 1469 - 64126 Omar Jada
 	1 | 2733 - 74600 Benny Jona
 	1 | 2192 - 73487 Zeymane Corp
 	1 | 5006 - 39261 Salifu Bawa
 	1 | 3556 - 36214 RC Andrews Cab
 	1 | 3721 - Santamaria Express, Alvaro Santamaria
 	1 | 2809 - 95474 C & D Cab Co Inc.
 	1 | 2241 - 44667 - Felman Corp, Manuel Alonso
 	1 | 3620 - 52292 David K. Cab Corp.
 	1 | 2823 - 73307 Lee Express Inc
 	1 | 6057 - 24657 Richard Addo
 	1 | 6742 - 83735 Tasha ride inc
 	1 | 1085 - 72312 N and W Cab Co
 	1 | 3591 - 63480 Chuks Cab
 	1 | 0118 - 42111 Godfrey S.Awir
 	1 | 6574 - Babylon Express Inc.
 	1 | 3094 - 24059 G.L.B. Cab Co
 	1 | 5874 - 73628 Sergey Cab Corp.
 	1 | 6743 - 78771 Luhak Corp
 	1 | 5074 - 54002 Ahzmi Inc
 	1 | 3623 - 72222 Arrington Enterprises
 	1 | 4053 - 40193 Adwar H. Nikola
 	1 | Chicago Star Taxicab
 	1 | 3011 - 66308 JBL Cab Inc.
```

**Challenges Faced:**
I encountered challenges due to occasional misinterpretations on my part regarding the developers' requests. Improved communication efficiency played a crucial role in enhancing my understanding of their requirements, ultimately leading to more accurate results.

**Results and Outcomes:**
The remote server indicates the existence of requests that could potentially be contributing factors to the system defect.

Upon examining the database, disparities emerged between the expected and actual results. Additionally, potential companies to engage with regarding the low number of available cars were identified.

**Key Takeaways:**

I've gained proficiency in the following:
- Employing bash commands for tasks related to databases and remote servers.
- Executing a diverse range of queries using SQL.

**Conclusion:**

The project proved to be a valuable and hands-on experience in utilizing the console for working with remote servers and databases in the realm of software testing. The process of analyzing and condensing logs into files, as well as executing SQL queries to compare results, has honed skills that will undoubtedly prove beneficial in future projects.

I extend my gratitude to Ekaterina Kolesnikova for offering valuable insights that have enhanced the quality of my work.

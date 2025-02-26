# Web-Server-Log-Analysis
# Project Overview

Web-Server-Log-Analysis is a project designed to analyze web server logs using Apache Hive to understand user interactions and system performance. The project's purpose is to provide insights into the frequency of web requests, status code distributions, the popularity of specific pages, common user agents, and patterns of failed requests. It aims to help in optimizing server performance, improving user experience, and enhancing security measures by identifying suspicious activities.

# Implementation Approach
The project utilizes a series of HiveQL queries to extract and summarize data from web server logs. Below are explanations of each query used in the analysis:

a. Total Web Requests:
Calculates the total number of web requests logged.
SELECT COUNT(*) AS total_requests FROM webserver_logs;

b. Status Code Analysis:
Aggregates requests by HTTP status codes to determine their frequency.
SELECT status, COUNT(*) AS Frequency FROM webserver_logs GROUP BY status;

c. Most Visited Pages:
Identifies the top three most frequently accessed URLs.
SELECT url, COUNT(*) AS Visits FROM webserver_logs GROUP BY url ORDER BY Visits DESC LIMIT 3;

d. Traffic Source Analysis:
Lists the most common user agents used during web requests, which helps in understanding the predominant browsers or bots.
SELECT user_agent, COUNT(*) AS Count FROM webserver_logs GROUP BY user_agent ORDER BY Count DESC;

e. Suspicious IP Addresses:
Detects IP addresses with more than 3 failed requests (HTTP status 404 or 500), which could indicate potential security threats.
SELECT ip, COUNT(*) AS Failed_Requests FROM webserver_logs WHERE status = 404 OR status = 500 GROUP BY ip HAVING COUNT(*) > 3;

f. Traffic Trend Over Time:
Analyzes the number of requests per minute to observe traffic trends and peak usage times.
SELECT SUBSTR(ts, 1, 16) AS Minute, COUNT(*) AS Requests FROM webserver_logs GROUP BY SUB
# yaa_SQL_portfolio
# "Stars and Awards: Unraveling 'Epic TV Adventures' Success Through Comprehensive Dataset Analysis"

# A LITTLE ABOUT THE DATASET 
The dataset, powered by SQL, delves into "Epic TV Adventures," covering awards, characters, credits, episodes, persons, and votes. SQL queries provide key insights into award distribution, organizational achievements, individual contributions, and viewer engagement. This dataset is a valuable resource for making informed decisions to ensure the ongoing success of "Epic TV Adventures."

Insight to be Gained:

To discover details about awards, unique organizations, character award counts, top-rated episodes, average person height, highly voted episodes, organizational success, relationships, individual achievements, and episode comparisons. SQL's analytical capabilities make this dataset essential for navigating the dynamic world of television entertainment.

# QUESTIONS TO LEAD TO THE INSIGHT

1. Retrieve all columns from the "Award" table.
2. List unique organizations from the "Award" table.
3. Count the total number of records in the "Character_Award" table.
4. Display the distinct roles from the "Credit" table.
5. Find the maximum and minimum birthdates from the "Person" table.
6. List the top 5 episodes with the highest ratings.
7. Calculate the average height of persons in meters from the "Person" table.
8. Identify episodes with more than 100 votes in the "Episode" table.
9. Count the number of awards won by each organization.
10. Retrieve the names of persons who have not been credited in any episode.
11. Find the episode with the most keywords.
12. Calculate the average number of votes per episode.
13. Identify persons who have won awards in multiple categories.
14. List the top 3 most common birthplaces in the "Person" table.
15. Calculate the percentage of votes for each episode in the "Vote" table.
16. Determine the person with the most credited roles in episodes.
17. Find the organization with the highest number of awards in a specific year.
18. Identify episodes that share keywords with a given episode.
19. Calculate the total number of awards won by each person.
20. Find episodes with the same ratings and display their details.

# SQL CODE DEPLOYMENT


-- Retrieve all columns from the "Award" table.

SELECT * FROM [dbo].[Award]

-- List unique organizations from the "Award" table.

SELECT DISTINCT [Organization] AS [THE DIVERSE ORGANIZATION]
FROM [dbo].[Award]


-- Count the total number of records in the "Character_Award" table.

SELECT COUNT(*) AS [TOTAL NUMBER OF RECORDS]
FROM [dbo].[Character_Award]


-- Display the distinct roles from the "Credit" table.

SELECT DISTINCT [role] AS [ THE VARIOUS ROLES]
FROM [dbo].[Credit]

-- Find the maximum and minimum birthdates from the "Person" table.

SELECT MAX([birthdate]) AS [OLDEST DATE OF BIRTH],
MIN([birthdate]) AS [YOUNGEST DATE OF BIRTH]
FROM [dbo].[Person]


-- List the top 5 episodes with the highest ratings.

SELECT TOP 5 [title] AS [TITLE]
            ,[episode_id] AS [EPISODE ID]
            ,[rating] AS [TOP RATINGS]
            ,[episode] AS [TOP EPISODE]
FROM [dbo].[Episode]
ORDER BY [rating] DESC

-- Find the organization with the highest number of awards in a specific year

SELECT TOP 1
 [Organization], 
 COUNT(*) AS [NUMBER OF AWARDS]
 FROM [dbo].[Award] 
 WHERE [Year] = '2014'
 GROUP BY [Organization]
 ORDER BY [NUMBER OF AWARDS] DESC;
 

 -- Calculate the average number of votes per episode.

SELECT 
AVG([votes]) AS [NUMBER OF VOTES PER EPISODE]
FROM [dbo].[Episode]


-- Identify episodes with more than 100 votes in the "Episode" table.

SELECT [episode_id] AS [EPISODE ID]
        ,[title] AS [TITLE]
        ,[votes] AS [NUMBER OF VOTES]
FROM [dbo].[Episode]
WHERE [votes] > 100 

-- Count the number of awards won by each organization.

SELECT COUNT(*) AS [NUMBER OF AWARDS WON],
        [Organization] AS [ORGANIZATIONS]
FROM [dbo].[Award]
GROUP BY  [Organization]
ORDER BY [NUMBER OF AWARDS WON] DESC


-- Retrieve the names of persons who have not been credited in any episode.

SELECT [name] AS [NAMES OF INDIVIDUALS WHO HAVE NOT BEEN CREDITED]
FROM [dbo].[Person] 
WHERE [name] NOT IN (
SELECT DISTINCT [person] 
FROM [dbo].[Credit]) 
ORDER BY [NAMES OF INDIVIDUALS WHO HAVE NOT BEEN CREDITED] 

-- Calculate the average height of persons in meters from the "Person" table.

SELECT ROUND(AVG([height_meters]),2)  AS [AVERAGE HEIGHT OF PERSONS]
FROM [dbo].[Person]

-- Find the episode with the most keywords.

SELECT TOP 1
        [episode_id] AS [EPISODE ID],
        COUNT(*) AS [NUMBER OF KEYWORDS]
FROM [dbo].[Keyword]
GROUP BY [episode_id]
ORDER BY [NUMBER OF KEYWORDS] DESC


-- Calculate the average height of persons in meters from the "Person" table.

SELECT ROUND(AVG([height_meters]),2)  AS [AVERAGE HEIGHT OF PERSONS]
FROM [dbo].[Person]

-- Identify persons who have won awards in multiple categories.

SELECT 
NULLIF(LTRIM(RTRIM([Person])), '') AS [PEOPLE WHO WON AWARDS],
COUNT(DISTINCT [Award_category]) AS [THE VARIOUS CATEGORIES]
FROM [dbo].[Award] 
WHERE [Person]IS NOT NULL 
AND NULLIF(RTRIM(LTRIM([Person])), '') IS NOT NULL
GROUP BY [Person]
HAVING COUNT(DISTINCT [Award_category]) > 1


-- List the top 3 most common birthplaces in the "Person" table.

SELECT TOP 3
    NULLIF(LTRIM(RTRIM([birth_place])), '') AS cleaned_birth_place,
    COUNT(*) AS birthplace_count
FROM [dbo].[Person]
WHERE [birth_place] IS NOT NULL AND NULLIF(LTRIM(RTRIM([birth_place])), '') IS NOT NULL
GROUP BY NULLIF(LTRIM(RTRIM([birth_place])), '')
ORDER BY birthplace_count DESC;

-- Calculate the percentage of votes for each episode in the "Vote" table.

SELECT [episode_id],
    COUNT(DISTINCT [episode_id]) AS [THE VARIOUS EPISODES]
    ,[votes] AS [NUMBER OF VOTES]
    ,[percent] AS [PERCENTAGE OF VOTES]
FROM [dbo].[Vote]
GROUP BY [votes], [percent], [episode_id]
ORDER BY [votes] DESC

SELECT [episode_id] [THE VARIOUS EPISODES],
        [votes] [NUMBER OF VOTES],
        [percent] [PERCENTAGE OF VOTES]
FROM [dbo].[Vote]
ORDER BY [percent] DESC


-- List the top 3 most common birthplaces in the "Person" table.

SELECT TOP 3
    NULLIF(LTRIM(RTRIM([birth_place])), '') AS cleaned_birth_place,
    COUNT(*) AS birthplace_count
FROM [dbo].[Person]
WHERE [birth_place] IS NOT NULL AND NULLIF(LTRIM(RTRIM([birth_place])), '') IS NOT NULL
GROUP BY NULLIF(LTRIM(RTRIM([birth_place])), '')
ORDER BY birthplace_count DESC;


-- Find the episode with the most keywords.

SELECT TOP 1
   EP.[episode] AS [EPISODE],
   EP.[air_date] AS [DATE AIRED],
   EP.[title] AS [TITILE OF EPISODE],
COUNT(KD.[keyword]) AS [EPISODE WITH THE MOST KEY PHRASE]
FROM [dbo].[Keyword] KD
JOIN [dbo].[Episode] EP 
ON KD.[episode_id] = EP.[episode_id]
GROUP BY EP.[title], EP.[episode],EP.[air_date]
ORDER BY [EPISODE WITH THE MOST KEY PHRASE] DESC


-- Find the organization with the highest number of awards in a specific year

SELECT TOP 1
 [Organization] AS [ORGANIZATION], 
 COUNT(*) AS [NUMBER OF AWARDS]
 FROM [dbo].[Award] 
 WHERE [Year] = '2014' 
 GROUP BY [Organization]
 ORDER BY [NUMBER OF AWARDS] DESC;
 

-- Calculate the percentage of votes for each episode in the "Vote" table.

SELECT [episode_id],
    COUNT(DISTINCT [episode_id]) AS [THE VARIOUS EPISODES]
    ,[votes] AS [NUMBER OF VOTES]
    ,[percent] AS [PERCENTAGE OF VOTES]
FROM [dbo].[Vote]
GROUP BY [votes], [percent], [episode_id]
ORDER BY [votes] DESC

SELECT [episode_id] [THE VARIOUS EPISODES],
        [votes] [NUMBER OF VOTES],
        [percent] [PERCENTAGE OF VOTES]
FROM [dbo].[Vote]
ORDER BY [percent] DESC

-- Calculate the average number of votes per episode.

SELECT 
AVG([votes]) AS [NUMBER OF VOTES PER EPISODE]
FROM [dbo].[Episode]

-- Determine the first 100 people with the most credited roles in episodes.

SELECT TOP 100
        CT.[person] AS [PERSON WITH THE MOST CREDITED ROLES],
        ED.[title] AS [EPISODE TITLE],
        CT.[role] AS [ROLE],
        CT.[credited] AS [CREDITED(TRUE OR FALSE)],
        ED.[episode_id] AS [EPISODE_ID]
       
FROM 
    [dbo].[Credit] CT
JOIN
    [dbo].[Episode] ED
ON CT.[Episode_id] =ED.[episode_id]
ORDER BY [CREDITED(TRUE OR FALSE)] DESC


-- Find the organization with the highest number of awards in a specific year

SELECT TOP 1
 [Organization] AS [ORGANIZATION], 
 COUNT(*) AS [NUMBER OF AWARDS]
 FROM [dbo].[Award] 
 WHERE [Year] = '2014' 
 GROUP BY [Organization]
 ORDER BY [NUMBER OF AWARDS] DESC;
 
-- Calculate the total number of awards won by each person.

SELECT TOP 10
   NULLIF(LTRIM(RTRIM([Person])),'') AS [INDIVIDUALS],
    COUNT(DISTINCT [Award]) AS [TOTAL NUMBER OF AWARDS]
FROM[dbo].[Award]
WHERE  NULLIF(LTRIM(RTRIM([Person])),'')  IS NOT NULL  AND  [Person] IS NOT NULL
GROUP BY [Person]
ORDER BY[TOTAL NUMBER OF AWARDS] DESC


-- Find episodes with the same ratings and display their details.

SELECT 
ED1.[episode_id] [EPISODE_ID],
ED1.[title] [EPISODE TITLE],
ED2.[episode_id] [EPISODE2_ID],
ED2.[title] [TITLE2_ID],
ED1.[rating]
FROM 
[dbo].[Episode] ED1
JOIN
[dbo].[Episode] ED2
ON ED1.[rating] = ED2.[rating]
AND ED1.[episode_id] <> ED2.[episode_id]
WHERE ED1.[episode_id] < ED2.[episode_id]
ORDER BY ED1.[rating] DESC



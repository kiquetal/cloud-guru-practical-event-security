#### Query Events

- By default Cloudtrail store data by 90 days.

aws cloudtrail lookup-events --max-items 100

aws cloudtrail lookup-events --lookup-attributes "AtributeKey=Username,AttributeValue=Alex.Higgns" 


#### Athena queries


- Direct integration on cloudtrail.

```sql
# QUERY 1
# Query based on a username.
SELECT *
FROM "default"."cloudtrail_logs_my_acg_test_cloudtrail_logs"
WHERE 
    useridentity.username = 'TheAlexanderHiggins@gmail.com'
LIMIT 10;

# QUERY 2
# Query Based on multiple users.
SELECT *
FROM "default"."cloudtrail_logs_my_acg_test_cloudtrail_logs"
WHERE
    useridentity.username = 'TheAlexanderHiggins@gmail.com' OR
    useridentity.username = 'alex.higgins' OR
    useridentity.username = 'andrew.kroll'
LIMIT 10;

# QUERY 3
# See active users in the last 7 days.
SELECT DISTINCT useridentity.username
FROM "default"."cloudtrail_logs_my_acg_test_cloudtrail_logs"
WHERE 
    from_iso8601_timestamp(eventtime) > date_add('day', -7, now())
LIMIT 10;


```




#### Cross Account Cloudtrail


- Manage different accounts to send data to a central logging account.

- Keeps logs away from the same account they were created in.

- Better restrict who can access log data.





### Quizzes

- 90 days by default
- S3 and Lambda can be used to store data events.
- Cloudtrail by default is enabled to all regions.


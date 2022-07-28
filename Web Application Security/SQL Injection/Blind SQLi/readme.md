# Blind SQLi

## What is Blind SQLi?
- A type of SQLi attack that asks the DB true or false questions and determines the answer based on the appllications responses. 
- This type of attack can help a malicious actor ascertain pieces of information about the application or information within the databse by following a methodical approach
- This type of SQL injection is uch mroe difficult but can be very effective
    
    
## Content Based Blind SQLi    
- By using process of elimination, attackers can learn more and more about the inner workings of an application or information stored within it's database
- This type of attack relies on the idea that the application will respond a different way depedning on if a statement sent to the database is true or false.

For example if you type in a URL and it looks like this:

```bash
http://fun.com/catalog.php?id=2
``` 

and it sends the following query to the DB:

```SQL
SELECT name, description FROM catalog WHERE id=2
```

From there the attacker may then try ti inject a query that returns 'false':

```bash
http://fun.com/catalog.php?id=2 and 1=2
``` 

Now the query would look like this:
```SQL
SELECT name, description FROM catalog WHERE id=2 and 1=2
```

if it is vulnerable to SQL injection then it probably will not return anything. To make sure the attacker will inject a query that will return true they can run this:
```SQL
SELECT name, description FROM catalog WHERE id=2 and 1=1
```

While this process may seem tedious, by contining to run these queries against a site, the attacker is only limited by their imagination and their time. 

## Time based Blind SQL Injection

This kind of attack relies on the DB pausing for a specified amount of time then returning the results, indicating successful SQL query executing. 

Attackers will inject time pauses to determine if a query they sent is true. 

This includes:
- Using operations that perform a specific task tha happen to cause a time delay
- Or specficfially passing a function that causes time delays 

SQLMap is a great tool to used for detecting SQL Injection attacks (Created by the OWASP Foundation)




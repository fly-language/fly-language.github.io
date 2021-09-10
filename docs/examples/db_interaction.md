---
layout: default
title: DB Interaction
parent: Examples
nav_order: 3
---
# DB Interaction example

### Average temperature insertion
The example aims to show how to interact with a database in Fly language. The operations will calculate the average temperature for each province.

## How to run
In order to correctly run the algorithm, there are some rules that must be respectes:
* The value of __nthread__ must be a number between 0 and the number of different provinces into the database.
* There are multiple declaration of the __cloud__ environment, one for each supported Cloud Provider. Only one of them could not be commented.

## CSV File
The content of the CSV file is the following:
| ID | Temperature | City | Province |
|:---:|:---:|:---:|:---:|
|1|11|Marcianise|Caserta|
|2|14|Napoli|Napoli|
|3|9|Fisciano|Salerno|
|4|13|Capua|Caserta|
|5|13|Afragola|Napoli|
|6|11|Nocera|Salerno|
|7|12|Aversa|Caserta|
|8|12|Acerra|Napoli|
|9|10|Salerno|Salerno|
|10|14|Battipaglia|Salerno|
|11|13.5|Eboli|Salerno|
|12|12.6|Maddaloni|Caserta|
|13|13.3|Mondragone|Caserta|
|14|14|Torre del Greco|Napoli|
|15|13.5|Casoria|Napoli|


## Functions

The program is composed by two functions:

* **[Insert average Function](#insert-average-function)**
* **[Check insertion Function](#check-insertion-function)**
  
### Insert average Function 

This function calculates the average temperature for each province, then insert the value into the database. If the query is correctly executed, every city of a determined province will have the same temperature of the others. Before executing this function, the program creates the DB from the CSV file and calculate the __columns__ variable, containing the list of all provinces in the database.

The Fly code is the following:

```
func insertavg (columns){

	var dbConnCloud = [type="sql", resourceGroup="", instance="", dbName="companyFunding", user="", password=""] on cloud
	//var dbConnCloud = [type="sql", instance="database-1", dbName="companyFunding", user="root", password=""] on cloud
	
	for x in columns{
		var queryStrAvg = "SELECT AVG(temperatura) FROM temperaturacomune WHERE provincia = \\\"" + x[0] as String + "\\\""
		
		var queryStmtAvg = [type="query", query_type="value", connection=dbConnCloud, statement=queryStrAvg]
	
		var avg = queryStmtAvg.execute()

		var queryStrIns = "INSERT INTO temperaturaprovincia (temperatura, provincia) VALUES ( \\\"" + avg + "\\\", \\\"" + x[0] as String + "\\\")"
		
		var queryStmtIns = [type="query", query_type="update", connection=dbConnCloud, statement=queryStrIns]
	
		queryStmtIns.execute()
	}
}
```

### Check insertion Function 

The check insertion function prints the database after the updates in order to check if the insertion has been correctly executed.
The Fly code is the following:

``` 
func checkIns (){  
	var dbConnCloud = [type="sql", resourceGroup="", instance="", dbName="companyFunding", user="", password=""] on cloud
	//var dbConnCloud = [type="sql", instance="", dbName="companyFunding", user="root", password=""] on cloud
	var newTable = [type="dataframe", table_name="temperaturaprovincia", source=dbConnCloud]
	
	println newTable
}
```


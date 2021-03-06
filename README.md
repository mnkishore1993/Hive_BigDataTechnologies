# Hive_BigDataTechnologies
 
### Connect to EMR  

	ssh hadoop@ec2-3-83-4-13.compute-1.amazonaws.com -i C:/BigDataTechnologies/emr-key-pair.pem

### HIVE Commands:



- Copy HQL.zip to local content folder

			scp -i C:/BigDataTechnologies/emr-key-pair.pem C:/BigDataTechnologies/hql.zip hadoop@ec2-3-83-4-13.compute-1.amazonaws.com:/home/hadoop
			
- Start Hive console

			Go to corresponding directory "cd home/hadoop/hql"
			And Enter 
			"hive" 
			to open hive console and to exit console use 
			Ctrl + C
			
	- Create MyDb database

			CREATE DATABASE IF NOT EXISTS MyDb;
			
	- Set our database as default:
			
			use MyDb;
			
	- Create Table with column Comments (comments are optional - commnet and value can be removed)
		
				CREATE TABLE IF NOT EXISTS foodratings(
				name STRING COMMENT 'NameComment',
				food1 INTEGER COMMENT 'food1Comment',
				food2 INTEGER COMMENT 'food2Comment',
				food3 INTEGER COMMENT 'food3Comment',
				food4 INTEGER COMMENT 'food4Comment',
				id INTEGER COMMENT 'IdComment')
				COMMENT 'FoodratingTableComment'
				ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
				STORED AS TEXTFILE;
				
- Drop Table 
		
			DROP TABLE IF EXISTS foodratings;
			
- Describe existing table
		
			DESCRIBE FORMATTED MyDb.foodratings;
			
- Load data into table
		
			LOAD DATA LOCAL INPATH './foodratings89779.txt' OVERWRITE INTO TABLE foodratings;
			
- Select data from table
		
			SELECT avg(food3), min(food3), max(food3) 
			FROM foodratings;
			
- Create Partition table

			CREATE TABLE IF NOT EXISTS foodratingspart (
			food1 INTEGER,
			food2 INTEGER,
			food3 INTEGER,
			food4 INTEGER,
			id INTEGER)
			PARTITIONED BY (name STRING);

			
	- 	Load data into partion table from existing table
		
			INSERT OVERWRITE TABLE foodratingspart
			PARTITION (name)
			SELECT food1,food2,food3,food4,id,name
			FROM foodratings;
			
	

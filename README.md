# Socail networking site for IOT devices

One Paragraph of project description goes here

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

You need Ubuntu or any unix based  machine to run this project


### Setting up the enviroment
#### 1. Install and configure PostgreSQL on Debian/Ubuntu

Update your system to the latest available version in the repository
```
$  sudo apt-get update
```
 Install PostgreSQL using apt-get
```
$  sudo apt-get install postgresql postgresql-contrib
```
Creat user
```
$  sudo -u postgres createuser --interactive --pwprompt
```
```
Output:
Enter name of role to add: dspot
Enter password for new role:dspot 
Enter it again: dspot
Shall the new role be a superuser? (y/n) y
```
Create Database under dspot user

```
$  sudo -u postgres createdb -O dspot dspot_db


```
#### 2. Install and Django on Debian/Ubuntu

Install django using pip
```
$ sudo pip install django
```
Install django module for postgresql
```
$  pip install psycopg2
```


## Building and Running
### 1. Building and Running--Tha main django server

To clone this project use git
```
$  git clone https://github.com/attaakkhan/Dspot-FYP-2016.git

```
Navigate to dspot directory.
```
$ cd Dspot-FYP-2016/Dspot/Dspot
```
Now migrate the changes to Postresql
```
$ python manage.py migrate
```
Run The Server
```
$ python manage.py runserver
```
Now the server is running open http://127.0.0.1:8000/register/ in your Web Browser you will see the site

Following is the sample of log generated and sent to kafka servers
```
Logs:`
{"time":"2018-09-15 10:25:02.249","type":"delete","Person":"{\"name\":\"Name101\",\"role\":\"user\",\"id\":101,\"age\":50}"}
{"time":"2018-09-15 10:25:02.249","type":"delete","Person":"{\"name\":\"Name102\",\"role\":\"user\",\"id\":102,\"age\":50}"}
{"time":"2018-09-15 10:25:02.25","type":"delete","Person":"{\"name\":\"Name103\",\"role\":\"user\",\"id\":103,\"age\":50}"}
{"time":"2018-09-15 10:25:02.25","type":"delete","Person":"{\"name\":\"Name104\",\"role\":\"user\",\"id\":104,\"age\":50}"}
{"time":"2018-09-15 10:25:02.25","type":"delete","Person":"{\"name\":\"Name105\",\"role\":\"user\",\"id\":105,\"age\":50}"}
{"time":"2018-09-15 10:25:02.251","type":"delete","Person":"{\"name\":\"Name106\",\"role\":\"user\",\"id\":106,\"age\":50}"}
{"time":"2018-09-15 10:25:02.251","type":"delete","Person":"{\"name\":\"Name107\",\"role\":\"user\",\"id\":107,\"age\":50}"}
{"time":"2018-09-15 10:25:02.251","type":"delete","Person":"{\"name\":\"Name108\",\"role\":\"user\",\"id\":108,\"age\":50}"}
{"time":"2018-09-15 10:25:02.252","type":"delete","Person":"{\"name\":\"Name109\",\"role\":\"user\",\"id\":109,\"age\":50}"}
{"time":"2018-09-15 10:25:02.252","type":"delete","Person":"{\"name\":\"Name110\",\"role\":\"user\",\"id\":110,\"age\":50}"}
{"time":"2018-09-15 10:25:02.252","type":"delete","Person":"{\"name\":\"Name111\",\"role\":\"user\",\"id\":111,\"age\":50}"}
{"time":"2018-09-15 10:25:02.253","type":"delete","Person":"{\"name\":\"Name112\",\"role\":\"user\",\"id\":112,\"age\":50}"}
{"time":"2018-09-15 10:25:02.253","type":"delete","Person":"{\"name\":\"Name113\",\"role\":\"user\",\"id\":113,\"age\":50}"}
{"time":"2018-09-15 10:25:02.253","type":"delete","Person":"{\"name\":\"Name114\",\"role\":\"user\",\"id\":114,\"age\":50}"}
{"time":"2018-09-15 10:25:02.254","type":"delete","Person":"{\"name\":\"Name115\",\"role\":\"user\",\"id\":115,\"age\":50}"}
............

```

Log are genrated and sent to kafka servers, Its time to build the etl consumer to transform these logs and load to psql run:

```
$  cd ../ConsumerETL/
$  mvn package

```
Run the ETL Consumer

```
$ java -jar target/ConsumerETL.jar
```
Now the log has been tarnformed and loaded to psql Database.

Here is the activity table in Psql
```
 equip_id |  type  |  name   | role  |          time           | id  
----------+--------+---------+-------+-------------------------+-----
     1769 | login  | Name0   | admin | 2018-09-15 10:45:00.906 |   0
     1770 | login  | Name1   | admin | 2018-09-15 10:45:01.031 |   1
     1771 | login  | Name2   | admin | 2018-09-15 10:45:01.032 |   2
     1772 | login  | Name3   | admin | 2018-09-15 10:45:01.033 |   3
     .
     .
     .
        1904 | update | Name135 | user  | 2018-09-15 10:45:01.124 | 135
     1905 | update | Name136 | user  | 2018-09-15 10:45:01.124 | 136
     1906 | update | Name137 | user  | 2018-09-15 10:45:01.125 | 137
     1907 | update | Name138 | user  | 2018-09-15 10:45:01.126 | 138
     1908 | update | Name139 | user  | 2018-09-15 10:45:01.126 | 139
(140 rows)
```
And the login table in Psql
```
 equip_id |  name  | role  |          time           | id | age 
----------+--------+-------+-------------------------+----+-----
      335 | Name0  | admin | 2018-09-15 10:43:15.486 |  0 |  50
      336 | Name1  | admin | 2018-09-15 10:43:15.609 |  1 |  50
      337 | Name2  | admin | 2018-09-15 10:43:15.061 |  2 |  50
      338 | Name3  | admin | 2018-09-15 10:43:15.061 |  3 |  50
      339 | Name4  | admin | 2018-09-15 10:43:15.611 |  4 |  50
    .
    .
    .
    .
    .
    
      363 | Name28 | admin | 2018-09-15 10:43:15.627 | 28 |  50
      364 | Name29 | admin | 2018-09-15 10:43:15.628 | 29 |  50
(30 rows)

```

# Project Title

One Paragraph of project description goes here

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

What things you need to install the software and how to install them

```
Give examples
```

### Setting the enviroment for the ETL
#### 1. Install and configure Kafka servers on Debian/Ubuntu

##### Step 1- Install Java 
Update your system to the latest available version in the repository
```
$  sudo apt-get update
```
Apache Kafka requires java runtime environment, install it using apt-get
```
$ sudo apt-get install default-jre
```

##### Step 2- Install Zookeeper
Kafka servers depend on zookeeper to coordinate, and we will use Apache zookeeper, which is an open source service used to manage information among distributed servers. Install zookeeper using apt-get
```
$  sudo apt-get install zookeeperd 
```
After installing, it will run automatically listening on port 2181, to test it run:
```
$  telnet localhost 2181
```
At the prompt type 'ruok' and if it returns 'imok' then everything is working well.

Optionally, to check the zookeeper status use the following command
```
$ sudo systemctl status zookeeper
```
if zookeeper is not running, use the following command to activate the zookeeper
```
$ sudo systemctl enable zookeeper
```

##### Step 2- Download and install Apache kafka
Navigate to ~/Downloads/ directory to download Kafka binaries
```
$ cd ~/Downloads 
```
Download Kafka 2.0 using wget
```
$  wget http://www-us.apache.org/dist/kafka/2.0.0/kafka_2.11-2.0.0.tgz 
```
Now create a directory Kafka in the /opt directory
```
$  sudo mkdir /opt/Kafka
```
Extract Kafka binaries to /opt/kafka directory
```
$ sudo tar xvzf kafka_2.11-2.0.0.tgz -C /opt/Kafka

```
To view, the kafka Path use the following command
```
$  ls /opt/Kafka 
```
To add Kafka path to the system path, open /etc/profile using nano
```
$ sudo nano /etc/profile
```
Add the following lines to the end of the file, and then press ctrl+o to save and then press ctrl+x to exit
```
export KAFKA_PATH="/opt/Kafka/kafka_2.11-2.0.0"
export PATH="$PATH:${KAFKA_PATH}/bin"
```
Also, open  ~/.bashrc directory
```
$  sudo nano ~/.bashrc
```
And add the following lines to the end of the file, and then press ctrl+o to save and then press ctrl+x to exit
```
alias sudo='sudo env PATH="$PATH"'
```
Finally, reboot your system
```
$  sudo reboot
```
After the system starts, make a link to the Kafka server.properties file where configurations for the Kafka server  are stored
```
$ sudo ln -s $KAFKA_PATH/config/server.properties /etc/kafka.properties
 ```
Finally to run kafka server run the following command
```
$  sudo kafka-server-start.sh /etc/kafka.properties
```

##### Step 2- Testing Apache kafka using Terminal
To test Apache kafka, open a new terminal tab and create a test topic using the following command
```
$  sudo kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1   --topic testTopic --partitions 1
```
Now to publish messages, use the follwing command. After running the command an arrow(>) will appear
```
$  sudo kafka-console-producer.sh --broker-list localhost:9092 --topic testTopic
```
To Consume messages, Open a new terminal tab and  use the following command
```
$  sudo kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic testTopic --from-beginning
```
Now type 'Hello' on the producer Terminal tab and you will also be able to see it on the consumer terminal tab.
```



### Installing
#### 1. Install and configure Kafka servers on Debian/Ubuntu

Kafka servers are distributed messeging  servers
##### Step 1- Install Java 
Update your system to the latest available version in the repository
```
$ sudo apt-get update
```
Apache Kafka requires java runtime environment, install using apt-get
```
$ sudo apt-get install default-jre
```

##### Step 2- Install Zookeeper
Kafka servers depend on zookeeper to coordinate, and we will use Apache zookeeper, which is an open source service used to manage information among distributed servers. Install zookeeperd using apt-get
```
$  sudo apt-get install zookeeperd 
```
After installing it will run automatically listening on port 2181, to test it run:
```
$  telnet localhost 2181
```
At the prompt type 'ruok' and if it returns 'imok' then everything is working well.

Optionally, to check the zookeeper status use the followin command
```
$ sudo systemctl status zookeeper
```
if zookeeper is not running , use the following commant to activate the zookeeper
```
$ sudo systemctl enable zookeeper
```
##### Step 2- Download and install Apache kafka
Navigate to ~/Downloads/ directory to download Kafka binaries
```
$ cd ~/Downloads 
```
Download Kafka 2.0 using wget
```
$  wget http://www-us.apache.org/dist/kafka/2.0.0/kafka_2.11-2.0.0.tgz 
```
```
$ cd ~/Downloads 
```
```
$ cd ~/Downloads 
```
```
$ cd ~/Downloads 
```
```
$ cd ~/Downloads 
```


### Installing
#### 1. Install and configure Kafka servers on Debian/Ubuntu
### Installing
#### 1. Install and configure Kafka servers on Debian/Ubuntu

Kafka servers are distributed messeging  servers
##### Install Java
Update your system to the latest available version in the repository
```
$ sudo apt-get update
```
Apache Kafka requires java runtime envirment, install using apt-get
```
$ sudo apt-get install default-jre
```
Say what the step will be

```
Give the example
```

And repeat

```
until finished
Kafka servers are distributed messaging servers and 

Say what the step will be

```
Give the example
```

And repeat

```
until finished
```
#### 2. Install and configure Kafka servers on Debian/Ubuntu
#### 3. Install and configure Kafka servers on Debian/Ubuntu
End with an example of getting some data out of the system or using it for a little demo

## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why
![Screenshot](im/aa.png)

```
Give an example
```

## Deployment

Add additional notes about how to deploy this on a live system

## Built With

* [Dropwizard](http://www.dropwizard.io/1.0.2/docs/) - The web framework used
* [Maven](https://maven.apache.org/) - Dependency Management
* [ROME](https://rometools.github.io/rome/) - Used to generate RSS Feeds

## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone whose code was used
* Inspiration
* etc


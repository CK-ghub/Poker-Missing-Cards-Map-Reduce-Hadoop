# Poker-Missing-Cards-Map-Reduce-Hadoop
In this program, we will use a MapReduce-based approach to find all the missing Poker cards from the deck of cards listed in 'input.txt' using Java running in a Hadoop system. The list of missing cards is stored in the output folder of HDFS.

With the help of the following steps and commands, you can execute and test the program. I ran this on an EC2 instance configured with Ubuntu and Hadoop setup in pseudo-distributed mode. 

## Prerequisites: 
<li>Java installed</li>	
<li>Hadoop installed and setup</li>	
<br>
1) To place any file from your local onto EC2 instance: 
scp -i Ec2_instance_key.pem path/to/your/file ubunt@IPv4address:/home/ubuntu

To place any file from EC2 instance onto your local, open terminal on your local and type:
scp -i Ec2_instance_key.pem ubuntu@54.147.131.153:path/to/your/file/on/ec2 .

The '.' represents the current directory. 

2) Once you transfer the MissingCards.java and input.txt files onto the EC2 instance, we need to compile the classes and create a jar file. 

3) Command to compile the code:
javac -classpath ``hadoop classpath`` -d MissingCards MissingCards.java

4) Command to add all Class files in the MissingCards directory from step 3 to jar:
jar -cvf MissingCards.jar -C MissingCards/ .

5) Command to list directories in HDFS: hadoop fs -ls

6) Command to put input file in HDFS: hadoop fs -copyFromLocal input.txt /input/

This puts the 'input.txt' file in the input folder of HDFS. If you don't have a folder already. Create one in HDFS for storing the input file.

7) Command to create an input folder in HDFS: hadoop fs -mkdir /input

8) Once the txt file is placed. You can execute the jar file in hadoop using the following command:
hadoop jar MissingCards.jar MissingCards /input/ /output/

You have to specify the name of the jar file, the main class, and input and output directories.

5) To view the output, use the following command to access the output in output folder of HDFS:
hadoop fs -cat /output/part-r-00000

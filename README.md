# OS-for-Big-Data-and-Hadoop
----------------------------------

# Pre-requisites

Please use the recommended VM because there are numerous challenges with building and running this code (and Hadoop in general) on Windows. 

## Recommended Virtual Machine

Install the supplied Virtual Machine and [Virtualbox](https://www.virtualbox.org/wiki/Downloads). 

You may also get the Virtual Machine from this link (5.3 GB), but keep in mind that you'll need at least 4 GB for it:

[click here](https://downloads.cloudera.com/demo_vm/virtualbox/cloudera-quickstart-vm-5.13.0-0-virtualbox.zip)

## You can do it on your own linux machine (for those struggling with the Hadoop VM) 

You can get a recent Linux image and instal it locally or in a virtual machine here:

[click here](https://ubuntu.com/download/desktop/thank-you?version=20.04.2.0&architecture=amd64)



After you've finished installing, open a terminal and type:

    sudo apt install openjdk-8-jdk mvn
    sudo apt install python3

WARNING: Double-check that you're running Java 8!

- Check that your Java installation is correct and that the JAVA HOME variable is set.
- Get a competent editor or a Java IDE (IntelliJ or Eclipse).
- If you don't already have Maven, instal it; if you're using Eclipse, make sure you have the most recent version or instal the m2e plugin to import the maven project.

# Part 1

Clone this repository.

    git clone https://github.com/iemejia/formation-bigdata

1. Complete the implementation of Wordcount as shown in the class and test that it functions properly.

You can use your own file or download a book from the Gutenberg project; the example file dataset/hamlet.txt is also available.

2. Change the implementation to only return words that begin with the letter'm.'

- Did you make the modification in the mapper or the reducer?
- What are the ramifications of modifying each one's code?
- Compare the results of the Hadoop counters and explain which technique is the best.

## First steps in Hadoop HDFS (Inside the Cloudera VM)

We're going to perform the course's wordcount example, therefore we'll need to add the file to the distributed file system first.
So, first, we must login to the master server (again, using ssh) and perform the following:

    hadoop fs -mkdir hdfs:///user/id##/dataset/wordcount/

or

    hadoop fs -mkdir hdfs:///user/gcn##/dataset/wordcount/

depending on your master's and group's preferences (##).

Upload the file

    hadoop fs -put hamlet.txt hdfs:///user/id##/dataset/wordcount/

Verify the upload

    hadoop fs -ls hdfs:///user/id##/dataset/wordcount/

This one is for distant IP addresses and includes the corresponding mapping (port 8020 or 9000)

    hadoop fs -ls hdfs://172.17.0.2/tp1/

You can look at the web interfaces for the clusters here:

Resource Manager - http://172.17.0.2:8088/
HDFS Name Node - http://172.17.0.2:50070/

## Using the YARN cluster to run a mapreduce job

The programme should be copied to the cluster.

The structure is as follows:

    hadoop jar JAR_FILE CLASS input output

    hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples*.jar wordcount hdfs:///user/id00/dataset/wordcount/hamlet.txt hdfs:///user/id00/output/wordcount/

The hadoop mapreduce examples is available in the following path in the cluster:

    /usr/lib/hadoop-mapreduce/hadoop-mapreduce-examples.jar

Verify the output

    hadoop fs -cat hdfs:///user/id00/output/wordcount/*

If the IP address is 172.17.0.2, for example, the following are the addresses for the various web interfaces (this applies to both the VM and the Cluster):

- NameNode http://172.17.0.2:50070/
- ResourceManager http://172.17.0.2:8088/
- MapReduce JobHistory Server http://172.17.0.2:19888/
- Hue http://172.17.0.2:8888/

## References

- https://developer.yahoo.com/hadoop/tutorial/
- http://blog.cloudera.com/blog/2009/08/hadoop-default-ports-quick-reference/


# Part 2

3. Use the GDELT dataset and a Map Reduce task to identify the top 10 nations with the most news relevance over a particular time period (one week, one day, one month).

More information on the gdelt column format can be found at:
[click here](http://data.gdeltproject.org/documentation/GDELT-Data_Format_Codebook.pdf)

You can test your implementation with a small test sample of the dataset at dataset/gdeltmini/20160529.export.csv.

You can also download the full datasets from:
[click here](http://data.gdeltproject.org/events/index.html)

We'll count the significance of an event based on its NumMentions column, and we'll use the country code as a three-letter identification (Actor1CountryCode).
As a result, this becomes a WordCount, with the Top 20 determined by counting the NumMentions of each event per country.


On the GDELT file format, Actor1CountryCode is column 7 and NumMentions is column 31.


If you're using Hadoop, Is it possible to add a combiner to the job? Do you think the counters have improved? Explain and contrast the numbers. What could possibly go wrong?


# Part 3 (Spark)

A current Linux installation is required. You can utilise the lab computers or install a VM using Ubuntu >= 18.04 (available in the class) (if you choose this route pay attention to paths that are unreadable in the machine in particular the one where you instal the project).

## Setup of the Environment

Create a python virtualenv

    python -m venv spark-env

Activate the venv

    source spark-env/bin/activate

Upgrade setup tools

    pip install --upgrade pip setuptools wheel

Install dependencies

    pip install pyspark jupyter ipython black

## You can now use pyspark to do so by selecting one of three choices (you choose one): 

- Interactive Python (ipython) REPL [RECOMMENDED]

    ipython

- Interactive Notebook

    jupyter notebook

- Python editor / IDE

If you use VS Code you must install the Python extension from the extension section.

    code .

For more visit to their documentation page and see the examples they have used to understand in a better way !!

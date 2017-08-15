---
title: Launch Apache Spark on AWS EC2 and Initialize SparkR Using RStudio
author: emaasit
date: 2015-11-10 09:41:40+00:00
categories:
  - Apache Spark
  - Big Data
  - Data Science
  - R
  - RStudio
  - SparkR
slug: launch-apache-spark-on-aws-ec2-and-initialize-sparkr-using-rstudio
summary: 'In this blog post, we shall learn how to launch a Spark stand alone cluster on Amazon Web Services (AWS) Elastic Compute Cloud (EC2) for analysis of Big Data. This is a continuation from our previous blog, which showed us how to download Apache Spark and start SparkR locally on windows OS and RStudio'
---

**Introduction**

![sparkr-ec2](/img/sparkr-ec2.jpg)

In this blog post, we shall learn how to launch a Spark stand alone cluster on [Amazon Web Services (AWS) Elastic Compute Cloud (EC2)](http://aws.amazon.com/) for analysis of Big Data. This is a continuation from our [previous blog](https://danielemaasit.com/post/2015/07/26/installing-and-starting-sparkr-locally-on-windows-os-and-rstudio/), which showed us how to download [Apache Spark](http://spark.apache.org/) and start SparkR locally on windows OS and [RStudio](https://www.rstudio.com/).

We shall use _Spark 1.5.1_ (released on October 02, 2015) which has a _spark-ec2_ script that is used to install stand alone Spark on AWS EC2.  A nice feature about this _spark-ec2_ script is that it installs RStudio server as well. This means that you don't need to install RStudio server separately. Thus you can start working with your data immediately after Spark is installed.

**Prerequisites**

	
  * You should have already downloaded [Apache Spark](http://spark.apache.org/) onto your local desktop from the [official site](http://spark.apache.org/). You can find instructions on how to do so in our [previous post](http://blog.sparkiq-labs.com/2015/07/26/installing-and-starting-sparkr-locally-on-windows-os-and-rstudio/).

	
  * You should have an AWS account, created secret access key(s) and downloaded your private key pair as a .pem file. Find instructions on how to create your access keys [here](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html#Using_CreateAccessKey) and to download your private keys [here](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-key-pairs.html#having-ec2-create-your-key-pair).

	
  * We will launch the clusters through [Bash shell](http://www.gnu.org/software/bash/manual/bashref.html) on Linux. If you are using Windows OS I recommend that you install and use the [Cygwin](http://www.cygwin.com/) terminal (It provides functionality similar to a Linux distribution on Windows)


**Launching Apache Spark on AWS EC2**

We shall use the _spark-ec2_ script, located in Spark's _ec2_ directory to launch, manage and shutdown Spark clusters on Amazon EC2. It will setup Spark, HDFS, Tachyon, RStudio on your cluster.

**Step 1: Go into the ec2 directory**

Change directory into the "_ec2"_ directory. In my case, I downloaded Spark onto my desktop, so I ran this command.

`$ cd Desktop/Apache/spark-1.5.1/ec2`

[![1-cd](https://sparkiqlabs.files.wordpress.com/2015/11/1-cd.png?w=300)](https://sparkiqlabs.files.wordpress.com/2015/11/1-cd.png)

**Step 2: Set environment variables**

Set the environment variables `AWS_ACCESS_KEY_ID` and `AWS_SECRET_ACCESS_KEY` to your Amazon EC2 access key ID and secret access key.

`$ export AWS_SECRET_ACCESS_KEY=AaBbCcDdEeFGgHhIiJjKkLlMmNnOoPpQqRrSsTtU`

`$ export AWS_ACCESS_KEY_ID=ABCDEFG1234567890123`

**Step 3: Launch the spark-ec2 script**

Launch the cluster by running the following command.

`$ ./spark-ec2 --key-pair=awskey --identity-file=awskey.pem --region=us-east-1 --instance-type=c3.4xlarge -s 2 --copy-aws-credentials launch test-cluster` 

[![2-launch](https://sparkiqlabs.files.wordpress.com/2015/11/2-launch.png?w=300)](https://sparkiqlabs.files.wordpress.com/2015/11/2-launch.png)

Where;



	
  * --key-pair=<name_of_your_key_pair> , The name of your EC2 key pair

	
  * --identity-file=<name_of_your_key_pair>.pem , The private key file

	
  * --region=<the_region_where_key_pair_was_created>

	
  * --instance-type=<the_instance_you_want>

	
  * -s N, where N is the number of slave nodes

	
  * "test-cluster" is the name of the cluster


In case you want to set other options for the launch of your cluster, further instructions can be found on the [Spark documentation website](http://spark.apache.org/docs/latest/ec2-scripts.html).

As I mentioned earlier, this script also installs RStudio server, as can be seen in the figure below.

[![3-install-rstudio](https://sparkiqlabs.files.wordpress.com/2015/11/3-install-rstudio.png?w=300)](https://sparkiqlabs.files.wordpress.com/2015/11/2-launch-awsscreen.png)

The cluster installation takes about 7 minutes. When it is done, the host address of the master node is displayed at the end of the log message as shown in the figure below. At this point your Spark cluster has been installed successfully and you are a ready to start exploring and analyzing your data.

![4-done](https://sparkiqlabs.files.wordpress.com/2015/11/4-done.png?w=300)

Before you continue, you may be curious to see whether your cluster is actually up and running. Simply log into your AWS account and go to the EC2 dashboard. In my case, I have 1 master node and 2 slave/worker nodes in my Spark cluster.

[![2-launch-awsScreen](https://sparkiqlabs.files.wordpress.com/2015/11/2-launch-awsscreen.png?w=300)](https://sparkiqlabs.files.wordpress.com/2015/11/2-launch-awsscreen.png)

Use the address displayed at the end of the launch message and access the Spark User Interface (UI) on port 8080. You can also get the host address of your master node by using the "_get-master_" option in the command below.

`$ ./spark-ec2 --key-pair=awskey --identity-file=awskey.pem get-master test-cluster`

[![5-online](https://sparkiqlabs.files.wordpress.com/2015/11/5-online.png?w=300)](https://sparkiqlabs.files.wordpress.com/2015/11/5-online.png)

**Step 4: Login to your cluster**

In the terminal you can login to your master node by using the "_login_" option in the following command

`$ ./spark-ec2 --key-pair=awskey --identity-file=awskey.pem login test-cluster`

[![6-login](https://sparkiqlabs.files.wordpress.com/2015/11/6-login.png?w=300)](https://sparkiqlabs.files.wordpress.com/2015/11/6-login.png)

**Step 5 (Optional): Start the SparkR REPL**

Here you can actually start the SparkR REPL by typing the following command.

`$ spark/bin/sparkR`

[![7-start-sparkr](https://sparkiqlabs.files.wordpress.com/2015/11/7-start-sparkr.png?w=300)](https://sparkiqlabs.files.wordpress.com/2015/11/7-start-sparkr.png)

SparkR will be initialized and you should see a welcome message as shown in the Figure below. Here you can actually start working with your data. However most R users, like myself, would like to work in an Integrated Development Environment (IDE) like RStudio. See steps 6 and 7 on how to do so.

[![8-welcome-sparkr](https://sparkiqlabs.files.wordpress.com/2015/11/8-welcome-sparkr.png?w=300)](https://sparkiqlabs.files.wordpress.com/2015/11/8-welcome-sparkr.png)

**Step 6: Create user accounts**

Use the following command to list all available users on the cluster.

`$ cut -d: -f1 /etc/passwd`

[![9-users](https://sparkiqlabs.files.wordpress.com/2015/11/9-users.png?w=300)](https://sparkiqlabs.files.wordpress.com/2015/11/9-users.png)

You will notice that "rstudio" is one of the available user accounts. You can create other user accounts and passwords for them using these commands.

`$ sudo adduser daniel`

`$ passwd daniel`

In my case, I used the "rstudio" user account and changed its password.

[![10-create-passwd](https://sparkiqlabs.files.wordpress.com/2015/11/10-create-passwd.png?w=300)](https://sparkiqlabs.files.wordpress.com/2015/11/10-create-passwd.png)

**Initializing SparkR Using RStudio**

The _spark-ec2_ script also created a "_startSpark.R_" script that we shall use to initialize SparkR.

**Step 7: Login to RStudio server**

Using the username you selected/created and the password you created, login into RStudio server.

[![11-rstudio](https://sparkiqlabs.files.wordpress.com/2015/11/11-rstudio.png?w=300)](https://sparkiqlabs.files.wordpress.com/2015/11/11-rstudio.png)

**Step 8: Initialize SparkR**

When you log in to RStudio server, you will see the "startSpark.R" in your files pane (already created for you).

[![12-startSparkR](https://sparkiqlabs.files.wordpress.com/2015/11/12-startsparkr.png?w=300)](https://sparkiqlabs.files.wordpress.com/2015/11/12-startsparkr.png)

Simply run the "startSpark.R" script to initialize SparkR. This creates a Spark Context and a SQL Context for you.

[![13-initialize](https://sparkiqlabs.files.wordpress.com/2015/11/13-initialize.png?w=300)](https://sparkiqlabs.files.wordpress.com/2015/11/13-initialize.png)

**Step 9: Start Working with your Data**

Now you are ready to start working with your data.

Here I use a simple example of the "mtcars" dataset to show that you can now run SparkR commands and use the MLLib library to run a simple linear regression model.

[![14-lm-example](https://sparkiqlabs.files.wordpress.com/2015/11/14-lm-example.png?w=300)](https://sparkiqlabs.files.wordpress.com/2015/11/14-lm-example.png)

You can view the status of your jobs by using the host address of your master and listening on port 4040. This UI also displays a chain of RDD dependencies organized in Direct Acyclic Graph (DAG) as shown in the figure below.

[![15-DAG](https://sparkiqlabs.files.wordpress.com/2015/11/15-dag.png?w=222)](https://sparkiqlabs.files.wordpress.com/2015/11/15-dag.png)

**Final Remarks**

The objective of this blog post was to show you how to get started with Spark on AWS EC2 and initialize SparkR using RStudio. In the next blog post we shall look into working with actual "Big" datasets stored in different data stores such as [Amazon S3](https://aws.amazon.com/s3/) or [MongoDB](https://www.mongodb.com/).

**Further Interests: RStudio Shiny + SparkR**

I am curious about how to use [Shiny](http://shiny.rstudio.com/) with SparkR and in the next couple of days I will investigate this idea further. The question is: how can one use SparkR to power shiny applications. If you have any thoughts please share them in the comments section below and let's discuss.

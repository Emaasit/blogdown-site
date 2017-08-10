---
title: Installing and Starting SparkR Locally on Windows OS and RStudio
author: emaasit
date: 2015-07-26 09:11:00+00:00
categories:
  - Apache Spark
  - Big Data
  - R
  - RStudio
  - SparkR
slug: installing-and-starting-sparkr-locally-on-windows-8-1-and-rstudio
---

**Introduction**

With the recent release of Apache Spark 1.4.1 on July 15th, 2015, I wanted to write a step-by-step guide to help new users get up and running with SparkR locally on a Windows machine using command shell and RStudio. SparkR provides an R frontend to Apache Spark and using Spark’s distributed computation engine allows R-Users to run large scale data analysis from the R shell. The steps listed here **WILL** also be documented in my upcoming online book titled "[Getting Started with SparkR for Big Data Analysis](http://www.danielemaasit.com/getting-started-with-sparkr/)" which can be accessed at: [http://www.danielemaasit.com/getting-started-with-sparkr/](http://www.danielemaasit.com/getting-started-with-sparkr/). These steps will get you up and running in less than 5 mins.

Make sure you have Java 6+ installed on your computer and the system environments set.

**Step 1: Download Spark**

Open your web browser and open this web page: [http://spark.apache.org/](http://spark.apache.org/). This is the official website for the Apache Spark project. You should see a large green button to the right of the page that reads "Download Spark", as shown in Figure 1. Click the green button.

{{< figure src="/img/greenbutton.png" title="Apache Spark home page" >}}

Clicking the green button will take you to the download page as shown in Figure 2 below.

{{< figure src="/img/2-downloadpage.png" title="The download page" >}}

You should follow the steps 1 to 3 to create a download link for a Spark Package of your choice. On the _"2. Choose a package type"_ option, select any pre-built package type from the drop-down list (Figure 3). Since we want to experiment locally on windows, a pre-built package for Hadoop 2.6  and later will suffice.

{{< figure src="/img/3-prebuilt.png" title="Choose a package type" >}}

On the _"3. Choose a download type" _option, select "Direct Download" from the drop-down list (Figure 4).

{{< figure src="/img/4-downloadtype.png" title="Choose a download type" >}}

After selecting the download type, a link is created next to the option _"4. Download Spark"_ (Figure 5). Click this link to download Spark.

{{< figure src="/img/5-download.png" title="Click the download link" >}}

Save the zipped file to your computer (Figure 6).

{{< figure src="/img/6-save.png" title="Save to your computer" >}}

**Step 2: Unzip Built Package**

Unzip and save the files to a directory folder of your choice. In Figure 7 below, I chose to save to _"C:/Apache/Spark-1.4.1"_.

{{< figure src="/img/7-unzippedfiles.png" title="List of Files in unzipped folder" >}}


**Step 3: Run in Command Prompt**

Now start your favorite command shell and change directory to your Spark folder as shown in Figure 8.

{{< figure src="/img/8-startcmd.png" title="Start command prompt and change directory" >}}


To start SparkR, simply run the command `".\bin\sparkR"` on the top-level Spark directory as shown in Figure 9 below.

{{< figure src="/img/9-startsparkr.png" title="Start SparkR" >}}

You will see logs on your screen that should take at most 15 seconds to launch SparkR. If everything ran smoothly you should see a welcome message that reads "Welcome to SparkR!" as shown in Figure 10.

{{< figure src="/img/10-ready.png" title="Welcome to SparkR!" >}}

At this point you are ready to start prototyping with SparkR on the command shell. Note that a Spark context and a SQL Context have been initialized for you as "_sc_" and "_sqlContext_" respectively. You can now start experimenting using the example shown in **Step 4.5**.

**Running in RStudio**

While using SparkR in the command shell is good for quickly getting started, most R users typically use an Integrated Development Environment (IDE) like RStudio for development and running production ready code. Step 4 below will guide you to get started using SparkR in RStudio.

**Step 4: Run in RStudio**



	
  * **Step 4.1: Set System Environment**


Once you have opened RStudio, you need to set the system environment first. You have to point your R session to the installed version of SparkR. Use the code shown in Figure 11 below but replace the _**SPARK_HOME**_ variable using the path to your Spark folder. Mine is "C:/Apache/Spark-1.4.1".

{{< figure src="/img/1-setenv.png" title="Set System Environment Variable" >}}


  * **Step 4.2: Set the Library Paths**


Second, you have to set the library path for Spark a shown in Figure 12 below.

{{< figure src="/img/12-libpaths.png" title="Set the Library Path" >}}


  * **Step 4.3: Load SparkR Library**


Next, you can now load SparkR just as you would any other R library using the `library()` command as shown in Figure 13.

{{< figure src="/img/13-loadsparkr.png" title="Load the SparkR library" >}}


  * **Step 4.4: Initialize Spark Context and SQL Context**


Initialize SparkR by creating a Spark context using the command `sparkR.init()`. The argument in this command is _master = "local[N]"_, where _N_ stands for the number of threads that you want to use.

Also, you need to create a SQL context to be able to work with DataFrames (the main abstraction in SparkR). Use the command `sparkRSQL.init()` to create a SQL context from your Spark context as shown in Figure 14.

{{< figure src="/img/14-sc.png" title="Initialize Spark Context and SQL Context" >}}

When you run the above commands (From step 4.1 to 4.4), this invokes the "spark-submit" script that launches java, as shown in Figure 15. If this runs successfully, your Spark context and SQL context should be created and at this stage you should be able to start experimenting with SparkR.

{{< figure src="/img/15-ready.png" title="All set" >}}


  * **Step 4.5: A Quick Example**


You can start experimenting with SparkR on the command shell and in RStudio using the example provided below. You can monitor your Spark jobs using the Spark UI at [localhost:4040](http://localhost:4040/)

https://gist.github.com/a25c41abe15a75c76e42

**Final Remarks**

The purpose of this blog post was to get you up and running quickly with SparkR locally on a personal computer. In the next blog post, I will show you how to use SparkR on a cloud computing framework like [Amazon Elastic Compute Cloud](http://aws.amazon.com/ec2/) (EC2) to manipulate large datasets with millions of records.

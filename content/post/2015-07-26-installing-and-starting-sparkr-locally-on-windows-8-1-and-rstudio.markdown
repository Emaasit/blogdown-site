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

<!-- more -->

**Prerequisite**

Make sure you have Java 6+ installed on your computer and the system environments set.

**Step 1: Download Spark**

Open your web browser and open this web page: [http://spark.apache.org/](http://spark.apache.org/). This is the official website for the Apache Spark project. You should see a large green button to the right of the page that reads "Download Spark", as shown in Figure 1. Click the green button.

[caption id="attachment_48" align="aligncenter" width="800"][![Apache Spark home page](https://emaasit.files.wordpress.com/2015/07/greenbutton.png)](https://emaasit.files.wordpress.com/2015/07/greenbutton.png) **Figure 1: Apache Spark home page**[/caption]

Clicking the green button will take you to the download page as shown in Figure 2 below.

[caption id="attachment_53" align="aligncenter" width="660"][![Figure 2: The download page](https://emaasit.files.wordpress.com/2015/07/2-downloadpage.png)](https://emaasit.files.wordpress.com/2015/07/2-downloadpage.png) **Figure 2: The download page**[/caption]

You should follow the steps 1 to 3 to create a download link for a Spark Package of your choice. On the _"2. Choose a package type"_ option, select any pre-built package type from the drop-down list (Figure 3). Since we want to experiment locally on windows, a pre-built package for Hadoop 2.6  and later will suffice.

[caption id="attachment_55" align="aligncenter" width="660"][![Figure 3: Choose a package type](https://emaasit.files.wordpress.com/2015/07/3-prebuilt.png)](https://emaasit.files.wordpress.com/2015/07/3-prebuilt.png) **Figure 3: Choose a package type**[/caption]

On the _"3. Choose a download type" _option, select "Direct Download" from the drop-down list (Figure 4).

[caption id="attachment_56" align="aligncenter" width="660"][![Figure 3: Choose a download type](https://emaasit.files.wordpress.com/2015/07/4-downloadtype.png)](https://emaasit.files.wordpress.com/2015/07/4-downloadtype.png) **Figure 4: Choose a download type**[/caption]

After selecting the download type, a link is created next to the option _"4. Download Spark"_ (Figure 5). Click this link to download Spark.

[caption id="attachment_54" align="aligncenter" width="660"][![Figure 5: Click the download link](https://emaasit.files.wordpress.com/2015/07/5-download.png)](https://emaasit.files.wordpress.com/2015/07/5-download.png) **Figure 5: Click the download link**[/caption]

Save the zipped file to your computer (Figure 6).

[caption id="attachment_57" align="aligncenter" width="660"][![Figure 6: Save to your computer](https://emaasit.files.wordpress.com/2015/07/6-save.png)](https://emaasit.files.wordpress.com/2015/07/6-save.png) **Figure 6: Save to your computer**[/caption]

**Step 2: Unzip Built Package**

Unzip and save the files to a directory folder of your choice. In Figure 7 below, I chose to save to _"C:/Apache/Spark-1.4.1"_.

[caption id="attachment_67" align="aligncenter" width="720"][![Figure 7: List of Files in unzipped folder](https://emaasit.files.wordpress.com/2015/07/7-unzippedfiles.png)](https://emaasit.files.wordpress.com/2015/07/7-unzippedfiles.png) **Figure 7: List of Files in unzipped folder**[/caption]

**Step 3: Run in Command Prompt**

Now start your favorite command shell and change directory to your Spark folder as shown in Figure 8.

[caption id="attachment_68" align="aligncenter" width="720"][![Figure 8: Start command prompt and change directory](https://emaasit.files.wordpress.com/2015/07/8-startcmd.png)](https://emaasit.files.wordpress.com/2015/07/8-startcmd.png) **Figure 8: Start command prompt and change directory**[/caption]

To start SparkR, simply run the command `".\bin\sparkR"` on the top-level Spark directory as shown in Figure 9 below.

[caption id="attachment_69" align="aligncenter" width="406"][![Figure 9: Start SparkR](https://emaasit.files.wordpress.com/2015/07/9-startsparkr.png)](https://emaasit.files.wordpress.com/2015/07/9-startsparkr.png) **Figure 9: Start SparkR**[/caption]

You will see logs on your screen that should take at most 15 seconds to launch SparkR. If everything ran smoothly you should see a welcome message that reads "Welcome to SparkR!" as shown in Figure 10.

[caption id="attachment_70" align="aligncenter" width="720"][![Figure 10: Welcome to SparkR!](https://emaasit.files.wordpress.com/2015/07/10-ready.png)](https://emaasit.files.wordpress.com/2015/07/10-ready.png) **Figure 10: Welcome to SparkR!**[/caption]

At this point you are ready to start prototyping with SparkR on the command shell. Note that a Spark context and a SQL Context have been initialized for you as "_sc_" and "_sqlContext_" respectively. You can now start experimenting using the example shown in **Step 4.5**.

**Running in RStudio**

While using SparkR in the command shell is good for quickly getting started, most R users typically use an Integrated Development Environment (IDE) like RStudio for development and running production ready code. Step 4 below will guide you to get started using SparkR in RStudio.

**Step 4: Run in RStudio**



	
  * **Step 4.1: Set System E****nvironment**


Once you have opened RStudio, you need to set the system environment first. You have to point your R session to the installed version of SparkR. Use the code shown in Figure 11 below but replace the _**SPARK_HOME**_ variable using the path to your Spark folder. Mine is "C:/Apache/Spark-1.4.1".

[caption id="attachment_73" align="aligncenter" width="720"][![Figure 11: Set System Environment Variable](https://emaasit.files.wordpress.com/2015/07/11-setenv.png)](https://emaasit.files.wordpress.com/2015/07/11-setenv.png) **Figure 11: Set System Environment Variable**[/caption]



	
  * **Step 4.2: Set the Library Paths**


Second, you have to set the library path for Spark a shown in Figure 12 below.

[caption id="attachment_74" align="aligncenter" width="720"][![Figure 12: Set the Library Path](https://emaasit.files.wordpress.com/2015/07/12-libpaths.png)](https://emaasit.files.wordpress.com/2015/07/12-libpaths.png) **Figure 12: Set the Library Path**[/caption]



	
  * **Step 4.3: Load SparkR Library**


Next, you can now load SparkR just as you would any other R library using the `library()` command as shown in Figure 13.

[caption id="attachment_75" align="aligncenter" width="720"][![Figure 13:  Load the SparkR library](https://emaasit.files.wordpress.com/2015/07/13-loadsparkr.png)](https://emaasit.files.wordpress.com/2015/07/13-loadsparkr.png) **Figure 13: Load the SparkR library**[/caption]



	
  * **Step 4.4: Initialize Spark Context and SQL Context**


Initialize SparkR by creating a Spark context using the command `sparkR.init()`. The argument in this command is _master = "local[N]"_, where _N_ stands for the number of threads that you want to use.

Also, you need to create a SQL context to be able to work with DataFrames (the main abstraction in SparkR). Use the command `sparkRSQL.init()` to create a SQL context from your Spark context as shown in Figure 14.

[caption id="attachment_76" align="aligncenter" width="720"][![Figure 14: Initialize Spark Context and SQL Context](https://emaasit.files.wordpress.com/2015/07/14-sc.png)](https://emaasit.files.wordpress.com/2015/07/14-sc.png) **Figure 14: Initialize Spark Context and SQL Context**[/caption]

When you run the above commands (From step 4.1 to 4.4), this invokes the "spark-submit" script that launches java, as shown in Figure 15. If this runs successfully, your Spark context and SQL context should be created and at this stage you should be able to start experimenting with SparkR.

[caption id="attachment_77" align="aligncenter" width="720"][![Figure 15: All set](https://emaasit.files.wordpress.com/2015/07/15-ready.png)](https://emaasit.files.wordpress.com/2015/07/15-ready.png) **Figure 15: All set**[/caption]



	
  * **Step 4.5: A Quick Example**


You can start experimenting with SparkR on the command shell and in RStudio using the example provided below. You can monitor your Spark jobs using the Spark UI at [localhost:4040](http://localhost:4040/)

https://gist.github.com/a25c41abe15a75c76e42

**Final Remarks**

The purpose of this blog post was to get you up and running quickly with SparkR locally on a personal computer. In the next blog post, I will show you how to use SparkR on a cloud computing framework like [Amazon Elastic Compute Cloud](http://aws.amazon.com/ec2/) (EC2) to manipulate large datasets with millions of records.

---
title: 'Using Apache SparkR to Power Shiny Applications: Part I'
author: emaasit
date: 2015-12-08 17:24:26+00:00
categories:
  - Apache Spark
  - Big Data
  - Data Science
  - Machine Learning
  - R
  - RStudio
  - Shiny
  - SparkR
slug: using-apache-sparkr-to-power-shiny-applications-part-i
---

_This post was first published on [SparkIQ Labs' blog](http://blog.sparkiq-labs.com) and re-posted on my personal blog._



### [![shiny-sparkr](https://sparkiqlabs.files.wordpress.com/2015/11/shiny-sparkr.jpg?w=300)](https://sparkiqlabs.files.wordpress.com/2015/11/shiny-sparkr.jpg)




### **Introduction**


The objective of this blog post is demonstrate how to use [Apache SparkR](http://spark.apache.org) to power [Shiny applications](http://shiny.rstudio.com). I have been curious about what the use cases for a "Shiny-SparkR" application would be and how to develop and deploy such an app.

**SparkR** is an R package that provides a light-weight frontend to use Apache Spark from R. SparkR provides a distributed data frame implementation that supports operations like selection, filtering, aggregation etc. (similar to R data frames, dplyr) but on large datasets. SparkR also supports distributed machine learning using MLlib.

**Shiny** is an open source R package that provides an elegant and powerful web framework for building web applications using R. Shiny helps you turn your analyses into interactive web applications without requiring HTML, CSS, or JavaScript knowledge.

<!-- more -->


### **Use Cases**


So you're probably asking yourself, "Why would I need to use SparkR to run my Shiny applications?". That is a legitimate question and to answer it, we need to understand the different classes of big data problems.

**Classes of Big Data Problems**
In a recent [AMA on Reddit](http://bit.ly/1LbWPhl), [Hadley Wickham](http://had.co.nz/) (Chief Scientist at [RStudio](https://www.rstudio.com/)) painted a clearer picture of how "Big Data" should be defined. His insights will help us to define uses cases for SparkR and Shiny.

I believe big data problems should be categorized in 3 main classes:



	
  1. **Big Data-Small Analytics:** This is where a data scientist begins with a raw big dataset and then slices and dices that data to obtain the right sample required to answer a specific business/research problem. In most cases the resulting sample is a small dataset, which **doesnot** require the use of SparkR to run a shiny application.

	
  2. **Partition Aggregrate Analytics:** This is where a data scientist needs to distribute and parallelize computation over multiple machines. Wickham defines this problem as a **trivially parallelisable problem**. An example is when you need to fit one model per individual for thousands of individuals. In this case SparkR is a good fit but there are also packages in R that solve this problem such as the [foreach package](https://cran.r-project.org/web/packages/foreach/index.html).

	
  3. **Big Data-Large Scale Analytics**. This is where a data scientist needs all the big data, perhaps because they are fitting a complex model. An example of this type of problem is recommender systems which really do benefit from lots of data because they need to recognize interactions that occur only rarely. SparkR is a perfect fit for this problem when developing Shiny applications.


**Memory Considerations**

Also, it's important to take into consideration memory availability and size when looking into such an application. This can be viewed in two different ways:



	
  * If you are running your shiny applications on servers that have more than enough memory to fit your big data, then you probrably do not need SparkR. Nowadays there is accessibility to machines with terabytes on RAM from cloud providers like [Amazon AWS](http://aws.amazon.com).

	
  * If your big data cannot fit on one machine, you may need to distribute it on several machines. SparkR is a perfect fit for this problem because it provides distributed algorithms that can crunch your data on different worker nodes and return the result to the master node.




### **A Simple Illustrative Example**


Before we start understanding how each piece of such an application would operate, let's download and run this simple Shiny-SparkR application. Go to this github repository [https://github.com/SparkIQ-Labs/Demos](https://github.com/SparkIQ-Labs/Demos) and access the **"shiny-sparkr-demo-1"** example.

[![Repository](https://github.com/SparkIQ-Labs/Demos/raw/master/shiny-sparkr-demo-1/img/repo.png)](https://github.com/SparkIQ-Labs/Demos/blob/master/shiny-sparkr-demo-1/img/repo.png)

**Prerequisites**



	
  1. Make sure you already have Apache Spark 1.5 or later downloaded onto your computer. Instructions for downloading and starting SparkR can be found in this [blog post](http://bit.ly/1kP5Fbm).

	
  2. Make sure you have Java 1.7.x installed and the environment variables are set.




### **Launch the App**


Once you have downloaded the app-folder, open the project in RStudio and open the **"server.R"** file.




	
    1. **Change Spark Home**. Change the path of the **SPARK_HOME** environment variable to point to the destination of your Spark installation.



[![Change Spark home](https://github.com/SparkIQ-Labs/Demos/raw/master/shiny-sparkr-demo-1/img/spark-home.png)](https://github.com/SparkIQ-Labs/Demos/blob/master/shiny-sparkr-demo-1/img/spark-home.png)



	
  1. **Run the App**. Run the shiny app by using this command `shiny::runApp()`. It will take some time for SparkR to be initialized before you can see the results of the underlying analysis are displayed.


[![The App](https://github.com/SparkIQ-Labs/Demos/raw/master/shiny-sparkr-demo-1/img/app.png)](https://github.com/SparkIQ-Labs/Demos/blob/master/shiny-sparkr-demo-1/img/app.png)

Here is the the code for the "server.R" file.

[gist]7cf8aa8efc535db160df[/gist]


### ** What happens Underneath.**






	
    1. **Stage 1:** When you run the app, the user interface is displayed but without the rendered text output or model summary.



[![App without the results](https://github.com/SparkIQ-Labs/Demos/raw/master/shiny-sparkr-demo-1/img/no-results.png)](https://github.com/SparkIQ-Labs/Demos/blob/master/shiny-sparkr-demo-1/img/no-results.png)




	
    1. **Stage 2:** Meanwhile, in the background on your computer node(s), java is launched using the Spark-submit file, then the SparkR library is loaded and then SparkR is initialized.



[![SparkR is initialized](https://github.com/SparkIQ-Labs/Demos/raw/master/shiny-sparkr-demo-1/img/java-launch.png)](https://github.com/SparkIQ-Labs/Demos/blob/master/shiny-sparkr-demo-1/img/java-launch.png)




	
    1. **Stage 3:** SparkR commands in the Server.R file are then executed, which finally shows the output within the shiny app.



[![Results in the App](https://github.com/SparkIQ-Labs/Demos/raw/master/shiny-sparkr-demo-1/img/app.png)](https://github.com/SparkIQ-Labs/Demos/blob/master/shiny-sparkr-demo-1/img/app.png)

You can use the Spark UI to check the jobs that were completed, in the event timeline, to produce the final results in the shiny app. Go to localhost and listen on port 4040.

[![Results in the App](https://github.com/SparkIQ-Labs/Demos/raw/master/shiny-sparkr-demo-1/img/event-timeline.png)](https://github.com/SparkIQ-Labs/Demos/blob/master/shiny-sparkr-demo-1/img/event-timeline.png)



	
  1. **Stage 4:** When you change the input values in the app and click the "Predict Sepal Length" button, the application uses the already exciting Spark Context to run the predict function and displays the predicted value. This operations takes a shorter time than the initial launch of the shiny app.


[![Change values](https://github.com/SparkIQ-Labs/Demos/raw/master/shiny-sparkr-demo-1/img/new-result.png)](https://github.com/SparkIQ-Labs/Demos/blob/master/shiny-sparkr-demo-1/img/new-result.png)


### **Moving Forward**


The objective of this first demo was to learn the use cases for SparkR and Shiny; and to see what happens underneath when you eventually deploy and run such an application on a PC.

In **Part II** of this tutorial series, we shall see how to develop and deploy such an application for a "Big Data-Large Scale Analytics" problem on big data stored on a cluster on AWS EC2. As we have already established this is one of the perfect use cases for SparkR and Shiny.

Please share your thoughts and experiences in the comments' section below if you have built such applications.



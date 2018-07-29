# Big Data Platforms Spark V Hadoop
Big Data is everywhere and it comes with a lot of jargon.  The term is being used to refer to everything from ‘lots of data’ to so much data it can’t be processed on a single server.


## What Is Big Data

-**Volume:** More data is generated every second than ever before.  Big Data technology can be used to store and compute data across distributed systems with software that brings it all together.

-**Velocity:** Data is being generated faster than ever before.  Big Data Technology allows data to be generated, stored and analysed in one step.

-**Variety:** Traditionally we think of data as structured and store it in relational databases.  Unstructured data refers to photos, videos, emails and powerpoint presentations. Big Data technology allows us to harness both types.


## Frameworks
You can’t talk about Big Data without hearing about Hadoop and Spark.  They are both Big Data frameworks but do different things.  Hadoop is a distributed data infrastructure that allows data to be processed and analysed more effectively.  Spark operates on that data and doesn’t do any of the storage.  You can use one without the other as Hadoop has an equivalent called MapReduce, but Spark is quicker.  Here are the main differences between the two.


| 	| Spark |	Hadoop |
|---|-------|--------|
|Data Processing	| Performs batch and stream processing in memory.	| MapReduce performs batch processing stored on disk.
| Graph Processing | Great at iterative workloads (Machine learning).	| Not ideal for iterative work.
| Ease of use	| Java, Python, Scala supported with user friendly APIs.	| No interactive mode but tools like Pig and Hive make it easier.
| Costs	| Open source but uses large amounts of RAM. | Open source but requires more systems to distribute the disk.



## Ecosystem
The processing engine is only part of what frameworks like Hadoop and Spark do.  Their suite of tools that can be used to do everything from allowing users to query data to implementing machine learning.  Read more about each of them, what they do and which framework is right for your project.


| 	| Spark |	Hadoop |
|---|-------|--------|
| Data Analysis Tool	| Spark Native API | Pig
| SQL Engine | Spark SQL | Hive
| Machine Learning Library | MLLib |	Mahout
| Data Streaming | Spark Streaming | Storm
| Graph Processing | Spark GraphX |	Giraph
| Workbench | Spark Notebook | Hue

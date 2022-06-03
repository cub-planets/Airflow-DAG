# Airflow-DAG
## Downloading and monitoring images by Airflow/DAG
Apache Airflow is an open-source platform to author, schedule, and monitor workflows.
When workflows are defined as code, they become more maintainable, versionable, testable, and collaborative.
Use Airflow to author workflows as directed acyclic graphs (DAGs) of tasks. The Airflow scheduler executes your tasks on an array of workers while following the specified dependencies. Rich command line utilities make performing complex surgeries on DAGs a snap. The rich user interface makes it easy to visualize pipelines running in production, monitor progress, and troubleshoot issues when needed.
## Table of contents

- Project Focus
- Principles
- Requirements
- Getting started
## Project Focus
Airflow is best thought of as a spider in a web: it sits in the middle of your data processes and coordinates work happening across the different (distributed) systems. As such, Airflow is not a data processing tool in itself, but orchestrates the different components responsible for processing your data in data pipelines.
The Airflow scheduler—Parses DAGs, checks their schedule interval, and (if the DAGs’ schedule has passed) starts scheduling the DAGs’ tasks for execution by passing them to the Airflow workers.  The Airflow workers—Pick up tasks that are scheduled for execution and execute them. As such, the workers are responsible for actually “doing the work.”  The Airflow webserver—Visualizes the DAGs parsed by the scheduler and provides the main interface for users to monitor DAG runs and their results.
In this project, we run airflow for monitoring and downloading images and updating our data from API or text files (that have many URL addresses) every 2min automatically or manually whenever we need to update our data. Airflow enables us to manage our data pipeline and organize the whole process by defining the rule that can be our tasks and dependencies between them. So, everything goes according to our plan.

## Principles
- Dynamic: Airflow pipelines are configuration as code (Python), allowing for dynamic pipeline generation. This allows for writing code that instantiates pipelines dynamically.
- Extensible: Easily define your own operators, executors and extend the library so that it fits the level of abstraction that suits your environment.
- Elegant: Airflow pipelines are lean and explicit. Parameterizing your scripts is built into the core of Airflow using the powerful Jinja templating engine.
- Scalable: Airflow has a modular architecture and uses a message queue to orchestrate an arbitrary number of workers.
## Requirements
Apache Airflow is tested with:
- Python		
- PostgreSQL
- MySQL	
- SQLite	
- MSSQL	
* Experimental
- Note: running Airflow on Windows 10 can be challenging even I tried it by WSL but it was not successful and I did it by Docker.



## Running Airflow in Docker containers:
Docker containers are also popular to create isolated environments to run a reproducible set of Python packages and avoid dependency clashes. However, Docker containers create an isolated environment on the operating system level. For running Docker containers, we require a Docker Engine to be installed on your machine. Below link help you to run Airflow in docker.
 
https://airflow.apache.org/docs/apache-airflow/stable/start/docker.html

## Getting started
Below link is the the official Airflow website that is very useful for installing Airflow, getting started, or walking through a more complete tutorial.
"https://airflow.apache.org/Visit" 
Also there is a documentation in the below address:
s.apache.org/airflow-docs
 
 ## User Interface
DAGs: Overview of all DAGs in your environment

![image](https://user-images.githubusercontent.com/93762108/171958386-5b731384-ef32-4539-8e58-9e9b1e8de865.png)


## Data pipelines
Data pipelines generally consist of several tasks or actions that need to be executed to achieve the desired result. In this project, we need to download images from URL/API or text file whenever it is updated. To implement this dashboard, we need to perform something like the following steps: 
1- Fetch images from API or a text file that has URL addresses for downloading images. (Task A)
2-Start downloading (Task B)
3- Notify that images are downloaded (tasks C)
By just quickly glancing at the graph, we can see that our pipeline consists of three different tasks, each corresponding to one of the tasks outlined. Other than this, the direction of the edges indicates the order in which the tasks need to be executed: we can simply follow the arrows to trace the execution.

![image](https://user-images.githubusercontent.com/93762108/171960113-d6f4da11-6c3d-47fd-bfcd-3ad027b2deba.png)


## Defining pipelines flexibly in (Python) cod:
Airflow allows you to define pipelines or workflows as DAGs of tasks. With tasks being defined as nodes in the graph and dependencies as directed edges between the tasks. In Airflow, you define your DAGs using Python code in DAG files, which are essentially Python scripts that describe the structure of the corresponding DAG. As such, each DAG file typically describes the set of tasks for a given DAG and the dependencies between the tasks, which are then parsed by Airflow to identify 
the DAG structure. Besides this, the DAG also defines a schedule interval that determines when Airflow executes the DAG.

![image](https://user-images.githubusercontent.com/93762108/171960286-a3f7ef92-bdae-49ff-934d-3fb275a6f85c.png)
## Writing Airflow DAG
The DAG is the starting point of any workflow. All tasks within the workflow reference this DAG object so that Airflow knows which tasks belong to which DAG.
Note the (lowercase) dag is the name assigned to the instance of the (uppercase) DAG class. The instance name could have any name; you can name it “download images” or whatever_name_you_like. We will reference the variable (lowercase dag) in all operators, which tells Airflow which DAG the 
operator belongs to.
## Defining scheduling intervals
In Airflow, we can schedule a DAG to run at certain intervals by defining a schedule interval for it using the schedule interval argument when initializing the DAG. By default, the value of this argument is None, which means the DAG will not be scheduled and will be run only when triggered manually. Airflow provides the convenient macro @daily for defining a daily scheduled interval, which runs our DAG once every day at midnight. But in this project, we set it “2 min” which means that every 2 min the DAG will run.
An overview of the other macros supported by Airflow is shown in the table
![image](https://user-images.githubusercontent.com/93762108/171960657-a6f37c09-06f8-4eb0-b06b-3c5f29ad49a4.png)

## Defining the start and end date for the DAG
Airflow also needs to know when we want to start executing the DAG, specified by its start date. Based on this start date, Airflow will schedule the first execution of our DAG to run at the first scheduled interval after the start date (start + interval). Subsequent runs will continue executing at scheduled intervals following this first interval.
Without an end date, Airflow will (in principle) keep executing our DAG on this daily schedule until the end of time. However, if we already know that our project has a fixed duration, we can tell Airflow to stop running our DAG after a certain date using the end_date parameter.
start_date=dt. datetime (year=2022, month=1, day=1), end_date=dt. datetime (year=2023, month=1, day=5),
Operators are the main building blocks of Airflow DAGs. They are classes that encapsulate logic to do a unit of work. When you create an instance of an operator in a DAG and provide it with its required parameters, it becomes a task. 

## Running a Python function using the Python Operator
The program has the ability to check if the file had been downloaded before and existed in the folder or not. if the file is not found to be duplicate it starts the downloading process and logs the result in the log.txt file, otherwise, it scapes that file and searches for other new files for downloading. The log management designed in the program records every transaction in a separate row including the date, time, and several files downloaded. The program has been tested for both input file and API mode and resulted in successful downloading operations. The Airflow provides the capability to schedule the python program in predefined intervals. Currently, the schedule intervals are set at 2 minutes meaning that every 2 minutes the Airflow run the python to download the files. The files are commanded to save in a predefined target folder (path). The program is completely flexible to set to download and types of files e.g. images, music, text, and so on.
![image](https://user-images.githubusercontent.com/93762108/171961058-4b3825ed-3f58-4af2-8168-691c15a840d8.png)


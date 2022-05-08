# Data Lakes
## Project introduction

A music streaming startup, Sparkify, has grown their user base and song database even more and want to move their data warehouse to a data lake. Their data resides in S3, in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

## Table of contents:

- [Objective](#objective)
- [Dimension and fact Table](#starschema)
- [steps needed to run project](#runproject)
- [Datasets](#datasetsource)
- [Additional Steps that can be taken](#additionalsteps)


## Objective
build an ETL pipeline that extracts their data from S3, processes them using Spark (AWS Elastic Map Reduce(EMR)), and loads the data back into S3 as a set of dimensional tables

## StarSchema
- songplays: fact table - (songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent)
- songs: dimensions table - (song_id, title, artist_id, year, duration)
- artists: dimensions table - (artist_id, name, location, lattitude, longitude)
- users: dimensions table - (user_id, first_name, last_name, gender, level)
- time : dimension table - (start_time, hour, day, week, month, year, weekday)

### RunProject
run the etl.py file in the project
```bash
python etl.py
```
## DatasetSource
### Song dataset
The first dataset is a subset of real data from the [Million Song Dataset](http://millionsongdataset.com/). Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are filepaths to two files in this dataset.
###Log dataset
The second dataset consists of log files in JSON format generated by this [event simulator](https://github.com/Interana/eventsim) based on the songs in the dataset above. These simulate app activity logs from an imaginary music streaming app based on configuration settings.

The data is  sourced from S3 buckets on aws
- Song data: s3://udacity-dend/song_data
- Log data: s3://udacity-dend/log_data

## AdditionalSteps
- one run unit tests via a spark notebook to check for any corrupt_records in the json file
- partition the data into parts to spot any form for data skewness. It could help spot trends or shifts data due to events such as seasonality e.g a rise in user interaction with christmas songs in december

This could help in the long term as the log data is only is only for one month(November 2018) and its distribution may change if one is building an etl pipeline to process months or years of data.

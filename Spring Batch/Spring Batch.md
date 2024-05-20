# Tutorial

> The following is based on Spring Batch Tutorial: https://spring.academy/courses/building-a-batch-application-with-spring-batch


## Features

Transaction Management
Chunk Based Processing
Declarative I/O
Start/Stop/Restart
Retry/Skip
Web based administration interface (Spring Cloud Data)

## Introduction

Batch processing is a method of processing large volumes of data simultaneously (as opposed to real-time stream processing).

### Domain model

![[domain-model.png]]

- `Job` :  entity that encapsulates an entire batch process, that runs from start to finish without interruption.
- `Step` : a unit of work that can be a simple task (such as copying a file). A `Job` has one or more `Step`s.
- `JobLauncher` :  launches a `Job` with a set of `JobParameter`s.
- `JobRepository` :  holds metadata about the currently running job.

Spring Batch provides a relational model of the batch domain concepts with metadata tables that closely match the classes and interfaces in the Java API.

![[relational-model.png]]
Details: [Spring Batch Overview - Batch Domain Model](https://spring.academy/courses/building-a-batch-application-with-spring-batch/lessons/overview#batch-domain-model)

### Architecture

The following diagram shows the layered architecture:

![[architecture.png]]

- `Application`: contains the batch job and custom code written by the developers of the batch application.
- `Batch Core` : core runtime classes provided by Spring Batch that are necessary to create and control batch jobs.
- `Batch Infrastructure` : common item readers and writers provided by Spring Batch, plus base services such as the repeat and retry mechanisms.

## Launching Jobs


The following diagram shows how the `JobLauncher`, the `JobRepository` and the `Job` interact with each other.

![[launching-jobs.png]]


## Job Instances

A `Job` might be defined once, but it'll likely run many times, commonly on a set schedule.

A `JobInstance` is a unique parametrisation of a `Job` definition. 

In the once-per-day scenario, we can use Spring Batch to create an `EndOfDay` `Job`.  There would be a single `EndOfDay` `Job` definition, but multiple instances of that same `Job`, one per day.

A `JobInstance` is distinct from other `JobInstance`s by a specific parameter, or a set of parameters. `JobParameter`s are what distinguish one `JobInstance` from another.

![[job-parameters.png]]

Designing `JobInstance`s to represent the data to be processed is easier to configure, to test, and to think about, in case of failure.

Here are a few examples of `JobParameter`s, and how they represent the data to be processed by the corresponding `JobInstance`:

- A specific date: In this case, we would have a `JobInstance` per date.
- A specific file: In this case, we would have a `JobInstance` per file.
- A specific range of records in a relational database table: In this case, we would have a `JobInstance` per range.

## Job Executions

A `JobExecution` refers to a single _attempt_ to run a `JobInstance`. A `JobExecution` may end in a success or failure. In the case of the `EndOfDay` `Job`, if the January 1st run fails the first time, it can be run again. Therefore, each `JobInstance` can have multiple `JobExecution`s.

![[job-execution.png]]

Lifecycle of a `JobInstance`:

![[job-instance-lifecycle.png]]



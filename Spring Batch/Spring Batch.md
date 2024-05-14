# Tutorial

> The following is based on Spring Batch Tutorial: https://spring.academy/courses/building-a-batch-application-with-spring-batch


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

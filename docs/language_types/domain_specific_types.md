---
layout: default
title: Domain Specific Types
nav_order: 2
parent: Language Types
---


# Domain Specific Types
{:.no_toc}

## Table of Contents 
{: .no_toc .text-delta }
1. TOC
{:toc}

---

## Introduction to Fly Objects
The main domain type is the __object__ type.
A FLY object is a heterogeneous collection of basic and/or domain types elements. 

Essentially a FLY object is a mixture between an array and map data structure, which stores data in key/value
pair. 

The value of an element can be accessed in two different ways: by position (like arrays) or by key (like maps). When a new value is assigned to a given key/position a new element is created, otherwise the new value replaces the previous one. 

Moreover, all FLY domain specific type are an instance of the object type, which means are build in similar fashion, specifying the object type using the parameter keyword `type = “object_type”`.

---

## Object Domain Types

Let's see which are all the domain specific types provided by FLY

### Environments

The **Environment** type represents an abstraction of a execution environment. It provides the ability to interact with a cloud provider or a SMP system.  Different environments are treated in the same way by FLY, leaving the details relating to the specific use of each execution environment to the FLY compiler.

Environments are declared as an object using several parameters that characterize a back-end.

#### SMP

The SMP backend is the local machine execution environment, and can be used to execute functions on the local machine.

```js
var Smp = [type="smp", nthread=4]
```

- *nthread* parameter is the number of threads used by the local stack to execute the FLY program, it must be an integer greater then **2**.

#### Azure

The Azure backend offer the transparent communication with the Microsoft Azure Cloud, specifing the following parameters.

```js
var Azure = [type="azure", client_id="<client>", tenant_id="<tenant>", secret_key="<secret>", subscription_id="<subscription>", region="<region>", language="<language>", nthread=3, seconds=1]

```

- _client_id_: the Azure Client ID
- _tenant_id_: the Azure Tenant ID
- _secret_key_: the secret key of Azure services
- _subscription_id_: the subscription ID of Azure services
- _region_: the Azure region you want to use
- _language_: the programming language to use (see the introduction chapter)
- _nthread_: the number of threads you want to use on AWS backend
- _seconds_: the time for each execution limit of the backend

#### AWS

The AWS backend offer the transparent communication with the AWS Cloud, specifing the following parameters.

```js
var Aws = [type="aws", profile="<profile>", access_id_key="<id>", secret_access_key="<secret>", region="<region>", language="<language>", nthread=4, memory=256, seconds=1]
```

- _profile_: the AWS profile name
- _access_id_key_: the secret ID key of AWS services
- _secret_access_key_: the secret key of AWS services
- _region_: the region you want to use
- _language_: the programming language to use (see the introduction chapter)
- _nthread_: the number of threads you want to use on AWS backend
- _memory_: the memory limit of the backend
- _seconds_: the time for each execution limit of the backend

Also, FLY provides a testing beckend with `type = "aws-debug"` which simulates AWS Cloud on the local machine. Obiously, the parameter declaration doesn't change.

```js
var Test = [type="aws-debug", profile="<profile>", ...]
```


#### Good Programming Note
{:.no_toc}

As a note for developers, each envirnoment variable should be delcared with an uppercase identificator.

### Channels

**Channel** type is a domain type that enables the synchronization and communication between FLY functions and/or the main program, defined
by the `type = “channel”`. 

A new channel is defined on an environment, and can be used for the communication between functions executing on the same back-end or from the main program to a back-end and viceversa. 

Channels are blocking message queues, that is, when the main program or a function tries to receive a message from a channel, the execution is blocked until a new message arrives on the channel.

Each channel must be defined on a specific back-end, using the keyword `on` after the variable declaration.

```js
var ch = [type="channel"] on <Backend> 
```

where Backend is an environment variable previously declared.

#### Communication Statements
{:.no_toc}

Messages are sent on a channel using the character `!` (e.g., the instruction ch!VAL sends a message VAL on the channel ch), while the character `?` is used to receive messages, (e.g., the instruction x=ch? reads a message from the channel ch and assigns the obtained value to the
variable x). 

Channels use network infrastructures to communicate with the cloud environment and for this reason a serialization mechanism is required for sending/receiving messages. FLY defines the serialization for objects, files, images and basic types. It is not allowed to send messages containing environments, channels, and random objects.

### File

__File__ object is the abstraction of file in FLY.
The language supports four file formats: csv, json, img, and txt.

A new file object is defined using also additional parameters: path (the file system path) or a reference to the file, and by the separator sep, that is an optional parameter defined for CSV files.

The language provides two methods to access files, which depend on where the file is stored: local or remote.

```js
var name = [type=”file” , path="path/to/the/file.(txt, json, csv, img)" , sep="separator"] on Env ( optional )
```

If the environment will not be specified, FLY'll assume the file locally. 

### Dataframe

FLY has a specific focus on csv files managing them as a __Dataframe__ (similar to R language dataframes). The memory is seen as a matrix structure, allowing the user to access to rows and columns, while it provides dedicated operations for querying, filtering, random access, etc.

TODO scrivere la documentazione dei dataframe

### Database Connection
TODO

#### SQL

#### NoSQL

#### Query

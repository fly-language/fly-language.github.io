---
layout: default
title: Introduction
nav_order: 1
description: "What is fly?"

---

# FLY a Domain Specific Language for scientific computing on the Multi Cloud
{:.no_toc}

Exploit the multi-cloud and HPC to achive better performance.
{: .fs-6 .fw-300 }

---

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

---

## What is FLY?

FLY is a parallel work-flow scripting imperative language inspired by functional languages peculiarities.
FLY uses two type of run-time environment: the local machine and/or cloud infrastructure. FLY perceives a cloud computing infrastructure as a parallel computing architecture on which it is possible to execute some parts of its execution flow in parallel.

FLY main goals are:
* ___expressiveness___, in deploying scientific large-scale computing work-flows;
* ___programming usability___, writing .fly program should be straightforward for domain experts, while the interaction with the cloud environment should be completely transparent; the users do not need to know the cloud providers APIs;
* ___scalability___ either on symmetric multiprocessing (SMP) architectures or cloud computing infrastructures supporting FaaS. 

FLY is compiled in native code (Java code) and it is able to automatically exploits the computing resources available that better fit its computation requirements. The innovative aspect of FLY is constituted by the concept of ___FLY function___. A FLY function can be seen as an independent block of code, that can be executed concurrently.

| Faas Cloud Computing Infrastructure | Supported          | Under development  | Future development |
|:-------------------------------------:|:--------------------:|:--------------------:|:--------------------:|
| Amazon AWS                          | ✔️ |                    |                    |
| Microsoft Azure                     | ✔️ |                    |                    |
| [LocalStack](https://localstack.cloud/)| ✔️ |                 |                    |
| Google Function                     |                    | ✔️ |  |
| IBM Bluemix/Apache OpenWhisk        |                    |                    | ✔️ |

### Supported Languages

|Faas Cloud Computing Infrastructure |Python | Javascript|
|:-------------------------------------:|:--------------------:|:--------------------:|
| Amazon AWS                               | ✔️ |✔️   |
| Microsoft Azure                          | ✔️ |✔️   |
| [LocalStack](https://localstack.cloud/)  | ✔️ |✔️   |

---

## Installation

Follow all these step to correct create a FLY Project.

### Requirements

- Eclipse with Xtext/Xtend support
- Ubuntu or OSX OS
- Java 8 (or greater)
- Apache Maven 3 (or greater)
- Amazon AWS CLI and SDK
- Python 3
- Node.js 8.10

### Preliminar Procedure

1. Download FLY from GitHub repository;
2. Import as Maven project the folder _FLY.compiler_
3. Right click on folder _fly.parent_ -> Run as -> maven build... -> Goal: "_clean verify_"
4. Right click on folder _fly.parent_ -> Maven -> Update Project
5. Right click on folder _org.xtext.FLY_ -> Run as -> Eclipse Application

### Install the Archetype

1. Extract file _fly-project-quickstart.zip_
2. From the terminal, navigate to the unzipped folder (in which should be contained a _pom.xml_ file)
3. Run `mvn install` and wait its termination
4. Run `mvn archetype:crawl`
5. In the new eclipse runtime, go in Preference -> Maven -> Archetypes -> Add Local Catalog... in the folder /home/user/.m2/repository select the file _archetype-catalog.xml_

### New FLY Project

1. In the new eclipse runtime select: New Project -> Maven Project -> select the archetype it.isislab
2. Right click on the package _src/main/fly_ -> New File -> "foo".fly (can be any name) -> Click on Yes

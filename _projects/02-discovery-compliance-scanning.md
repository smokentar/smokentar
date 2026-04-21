---
title: "Discovery and Compliance Scanning"
excerpt: "is a method for discovering resources and identifying security misconfigurations in a cloud infrastructure."
collection: projects
tags:
  - AWS
  - Python
  - Steampipe
  - Cloudquery
  - Neo4j
---

## TL;DR:

Discover resources in a target cloud account and evaluate them against pre-defined rules to generate alerts. Automate process using AWS services and open-source software.

## Overview

Today's enterprise operates across thousands of resources distributed over multiple cloud environments which evolve constantly - provisioned and modified by different teams - making one problem increasingly difficult to solve: context and visibility.

How does one answer in real time:

- What exactly is deployed, and where?
- Does it follow best practices?
- What's the exposure surface of a new CVE?
- Have compliance requirements silently drifted?

Cloud Security Posture Scanning (CSPM) continuously monitors an infrastructure, detects misconfigurations, and provides a real-time, unified view of resources and findings.

## The project

To achieve the above, we need a method to 1. discover resources and 2. evaluate their configuration against a set of rules.

![](/images/dcs.svg)

Staying consistent with how we approached [Agentless Vulnerability Scanning](/projects/01-agentless-vulnerability-scanning), we will use AWS services to automate this process:

- **API Gateway** to connect our frontend with the backend
- **Lambda** to handle orchestration logic and initiate analysis
- **Elastic Container Service (ECS)** to run the analysis containers
- **Simple Queue Service (SQS)** to queue and scale to hundreds of scan events
- **S3** to instantiate scan locks, similar to Terraform locks
- **Database** to store scan results
- **CloudWatch Logs** to retain execution logs

### Workflow

![](/images/dcs-pipeline.png)

#### 1. Initiation

Scans are triggered in two ways:

1. **Ad-hoc request** - user action in the frontend calls API Gateway, which invokes a Lambda function that sends a message to SQS.
2. **Scheduled execution** - EventBridge sends a message directly to SQS on a predefined schedule.

#### 2. Polling & Task dispatch

A Lambda poller continuously consumes messages from SQS and launches the appropriate ECS task based on the payload.

#### 3. Scan execution

The scanning software runs as a Docker container on ECS Fargate. Unlike the Agentless vulnearbility Scanning workflow - which uses ECS on EC2 due to custom volume mount requirements - this process is lightweight enough to run fully on Fargate.

The container assumes a role into the target cloud account, performs the scan and loads the data into a Neo4j database.

#### 4. Data load & Normalisation

Results are loaded into Neo4j to be queried and displayed on the frontend.

- CloudQuery writes directly to Neo4j via its native integration.
- Steampipe outputs results to disk first, after which they are cleaned, transformed and imported into Neo4j using Python.

This extra transformation step aligns Steampipe data to the CloudQuery schema, enabling consistent correlation.

### Result

![](/images/data-schema-is.png)

Due to the vast number of cloud resource types and possible relationships between them, it is incredibly difficult to represent an entire environment in a single diagram. This illustration shows a simplified example of correlations that may exist, in combination with [Agentless Vulnerability Scanning](/projects/01-agentless-vulnerability-scanning).

## The software

### Discovery

[CloudQuery](https://cloudquery.io) is a software built to extract, transform, and load (ETL) configuration from cloud provider APIs into destinations like databases or data lakes. Its [Amazon Web Services](https://www.cloudquery.io/hub/plugins/source/cloudquery/aws/latest/docs) integration was open-source when I developed this project, but later shifted to a paid model, leaving only the SDK as open-source.

### Compliance

[Steampipe](https://steampipe.io) is an open-source software that enables dynamic querying of cloud provider APIs using SQL syntax. It supports many plugins, but it truly shines when using its plugin mods. For example, the [Amazon Web Services](https://hub.steampipe.io/plugins/turbot/aws) plugin includes a [Compliance](https://hub.powerpipe.io/mods/turbot/steampipe-mod-aws-compliance) mod, which provides a collection of pre-defined rules for benchmarks such as GDPR, HIPAA, PCI DSS, Cyber Essentials. The engine can evaluate these rules against discovered cloud resources.

### Database

[Neo4j](https://neo4j.com) is an open-source graph database, heavily focusing on relationships between entity types. It provides a more natural way of querying and visualizing complex data.

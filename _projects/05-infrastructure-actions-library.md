---
title: "AWS Infrastructure Actions Library"
excerpt: "is a collection of Amazon Web Services actions, bringing speed and certainty to repetitive cloud operations."
collection: projects
tags:
  - AWS
  - Python
  - Boto3
  - Terraform
---

_Open source. View code at [avtomat-aws](https://github.com/avtomat-hub/avtomat-aws)._

## Overview

As an engineer in a managed services provider I want to automate manual tasks where possible. I'm confident my colleagues follow a similar methodology.

Unfortunately, engineering individuality leads to a fragmented landscape of custom scripts, many of which perform similar functions but are written, tested and maintained independently.

Just imagine having to run a global operation script against production, and you have to write it from scratch. Say you are a 10x engineer and cook up the code in lightning speed, now time to execute.

> "Fear leads to anger, anger leads to hate, hate leads to suffering." - Master Yoda

My motivation for creating this library is to 1. remove suffering from the equation, 2. ensure effort is not wasted, but built upon, and 3. get some practice on hosting open-source from scratch.

## The project

The library is a collection of reusable Amazon Web Services actions, written in Python, on top of Boto3, that can be used to automate common cloud tasks.

Think of `ec2.discover_unused_security_groups()` instead of 500 lines of boilerplate code.

**Flexible** - Actions can be used individually (CLI) or linked together to form workflows (programmatic).

**Standardised** - Each action received an input, processes it, and returns an output.

**Chainable** - Output from one action can be used as input to another action.

**Pre-configured** - Built in retry and error handling; embedded logging for each action; automatic pagination when processing many resources

**Least privilege** - <a href="https://docs.avtomat.io/aws/permissions" target="_blank">Permissions</a> are defined for each action and can be usd to swiftly create secure IAM policies.

## Examples

I have included a few <a href="https://docs.avtomat.io/aws/examples" target="_blank">examples</a> to demonstrate different use cases.

## More details

### Workflows

Currently, there are no built-in workflows. I have included some in the documentation, however they are currently closed-source, pending a decision about how to move the project forward.

### Work in progress

This project is a work in progress, I will be infrequently adding new actions and improving existing ones. I am also open to contributions from the community.

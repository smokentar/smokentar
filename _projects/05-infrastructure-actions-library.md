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

As an engineer, I naturally lean towards automation when possible. I'm confident my colleagues are the same.

Unfortunately, engineering individuality leads to a fragmented landscape of custom scripts, many of which perform similar functions but are written, tested and maintained independently.

Imagine having to run a global operation script against production, you write it from scratch, and now it's time to execute.

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

I have included a few programmatic <a href="https://docs.avtomat.io/aws/examples" target="_blank">examples</a> to demonstrate different use cases.

Furthermore, I have displayed some <a href="https://docs.avtomat.io/aws/workflows" target="_blank">simple workflows</a> to show what can be achieved through this library. I did not release the code for these, pending a decision about how to move the project forward.

## Work in progress

This library is a work in progress, I will be infrequently adding new actions and improving existing ones. I am also open to contributions from the community.

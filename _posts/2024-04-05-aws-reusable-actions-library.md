---
layout: post
title: Reusable Actions Library for AWS
date: 2024-04-05 08:01:35 +0300
categories: Project
tags: aws python open-source 
excerpt: A collection of reusable Amazon Web Services actions, bringing speed and certainty to repetitive cloud operations. <a href="https://github.com/avtomat-hub/avtomat-aws" target="_blank">GitHub</a>
mathjax: true
---

<script async src="https://www.googletagmanager.com/gtag/js?id=G-RSWENHHV9W"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());

  gtag('config', 'G-RSWENHHV9W');
</script>

* content
{:toc}

![](/images/open-source.svg)

## Overview

As an engineer in a managed services provider, I have observed that a lot of churn is attributed to repetitive and less innovative work. This mostly impacts junior engineers who don't yet have the experience to deliver projects and are mainly assigned to support roles.

Junior engineers are valuable, I see them as the mids and seniors of tomorrow. As a junior, I would have enjoyed having access to some library, allowing me to easily automate a task which I have already done manually a few times, so I could invest my time in learning something new.

That's why I created and open-sourced this project.

## The project

The library is a collection of reusable Amazon Web Services actions, written in Python, on top of Boto3, that can be used to automate common cloud tasks. It is designed to be easy to use and extend, allowing engineers to quickly automate repetitive tasks, even with limited coding experience.

#### Flexible
Actions can be used individually (CLI) or linked together to form workflows (programmatic).

#### Standardised
Each action received an input, processes it, and returns an output.

#### Chainable
Output from one action can be used as input to another action.

#### Pre-configured
- Built in retry and error handling
- Embedded logging for each action
- Automatic pagination when dealing with many resources

#### Least privilege
<a href="https://docs.avtomat.io/aws/permissions" target="_blank">Permissions</a> are defined for each action and can be usd to swiftly create secure IAM policies.

#### Examples
I have included a few <a href="https://docs.avtomat.io/aws/examples" target="_blank">examples</a> to demonstrate different use cases.

#### Work in progress
This project is a work in progress, I am (frequently or infrequently) adding new actions and improving existing ones. I am also open to contributions from the community.

## More details

#### Workflows
Currently, there are no built-in workflows. I have included some in the documentation, however they are currently closed-source, pending a decision about how to move the project forward.

#### Hosting
The entire codebase is hosted on <a href="https://github.com/avtomat-hub/avtomat-aws" target="_blank">GitHub</a>. Packages are published to <a href="https://pypi.org/project/avtomat-aws/" target="_blank">PyPi</a>.

## Conclusion

I created this project to 1. help engineers automate repetitive tasks and 2. get some practice on hosting open-source from scratch. 
It is mostly used internally by my team, however I am confident it can benefit a wider audience.



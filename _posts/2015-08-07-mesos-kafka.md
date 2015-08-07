---
layout: post
title: Terraform Provider for The Kafka Mesos Framework API
excerpt: "Create, update, and destroy Kafka clusters using Terraform"
tags: [mesos, apache, kafka, terraform, automation, devops]
comments: true
---

## Primer

At [Banno JHA](https://banno.com) we are working to automate our infrastructure using Mesos and Terraform. If you are interested in working with us send me an email: nicgrayson \<at\> gmail \<dot\> com

### Apache Kafka - [kafka.apache.org](http://kafka.apache.org)

Apache Kafka is a publish-subscribe messaging rethought as a distributed commit log.

### Apache Mesos - [mesos.apache.org](http://mesos.apache.org)

Apache Mesos abstracts CPU, memory, storage, and other compute resources away from machines (physical or virtual), enabling fault-tolerant and elastic distributed systems to easily be built and run effectively.

### Terraform - [terraform.io/intro/index.html](https://terraform.io/intro/index.html)

Terraform is a tool for building, changing, and versioning infrastructure safely and efficiently.

## Mesos Framework Overview

This Mesos frameowork provides a command line interface and a REST API. This framework allows operators to manage and update a Kafka cluster. The management of the cluster is performed manually each time a cluster needs to be modified. More information about this framework is on the Github Project [github.com/mesos/kafka](https://github.com/mesos/kafka).

## Terraform Provider Overview

Using the framework's API we are able to create, update, and destroy a cluster.

## Starting the Framework Scheduler

Start the scheduler with this command:
{% highlight bash %}
$ kafka-mesos.sh scheduler
{% endhighlight%}
I would suggest launching the scheduler with [Marathon](https://mesosphere.github.io/marathon/) to ensure it's uptime.

## How to use the Terraform Provider

### Install
{% highlight bash %}
$ go get github.com/Banno/terraform-provider-mesoskafka
{% endhighlight %}

### Configuring the Provider

The provider can be configured manually via
{% gist nicgrayson/945ed507ea5ff00d48a2 provider.tf %}

or with environmental variables:
{% highlight bash %}
export MESOS_KAFKA_URL=http://mesoskafka:7000
{% endhighlight %}

### Create Terraform Resource
{% gist nicgrayson/945ed507ea5ff00d48a2 resource.tf %}

## Example Run with Output

### Terraform Plan
{% gist nicgrayson/945ed507ea5ff00d48a2 terraformplan %}

### Terraform Apply
{% gist nicgrayson/945ed507ea5ff00d48a2 terraformapply %}

### Terraform Destroy
{% gist nicgrayson/945ed507ea5ff00d48a2 terraformdestroy %}

## Follow-up

Any issues with using this provider can be opened on the [Github Project](https://github.com/Banno/terraform-provider-mesoskafka/issues)

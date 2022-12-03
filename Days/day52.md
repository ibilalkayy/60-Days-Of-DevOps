On the fifty second day, I learned the following things about Continuous Monitoring.

# Continuous Monitoring Tool

- Monitoring is required after deployment of an application.

- Here you will monitor the bugs, errors or exploitation in an application after deployment.

## Why we need continuous monitoring?

We need it to avoid 

- Our application downtime and reduce it.

- Failure inside CI/CD pipeline.

- Application failure.

- Infrastructure failure.

- Analysis of code failure.

## Phases of continuous monitoring

- Define -> Develop a monitoring strategy(monitoring the pipeline, github code, build code, etc).

- Establish -> How frequently you're going to monitor it.

- Implement.

- Analyze data and report finding.

- Respond based on errors/failures.

- Review and update.

## Monitoring tools

- Nagios

- Splunk

- Prometheus

- ELK

- Librato

- Amazon Cloudwatch

- Sensu

## Nagios

- We are going to discuss nagios because it is commonly used nowadays.

- Nagios is an open source software for continuous monitoring of systems, networks, and infrastructure. It runs plugins that are stored on a server which is connected on a host or another server on your network or the internet. In case of any failure, nagios alerts about the issues so that the technical team can perform recovery process immediately.

- It's a client-server architecture.

- Usually on a network, a nagios server is running on a host and the plugins are running on all the remote host which you should monitor.

## History of Nagios

- In year 1999, Ethan galstad developed it as a part of Netsaint distribution.

- In 2002, Ethan renames the project to "Nagios" because of the trademark issues with the name "Netsaint".

- In 2009, Nagios released its first commercial version Nagios XI.

- In 2012, Nagios was again renamed as Nagios core.

- It uses port numbers 5666, 5667, and 5668 to monitor its client. These port numbers can be changed because they're logical. You can change them in the configuration file if you want to.

## Why Nagios?

We use nagios because it

- Detect all types of network, or server issues.

- Helps you to find the root cause of the problem which allow you to get the permanent solution to the problem.

- Reduce downtime.

- Monitors the entire infrastructure actively(nagios server itself tells the client).

- Monitors the entire infrastructure passively(client tells the nagios server).

- Allows you to monitor and troubleshoot server performance issues.

- Automatically fix problems.

## Features of Nagios

- Oldest and latest.

- Good log(reporting) and database system.

- Informative and attractive web interface.

- Automatically server alerts if condition changes.

- Helps you to detect network errors or server crashes.

- You can monitor the entire business process and IT infrastructure with a single time(in one time)

- Monitors the network services like http, smtp, snmp, ftp, ssh, pop, DNS, LDAP, IPMI etc.

## Nagios Architecture
                                                                                                 ------------------
    Web page dashboard  <---------------       Configuration files                   ssh         | -------------- |
                                       ↑             ↑                      ------------------>  | | nrpe agent | |
                                -------↑-------------↑-----------           ↑                    | -------------- |
                                |      ↑             ↑          |           |                    ------------------
                                |      ↑      -------↑-------   |           |
                                |      ↑      |   IP Add.   |   |           |                    ------------------
                                |      ↑      | User & Pass |   |           |        ssh         | -------------- |
                                |      ↑      ---------------   |           |  --------------->  | | nrpe agent | |
                                |      ↑              ↓         |           |  ↑                 | -------------- |
                                |    --↑---      ---------- ---------> ----------                ------------------
                                |    | DB | <--- | Daemon |     |      |  NRPE  |             
                                |    ------      ---------- <--------- ----------                ------------------
                                |                               |              ↓     ssh         | -------------- |  
                                ---------------------------------              --------------->  | | nrpe agent | |
                                        Nagios - Server                                          | -------------- |
                                                                                                 ------------------
                                                                                                     Client/Node

- Nagios server contains the configuration files in which all the things like ip address, http, smtp etc, username and password of all nodes are present and these nodes will be represented through this configuration data(ip, username, etc).

- The daemon will collect the data from the configuration files to perform the functionalities.

- Once the data is received in the daemon, it will call a plugin that is called NRPE(Nagios remote plugin executor) and that plugin will collect data from the nodes and store it in its own database. 

- The connection will be through ssh.

- On the receiving side of the node, there is another plugin called the nrpe agent that will build the connection, receive the requests and responed the status of the nodes.

- The status will go back to the NRPE and it will be given to the daemon.

- Once the status is received in the daemon, it will be given to the database for storage.

- The data will now be available on the webpage dashboard. You can access it via the internet.

- Main configuration file path of nagios is `/usr/local/nagios/nagios.cfg`.

- All monitoring things are called "service". For example: 5 nodes and 4 things running on them. It means you're monitoring 5x4 = 20 services.

## Prerequisites

- httpd

- php

- gcc & gd (compiler to convert raw data into binaries)

- makefile (to build)

- perl (script)

## **Explaining it in a video**

Here you can get an explanation in a video. [52/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=FkpzMbV_e4w&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=61)
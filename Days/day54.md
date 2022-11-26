On the fifty forth day, I learned the following things about Cloud Computing.

## Cloud Computing

- Cloud computing is an on-demand delivery of computer power, database, storage, applications and other IT resources through a cloud service platform(aws, azure, gcp, etc) via the internet with pay-as-you-go pricing model.

## Problems before cloud computing

- Before cloud computing, when you were starting a company, You already need the following items in advance.

    - Let's say you wanted 4 servers.
        - One AD server
        - One DNS server
        - Two Application servers
    - Router
    - Switch
    - Cabling
    - Gateway
    - Firewall
    - AC to cool the servers down
    - 24x7 electricity
    - Employees to maintain these servers in day and night

- Opex was required. It means that the employees expenditure was required to maintain the resources.

- It needed so much cost to install all of them.

- It required many days to install them.

- If the business failed, then this investment was wasted.

## Characteristics of Cloud computing

- On demand self-service.

- Broad network access(Access it from anywhere in the world through internet).

- Scalability(Increase or decrease the number of servers).

- Resource pooling(Get the required number of servers from a pool or a collection of servers).

- Measured services(Analysis about the traffic that visited the servers).

## Top players in Cloud

- AWS (Amazon Web Services)

- Microsoft Azure

- GCP (Google Cloud Platform)

- Alibaba Cloud

- Oracle

## History

- AWS was launched in 2006.

- AWS completely moved to Amazon.com in 2010.

- AWS certification started in 2013.

- The profit got doubled in 2015, 2016.

- They discussed about the virtual reality, AI, etc in a 2017 Re-invent conference.

## Services in cloud

- There are three services in a cloud that it provides.

    - IAAS(Infrastructure as a service).
    - PAAS(Platform as a service).
    - SAAS(Software as a service).

                                        --------------> -------------------
                                        |               |   Application   |
                                        |               |------------------
                                        |               |      Data       |
                                        |               |------------------ <--
                                        |               |     Runtime     |   |
                                        |               |------------------   |
                                        |               |    Middleware   |   |
                                        |           --> |------------------   |
                                SAAS    |           |   |       OS        |   |
                                        |           |   |------------------   |   PAAS
                                        |           |   | Virtualization  |   |
                                        |           |   |------------------   |
                                        |   IAAS    |   |     Server      |   |
                                        |           |   |------------------   |
                                        |           |   |     Storage     |   |
                                        |           |   |------------------   |
                                        |           |   |     Network     |   |
                                        ----------->--> ------------------- <--

- The OS, virtualization, server, storage, and network services that you take from the cloud is called IAAS.

- The above ones including the middleware and the runtime services that you take from the cloud is called PAAS.

- All the above ones including the application, and the data services that you take from the cloud is called SAAS.

## Deployment Model of Cloud

There are three deployment models of cloud.

- Public Cloud
- Private Cloud
- Hybrid Cloud

**Public Cloud:** Public cloud is for general users that anyone can use it. E.g. AWS, Azure, GCP.

**Private Cloud:** Private cloud is only used in an enterprise and in its different branches for its company usage. It is in your own hands, so it is secure.

**Hybrid Cloud:** Big companies uses both public cloud and private cloud. Azure provides the better facility of providing the hybrid cloud. You can merge public and private clouds in Azure.

## Virtualization

- The network, storage and server should be virtualized in order to run them.

- You need a hypervisor to make the network, storage, and server virtualized. Hypervisor divides and allocates the resources of network, storage, and server.

- There are different hypervisors for different companies.

    - Microsoft has hyper-v.
    - AWS has citrix.
    - VMWare has ESXi.

- You can only use cloud if you have the virtualization installed.

## **Explaining it in a video**

Here you can get an explanation in a video. [54/60 Day of DevOps Challenge]()
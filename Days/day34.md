On the thirty forth day, I learned the following things about Prometheus.

## Prometheus Installation

- Go to this [website](https://prometheus.io/download/) and download the prometheus according to your operating system.

- For linux type, `wget <link-of-the-tar-file>` and it will download the tar file for you.

- Untar the file by writing, `tar -xvf <file-name>` and then enter the directory using `cd`.

- Open the *prometheus.yml* file using the `cat` command and it will show the targets that needs to be scraped and also the time interval for scrapping metrics.

- Once you open the rules, it will show you the scrape_interval, alertmanager configuration, the rules that you can setup yourself, and the scrape configuration that is available on a particular port number.

- By default, scrape configuration contains only one endpoint to scrape. It means that the prometheus itself will be scraped on a given port number.

- `./prometheus` will execute prometheus. After activation, if you type `localhost:9090` in the browser, it will redirect you to the prometheus dashboard.

- To run prometheus as a service, first type `sudo cp -r . /usr/local/bin/prometheus`. It will copy the prometheus directory data to the `/usr/local/bin/prometheus` directory.

- After that create a *.service* file inside */etc/systemd/system* directory. Simply write `sudo vi /etc/systemd/system/prometheus.service` in the terminal and enter the following data in it.

      [Unit]
      Description=Prometheus Service
      After=network.target

      [Service]
      Type=simple
      ExecStart=/usr/local/bin/prometheus/prometheus --config.file=/usr/local/bin/prometheus/prometheus.yml

      [Install]
      WantedBy=multi-user.target

- Save the data inside the file and start the service file by writing `sudo service prometheus start`.

- After that, check the status of the service by typing `sudo service prometheus status`. It will show you that the service is running.

- If you write `localhost:9090` in the browser, you will see that the prometheus dashboard is opened.

- You can click on the check boxes to enable the local time or enable query history and much more.

- You will see the search bar in which you will type the expression that you would like to execute.

- The expression will be executed in the table and in the graph form.

- In the end of the page, you will see a button by the name **Add Panel**, through which you can add multiple panels if you want. In this way, you can execute different queries all at once.

- On the search bar, if you move to right side, you will see the small world map. If you click on it, it will give you a pop window of metrics explorer. Scroll down and click on the **up** option. It will give you this message `up{instance="localhost:9090", job="prometheus"}`.

- You can check the data both in the form of table and graph.

- If you type **go_info** in the search bar, you will you will get the result with the go version also `go_info{instance="localhost:9090", job="prometheus", version="go1.19.2"}`.

- If you click on alerts, it will show you nothing because we don't have one. Alerts are the conditions that you have to specify. If the conditions are satisfied, then the alert will be shown to the maintainer/manager.

- Inactive - If the condition is not satisfied.
- Pending - If the condition is satisfieid.
- Firing - If it exceeds the critical limit.

Click on the status button. It will show seven different options.

**1. Runtime and build information:** It will show the information of prometheus.

**2. TSDB status:** TSDB is the time-series database. This option allows to check the databases statuses like the number of series or the number of chunks. You can take the name and search it as a query 

**3. Command line flags:** These are the flags that you can use to make changes in your service file and show the information of the service file.

**4. Configuration:** Configuration contains the data that is present in the *prometheus.yml* file.

**5. Rules:** Rules are the conditions that you specify.

**6. Targets:** At first, only one endpoint `http://localhost:9090/metrics` is getting monitored. If you write `http://localhost:9090/metrics` in the browser, you will see nice format of the prometheus metrics.

- **Help** is the description of what the metric is. It helps in the readibility.
- **Type** will give you the type of a metrics.

**7. Service Discovery:** It will show you the endpoint that is scraped and discover the labels.

## Prometheus Node exporter

- Node exporter is a way to measure various machine resources. Machine resources could be your memory, disk, cpu utilization.

- Go to this [website](https://prometheus.io/download/) and scroll down to find the node exporter. Copy the tar file link and write `wget <link-of-the-node-exporter>`.

- After downloading the file, untar the file by writing `tar -xvf <file-name>`.

- List all the files inside that tar file and you will see that *node_exporter* file there. Copy the *node_exporter* file to the */usr/local/bin* directory by typing `sudo cp node_exporter-1.4.0.linux-amd64/node_exporter /usr/local/bin`.

- Create a service for the node exporter also by typing `sudo vi /etc/systemd/system/node-exporter.service` and type the following data inside that file.

      [Unit]
      Description=Prometheus Node Exporter Service
      After=network.target

      [Service]
      Type=simple
      ExecStart=/usr/local/bin/node_exporter

      [Install]
      WantedBy=multi-user.target

- After that, reload the system by typing `systemctl daemon-reload`.

- Once the system is reloaded, type `sudo service node-exporter start` to star the node exporter. You can check the status of it by writing `sudo service node-exporter status`.

- Type `http://localhost:9100/` in the browser because the node runs in the *9100* port.

- You can check the metrics by typing `http://localhost:9100/metrics` in the browser.

- After the node exporter is running, let's configure the node exporter into our *prometheus.yml* file.

- Type `cd /usr/local/bin` to go inside the *bin* directory and then go to the *prometheus* directory. Now edit the *prometheus.yml* file by typing `sudo vi prometheus.yml` and the add the following job in it and save it.

      - job_name: "node-exporter"
        static_configs:
          - targets: ["localhost:9100"]

- After saving the file, type `sudo service prometheus restart` to restart prometheus and then check the status of it by typing `sudo service prometheus status`.

- Go to the browser and type `http://localhost:9090/`. Go to the status and open the Service Discovery. You will see that the node-exporter is added.

- Go to the configuration and check the configuration file. After that check out the metrics in the search bar. You will see that new metrics are added by the name of node. Click on any of the node metrics and it will show you the details.

- You can stop the node-exporter by typing `sudo service node-exporter start`

- You can stop the prometheus service by typing `sudo service prometheus stop`.

## **Explaining it in a video**

Here you can get an explanation in a video. [34/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=S-d1GCP4QKM&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=32)
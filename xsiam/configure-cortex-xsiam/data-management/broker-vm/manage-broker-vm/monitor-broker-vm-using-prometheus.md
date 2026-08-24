---
description: Monitor Cortex XSIAM Broker VM metrics with Prometheus.
---

# Monitor Broker VM using Prometheus

Learn more on monitoring the Broker VM using Prometheus.

You can enable local monitoring of the Broker VM to provide usage statistics in a Prometheus metrics format. You can tap in and export data by navigating to `http://<broker_vm_address>:9100/metrics/`. By default, monitoring is disabled.

### Prerequisite

To monitor the Broker VM using Prometheus, ensure that you enable monitoring on the Broker VM. This is performed after configuring and registering your Broker VM, when you can edit existing configurations and define additional settings in the Broker VMs page.

1. Select Settings → Configurations → Data Broker → Broker VMs.
2. In the Broker VMs table, locate your Broker VM, right-click, and select Configure.

{% hint style="info" %}
#### Note

For all Broker VM nodes added to a HA cluster, you can also Configure the Broker VM nodes from the Clusters tab.
{% endhint %}

3. In the Broker VM Configurations page, select Monitoring from the left pane.
4. Clear the Use Default (Disabled) checkbox.
5. In the Montoring menu, select Enabled.
6. Click Save.

### How to set up Prometheus and Grafana to monitor the Broker VM

Below is an example of how to set up Prometheus and Grafana to monitor the Broker VM. This is set up using a docker compose on an Ubuntu machine to monitor the CPU usage.

Perform the following procedures in the order listed below.

#### Task 1. Install Docker and Docker Compose

1.  Update your Ubuntu system:

    ```bash
    sudo apt update
    ```
2. Install Docker:

{% hint style="info" %}
#### Note

For more information on Docker, see the [Docker website](https://www.docker.com/).
{% endhint %}

```bash
sudo apt install docker.io
```

3.  Start the Docker service:

    ```bash
    sudo systemctl start docker
    ```
4.  Enable Docker to start on boot:

    ```bash
    sudo systemctl enable docker
    ```
5.  Install Docker Compose:

    ```bash
    sudo curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
    ```

#### Task 2. Create a Docker Compose file

This task includes setting up Prometheus and Grafana.

1.  Create a file named `docker-compose.yml`, and open it for editing:

    ```bash
    vim docker-compose.yml
    ```
2.  Add the following content to the file:

    ```yaml
    version: '3.8'
    services:
      prometheus:
        image: prom/prometheus:latest
        container_name: prometheus
        restart: unless-stopped
        volumes:
          - ./prometheus.yml:/etc/prometheus/prometheus.yml
          - prometheus_data:/prometheus
        command:
          - '--config.file=/etc/prometheus/prometheus.yml'
          - '--storage.tsdb.path=/prometheus'
          - '--web.console.libraries=/etc/prometheus/console_libraries'
          - '--web.console.templates=/etc/prometheus/consoles'
          - '--web.enable-lifecycle'
          - '--log.level=debug'
        ports:
          - '9090:9090'
      grafana:
        image: grafana/grafana-enterprise
        container_name: grafana
        restart: unless-stopped
        ports:
          - '3000:3000'
        volumes:
          - grafana_data:/var/lib/grafana
    volumes:
      grafana_data: {}
      prometheus_data: {}
    ```
3. Save and close the file.

#### Task 3. Create a Prometheus configuration file

You need to configure Prometheus to scrape the Broker VM metrics by creating a Prometheus configuration file.

1. Create a Prometheus configuration file named `prometheus.yml` in the same directory as the `docker-compose.yml` file that you created above.
2.  Open the `prometheus.yml` file for editing:

    ```bash
    vim prometheus.yml
    ```
3.  Add the following content to the file:

    ```yaml
    global:
      scrape_interval: 15s
      scrape_timeout: 10s
    scrape_configs:
      - job_name: 'prometheus'
        static_configs:
          - targets: [':9090']
      - job_name: 'node'
        static_configs:
          - targets: [':9100']
    ```
4. Save and close the file.

#### Task 4. Run Docker Compose

1.  In the terminal, run the following command from the project directory:

    ```bash
    docker-compose up -d
    ```
2.  Verify that Prometheus is running correctly:

    ```bash
    docker-compose logs -f prometheus
    ```

#### Task 5. Access Grafana and Set Up Prometheus as a Data Source

1. Open a web browser and go to `http://<your server>:3000`.
2. Log in to Grafana using the default credentials.

* Username: `admin`
* Password: `admin`

3. Set up Prometheus as a data source:
4. In the left pane, select Administation → Data sources.
5. Click Add data source, and select Prometheus.
6. Under HTTP, set the URL to `http://<your server IP address>:9090`.
7. To verify the connection, click Save & Test.

#### Task 6. Create Dashboards in Grafana

You can now create dashboards in Grafana to visualize the data from Prometheus.

1. In Grafana, on the left pane, click Dashboards.
2. Select New and create a new dashboard.
3. Add a panel to the dashboard and configure the dashboard to display the Prometheus metrics that you want.
4.  To monitor CPU usage, use the following metric:

    ```
    100 - (avg by (instance) (rate(node_cpu_seconds_total{job="node",mode="idle"}[1m])) * 100)
    ```

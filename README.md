# Monitoring Environment

This project sets up a basic monitoring environment using Docker, Grafana, Prometheus, and Node Exporter.

### Prerequisites

Docker Engine and Docker Compose installed on the system. 

In case both are not installed, the instructions can be found below (retrieved from https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository)

    # Add Docker's official GPG key:
    sudo apt-get update
    sudo apt-get install ca-certificates curl gnupg
    sudo install -m 0755 -d /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    sudo chmod a+r /etc/apt/keyrings/docker.gpg

    # Add the repository to Apt sources:
    echo \
      "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
      "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    sudo apt-get update

    # Install the latest Docker Engine and Docker Compose version:
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

    # Verify that the Docker Engine installation is successful by running the hello-world image:
    sudo docker run hello-world

    # Verify that Docker Compose is installed and working: 
    sudo docker compose version

### Installation

1. Clone this repository to your local machine:
      
        git clone https://github.com/coffeeandtv07/monitoring_env.git
      

2. Go to the project directory:

        cd monitoring_env

The project's configuration files are in docker-compose.yml and prometheus.yml files. 

Main Docker container configuration is in docker-compose.yml -- this config defines the 'monitoring' network, and specifies the Grafana, Node Exporter, Prometheus service settings.
Settings include image sources, volumes that should be mounted, custom commands the services should be executed with, and ports to bind the services to.
Make sure that ports 3000, 9100, 9090 are allowed in your firewall.

The prometheus.yml config specifies the scrape interval and job names that should be scraped. Apart from the Prometheus and Node Exporter, no other custom jobs are included into the config.
Jobs like 'cpu' and 'memory' are included into Prometheus by default.

3. Start the monitoring environment:

        sudo docker-compose up -d

This command will pull the necessary Docker images and start the services. The following commands stops the Docker container:

        sudo docker-compose down
        
### Usage

Grafana: 

Access the Grafana dashboard at http://localhost:3000 or http://[your_server_ip]:3000. 
The default login credentials are:

    Username: admin
    Password: tgpSbeYzGAyxDt
  
Grafana Dashboards can be configured afterwards. Refer to https://grafana.com/docs/grafana/latest/dashboards/ for documentation.

Prometheus: 

Access the Prometheus UI at http://localhost:9090 or http://[your_server_ip]:9090.

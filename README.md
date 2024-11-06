### How to Install and Configure GitLab Using Docker Compose

#### Introduction:

* GitLab is a powerful platform for managing Git repositories, continuous integration/continuous delivery (CI/CD) pipelines, and DevOps workflows. 
* If you want to set up GitLab on your local machine for personal projects or team collaboration, Docker Compose offers a simple and efficient way to manage the installation.

#### Prerequisites:

Before getting started, make sure you have the following tools installed and configured on your local machine:

* Docker Desktop: Ensure that Docker is installed and running. You can download it from the official Docker website.
* Basic understanding of Docker and Docker Compose: Familiarity with Docker commands and Docker Compose configuration files will be helpful.
* Internet access: You must pull the GitLab Docker image from Docker Hub.

With these prerequisites covered, let’s dive into the steps to get GitLab running on your local machine.

#### Step 1: Create a docker-compose.yml File

To begin, could you please define the Docker Compose configuration for GitLab? This file will specify the services (GitLab in our case), ports, and volume mounts for persisting data.

Create a docker-compose.yml file in your project directory using the content from the docker-compose.yml file. 


##### Breakdown of the docker-compose.yml File:

* version: Specifies the Docker Compose version.
* services: Defines the GitLab service with its image (gitlab/gitlab-ce:latest).
* platform: Ensures compatibility with Linux/AMD64, which is especially useful for Mac users with ARM-based processors (Apple Silicon).
* hostname: Sets the hostname (replace 162.148.1.124 with your IP address if necessary).
* ports: Maps GitLab’s internal ports to your local machine.
* 443: HTTPS
* 80: HTTP
* 22: SSH for Git access
* volumes: Mounts directories to persist GitLab’s configuration, logs, and data between restarts.

#### Step 2: Launch GitLab with Docker Compose

Once you have the docker-compose.yml file set up, navigate to the directory where the file is located in your terminal and run the following command to start GitLab:

* docker-compose up -d

The -d flag runs the containers in detached mode, meaning they will run in the background. Docker will pull the required GitLab image and start the GitLab service.

#### Step 3: Access GitLab

* Once the installation is complete, you can access GitLab through your browser.
* You can open a browser and navigate to http://localhost (or replace localhost with the IP address you specified as the hostname, such as 162.148.1.124).

You will be prompted to set the root user's initial password. Once you do so, you can log in to GitLab and create your repositories and projects.

#### Step 4: Manage GitLab with Docker Compose

Docker Compose makes managing your GitLab instance easy. Below are a few essential commands you might need:
* docker-compose down   -> ***The command will stop GitLab and remove the containers.***
* docker-compose logs -f  -> ***The command will display the real-time logs from the GitLab container.***
* docker-compose restart -> ***The command will restart GitLab.***

#### Generate the Password
* docker exec -it <gitlab-container-name> /bin/bash
* gitlab-rails console -e production
* Enter the following commands:
```
bash
  user = User.find_by(username: 'root')
  user.password = 'new_password'
  user.password_confirmation = 'new_password'
  user.save!
```

#### Step 6: Configure GitLab’s external_url

If you want to set a custom external URL for GitLab (e.g., http://localhost or a custom domain), you can modify the GitLab configuration file directly from the container.

Run the following command to set the external_url:

* docker exec -it gitlab bash -c "echo \"external_url 'http://localhost'\" >> /etc/gitlab/gitlab.rb && gitlab-ctl reconfigure"

This will set the external URL to http://localhost and apply the configuration.


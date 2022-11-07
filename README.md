# Learning Objectives

## Run and Manage Containers

### Task 1.
1. Configure `Podman` to search the registry `registry-1:5000` last.
2. Configure the registry as an insecure registry.
### Task 2.
1. Pull the latest Nginx image `docker.io/library/nginx`.
2. Start a container using the Nginx image with the following:
    - Name = `web-vol`
    - Mount local directory `/home/cloud_user/web` to container as `/usr/share/nginx/html`
    - Run the container in the pod named `task-2` by using the podman option `--pod task-2`
3. Verify you can access the web page by using `curl localhost:8081`.
4. Save a copy of the container logs to a file named `web-vol.log`.
### Task 3.
1. Pull the latest MySQL image `docker.io/library/mysql`.

2. Start a container using the MySQL image with the following:
     - `/name=mysql-llama`
     - `MYSQL_PASSWORD=badpass`
     - `MYSQL_USER=guru`
     - `MYSQL_ROOT_PASSWORD=supersecret`
     - `MYSQL_DATABASE=llama`
     - Publish port `3306` on the container to port `3306` on the localhost

3. Verify the MySQL instance is running with the following command, and check that the llama database is there:

    - `echo "show databases;" | mysql -uguru -pbadpass --protocol tcp -h localhost`
4. Make a directory named `mysql_logs` and copy the log file `/var/lib/mysql/mysql/general_log_213.sdi` to the directory.

### Task 4.
1. Start a Nginx container from `registry-1:5000` using a tag that is NOT `latest`. Use the following parameters:
    - `name=web-default`
    - Publish port `80` in the container to `localhost` port `8080`
2. Verify you can access the web page with `curl localhost:8080`.
3. Start a Bash shell on the container and modify `/usr/share/nginx/html/index.html` in the container, then change the current message to `A guru was here!`.
4. Verify you can access the web page with `curl localhost:8080` and see your new message.
5. Commit the modified container to a new image named `registry-1:5000/nginx:web-guru`.

## Build and Run Custom Images

### Task 5.
1. Push your new image to `registry-1:5000`.
2. Stop the container web-default and start a new container using your new image. Use the following parameters:
    - `name=web-guru`
    - Publish port `80` in the container to `localhost` port `8080`
1. Verify you get your custom message with curl localhost:8080.
2. Save your new image as a tar file named guru-web.tar.

### Task 6.
1. Complete the incomplete Dockerfile located at /home/cloud_user/docker/Dockerfile. Details are listed in the [incomplete Dockerfile](https://github.com/linuxacademy/Red-Hat-Certified-Specialist-in-Containers-and-Kubernetes/blob/main/Dockerfile_exam_lab).

### Task 7.
1. Build an image from the completed Dockerfile in task 6. The image should be built with the following:
    - `name=llama-cart`
    - `tag=v1`
2. Start a container with the new image using the following settings:
    - `name=llama-web`
    - Publish port `90` in the container to `localhost` port `8090`
3. Verify the image works by putting your lab-system-name:8090 or IP-Address:8090 into a web browser.
    - Alternatively, use `curl localhost:8090` and see just the text version of the page.

## Creating Applications with OpenShift

## Task 8.
1. Create a new project.
    - (CodeReady Containers only)
        - Create a new project named `guru-php` with display name of `Test hello guru project`
    - (Red Hat OpenShift Sandbox)
        - Skip this and use default project `username-dev`
2. Create a new PHP application with the following:
    - [Git repo](https://github.com/linuxacademy/Red-Hat-Certified-Specialist-in-Containers-and-Kubernetes)
    - Use the Git repo context directory `php-hello-world`
    - Create app as a deployment config
    - Label `app=hello-guru`

## Task 9.
1. Create a new project.
    - (CodeReady Containers only)
         - Create a new project named `inventory`
    - (Red Hat OpenShift Sandbox)
        - Skip this and use default project `username-stage`
2. Download the following template:
[OpenShift Template](https://raw.githubusercontent.com/linuxacademy/Red-Hat-Certified-Specialist-in-Containers-and-Kubernetes/main/multi-container/multi_test.yaml)
3. Publish the template to the current project.
4. Process the template and save to a file named `processed_template.yaml`. Set the following parameters and label:
    - `NAME=fruit-stand`
    - `DATABASE_NAME=fruit_stand`
    - `DATABASE_USER=guru`
    - `DATABASE_PASSWORD=badpass`
    - `DATABASE_ADMIN_PASSWORD=badidea`
    - `label app=guru-fruit`
Create the application using the saved file `processed_template.yaml`.

## Task 10.
1. Create the following directories inside your home directory:
    - `logs/pod-fruit-stand`
    - `logs/pod-postgres`
2. Sync the directory `/var/log` from each running pod to previously created directories.
    - Put the logs from the fruit-stand application pod in `logs/pod-fruit-stand`
    - Put the logs from the postgresql application pod in `logs/pod-postgres`

Here's a step-by-step README file to guide you through creating a Docker Hub public repository, containerizing an Apache web server, uploading the image, and having a friend pull and build it.

---

# Dockerize Apache Web Server and Share via Docker Hub

## Step 1: Create a Docker Hub Public Repository

1. **Log in to Docker Hub**:
   - Go to [Docker Hub](https://hub.docker.com/).
   - Log in with your Docker Hub account. If you don't have an account, create one.

## Step 2: Containerize Apache Web Server

1. **Create an `index.html` File**:
   ```html
   echo '<!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Apache Docker</title>
   </head>
   <body>
       <h1>Docker is a platform that enables developers to create, deploy, and run applications in containers.</h1>
       <p>Containers are lightweight, standalone, and executable packages that include everything needed to run software.</p>
       <p>To create a container, you need a base image (from Docker Hub) or a custom image built using a Dockerfile.</p>
       <p>The main purpose of container technology is to ensure that applications work consistently across different environments, from a developer's local machine to production servers. Unlike virtual machines, which take longer to boot and consume more resources, containers start almost instantly and share the host OS kernel, making them more efficient.</p>
       <p>Created by Dzidzogbe Logotse</p>
   </body>
   </html>' > index.html
   ```

2. **Create a Dockerfile**:
   ```bash
   echo 'FROM fedora
   LABEL Engineer="Dzidzogbe Logotse"
   LABEL description="This Dockerfile deploys and manages an Apache web server."
   RUN yum -y update && yum install -y httpd
   COPY index.html /var/www/html/
   ENTRYPOINT ["/usr/sbin/httpd"]
   CMD ["-D", "FOREGROUND"]' > Dockerfile
   ```

3. **Build the Docker Image**:
   ```bash
   docker build -t my-apache-image:v1 .
   ```

## Step 3: Upload Image to Docker Hub

1. **Log in to Docker Hub**:
   ```bash
   docker login
   ```
   It will prompt you to enter username and password
   
3. **Tag the Image for Docker Hub**:
   ```bash
   docker tag my-apache-image:v1 your-dockerhub-username/my-apache-image:v1
   ```

4. **Push the Image to Docker Hub**:
   ```bash
   docker push your-dockerhub-username/my-apache-image:v1
   ```

## Step 4: Have a Friend Pull and Build the Image

1. **Share Repository Information with Your Friend**:
   - Tell your friend to pull the image using the repository name.

2. **Friend Pulls the Image**:
   ```bash
   docker pull your-dockerhub-username/my-apache-image:v1
   ```

3. **Friend Runs the Container**:
   ```bash
   docker run -d -p 80:80 your-dockerhub-username/my-apache-image:v1
   ```

4. **Access the Apache Web Server**:
   - Open a web browser and go to `http://localhost` to see the web page served by the Apache web server.
                                                                    ( See screeshot attached)
---

This README provides a step-by-step guide for creating a Docker Hub public repository, containerizing an Apache web server, uploading the image to Docker Hub, and having a friend pull and build the image.

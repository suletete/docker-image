
---

# **Working with Docker Images**

## **1. Introduction to Docker Images**
Docker images are the foundation of containers. They are lightweight, portable, and self-sufficient packages that include everything needed to run an application—such as the code, runtime, libraries, and system tools.

Images are created using a `Dockerfile`, which contains instructions for configuring the application environment.

---

## **2. Pulling Images from Docker Hub**
Docker Hub is a cloud-based registry for Docker images. You can explore and pull images using the following commands:

### **Search for an Image**
```bash
docker search ubuntu
```
- The **OFFICIAL** column in the output shows whether the image is verified by the organization that maintains it.

### **Pull an Image**
```bash
docker pull ubuntu
```

### **List Downloaded Images**
```bash
docker images
```

---

## **3. Creating a Dockerfile**

### **What is a Dockerfile?**
A Dockerfile is a plain text file with instructions for building a Docker image. It automates the environment setup.

### **Example Dockerfile (Using NGINX)**
Assume you have an `index.html` file in the same directory. Here’s a basic Dockerfile:

```Dockerfile
# Use the official NGINX base image
FROM nginx:latest

# Set the working directory
WORKDIR /usr/share/nginx/html/

# Copy local HTML file to container
COPY index.html /usr/share/nginx/html/

# Expose port 80 for external access
EXPOSE 80
```

### **Create the HTML File**
```bash
echo "Welcome to Darey.io" >> index.html
```

### **Build the Docker Image**
```bash
docker build -t dockerfile .
```

### **Run the Docker Container**
```bash
docker run -p 8080:80 dockerfile
```

This binds the container's port 80 to your EC2 instance's port 8080.

---

## **4. Configure EC2 Security Group**

To allow traffic to your container:

1. Go to **EC2 Dashboard > Instances > Your Instance**.
2. Click on **Security Tab > Security Group > Edit Inbound Rules**.
3. Add a new rule:
   - Type: **Custom TCP**
   - Port Range: **8080**
   - Source: **Anywhere (0.0.0.0/0)**

---

## **5. View Containers**

### **List All Containers**
```bash
docker ps -a
```

### **Start a Stopped Container**
```bash
docker start <CONTAINER_ID>
```

---

## **6. Access Your App**
Visit:  
```
http://<your-ec2-public-ip>:8080
```

---

## **7. Push Docker Image to Docker Hub**

### **Step-by-Step Guide**

1. **Create Docker Hub Account** (if not done).
2. **Create a Repository** on Docker Hub.
3. **Tag Your Image**:
   ```bash
   docker tag dockerfile <dockerhub-username>/<repo-name>:v1
   ```
4. **Login to Docker Hub**:
   ```bash
   docker login -u <dockerhub-username>
   ```
5. **Push the Image**:
   ```bash
   docker push <dockerhub-username>/<repo-name>:v1
   ```
6. **Verify on Docker Hub**: Navigate to your Docker Hub repo and confirm the image is listed.

---

## **8. Side Hustle Task: Dockerize a Basic Web Static Page**

### **Checklist**

- ✅ Launch and connect to an **Ubuntu EC2 instance**
- ✅ Install Docker and set it up
- ✅ Create a `Dockerfile` with NGINX and a static HTML file
- ✅ Build the Docker image
- ✅ Run the container and expose it on port 8080
- ✅ Add a rule in EC2's Security Group for port 8080
- ✅ Access your static page via browser
- ✅ Push your custom Docker image to Docker Hub

---

## **Tips**
- Use descriptive names for your images and containers.
- Comment your `Dockerfile` for clarity.
- Confirm your app runs properly before pushing to Docker Hub.

---

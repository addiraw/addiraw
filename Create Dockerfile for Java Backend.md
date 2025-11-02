Perfect! Let’s go step by step to **containerize your Java backend with Docker** and **deploy it on an AWS EC2 instance**. I’ll give you a **clear workflow** from Dockerfile → building → running → EC2 deployment.

---

# 🧱 Step 1: Create Dockerfile for Java Backend

Assuming your backend is a **Spring Boot app packaged as a JAR** (`app.jar`):

**Dockerfile**

```Dockerfile
# Use official OpenJDK image
FROM openjdk:23-jdk-slim

# Set working directory
WORKDIR /app

# Copy the Spring Boot JAR
COPY target/app.jar app.jar

# Expose port your Spring Boot app runs on (default 8080)
EXPOSE 8080

# Run the JAR
ENTRYPOINT ["java", "-jar", "app.jar"]
```

---

# 🧩 Step 2: Build the Docker Image Locally

From your project root (where `Dockerfile` is):

```bash
# Build Docker image, name it 'java-backend'
docker build -t java-backend .
```

Check the image exists:

```bash
docker images
```

---

# 🪝 Step 3: Run Locally (Optional, Test)

```bash
docker run -p 8080:8080 java-backend
```

* `-p 8080:8080` maps container port 8080 to host
* Test in browser or Postman: `http://localhost:8080`

---

# 🛫 Step 4: Push Docker Image to EC2

You have **two main options**:

### Option A — Copy Docker image to EC2

1. Save image as a tar file:

```bash
docker save java-backend -o java-backend.tar
```

2. SCP to EC2:

```bash
scp -i ~/Downloads/mykey.pem java-backend.tar ec2-user@<EC2_PUBLIC_IP>:~/
```
3. Correct way to copy from local machine → EC2

You should run the scp command on your local Mac, not from inside the EC2 instance.

Example from your local terminal:
```
scp -i ~/documents/aditya/sbi/keypair/admin-user.pem \
    ~eclipse-workspace/Spring-boot/java-backend.tar \
    ec2-user@<EC2_PUBLIC_IP>:~/
```

Make sure you are in your Mac terminal, not SSH’ed into EC2.


3. SSH into EC2:

```bash
ssh -i ~/Downloads/mykey.pem ec2-user@<EC2_PUBLIC_IP>
```

4. Load image in EC2:

```bash
docker load -i java-backend.tar
```

5. Run container on EC2:

```bash
docker run -d -p 8080:8080 java-backend
```

* `-d` → run in background
* Your backend is now accessible via `http://<EC2_PUBLIC_IP>:8080`

---

### Option B — Use Docker Hub or AWS ECR (Recommended for Production)

1. Tag the image for Docker Hub:

```bash
docker tag java-backend <your-dockerhub-username>/java-backend:latest
```

2. Push to Docker Hub:

```bash
docker push <your-dockerhub-username>/java-backend:latest
```

3. On EC2, pull and run:

```bash
docker pull <your-dockerhub-username>/java-backend:latest
docker run -d -p 8080:8080 <your-dockerhub-username>/java-backend:latest
```

> ✅ Advantage: You don’t need to manually copy tar files. Good for CI/CD pipelines.

---

# ⚙️ Step 5: Make It Accessible

1. **Check Security Group**

* Open **port 8080** in EC2 Security Group
* Source: 0.0.0.0/0 (or restrict to your IP for testing)

2. Access backend:

```
http://<EC2_PUBLIC_IP>:8080
```

---

# 🧩 Optional: Automate with Docker Compose

If you plan to **add a database (Postgres/Mongo)**:

```yaml
version: '3.8'
services:
  backend:
    image: java-backend
    ports:
      - "8080:8080"
    environment:
      - SPRING_PROFILES_ACTIVE=prod
```

Run on EC2:

```bash
docker-compose up -d
```

---

✅ **TL;DR**

1. Write a **Dockerfile** for your Spring Boot JAR
2. Build & test Docker image locally
3. Either:

   * Copy image tar to EC2 and run, **or**
   * Push to Docker Hub / AWS ECR and pull on EC2
4. Make port 8080 accessible in Security Group
5. Run with `docker run -d -p 8080:8080 java-backend`

---

I can also give you a **full ready-to-use workflow** including:

* **Building Docker image**
* **Pushing to AWS ECR**
* **Running it on EC2 with one command**

Do you want me to do that?



*[First Step](/SSH.md)*


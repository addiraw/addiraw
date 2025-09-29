
docker --version
docker run hello-world

# Use official Java image as base
FROM openjdk:17

# Set working directory in container
WORKDIR /app

# Copy Java source code into container
COPY Main.java .

# Compile Java program
RUN javac Main.java

# Command to run the program
CMD ["java", "Main"]


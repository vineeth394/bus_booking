# Bus Booking App

## Bash Script for Setup maven and Java 

Use the following script to install Java 11, Maven, and set up `JAVA_HOME`:

```bash
#!/bin/bash

set -e

echo "Starting installation of Java 11 and Maven..."

# Install Java 11
if ! java -version &>/dev/null; then
    echo "Installing Java 11..."
    sudo apt update
    sudo apt install -y openjdk-11-jdk
else
    echo "Java is already installed:"
    java -version
fi

# Set JAVA_HOME
JAVA_HOME_PATH=$(dirname $(dirname $(readlink -f $(which java))))
if ! grep -q "JAVA_HOME=$JAVA_HOME_PATH" /etc/environment; then
    echo "Setting JAVA_HOME..."
    echo "JAVA_HOME=$JAVA_HOME_PATH" | sudo tee -a /etc/environment
    echo "export JAVA_HOME=$JAVA_HOME_PATH" | sudo tee -a /etc/profile
    echo 'export PATH=$JAVA_HOME/bin:$PATH' | sudo tee -a /etc/profile
    source /etc/profile
    echo "JAVA_HOME set to $JAVA_HOME_PATH"
else
    echo "JAVA_HOME is already set."
fi

# Install Maven
if ! mvn -version &>/dev/null; then
    echo "Installing Maven..."
    sudo apt install -y maven
else
    echo "Maven is already installed:"
    mvn -version
fi

echo "Setup completed successfully."

========================================================================================================================================================================

How to Build

mvn clean install
mvn spring-boot:run

http://<public-ip>:8080.

==========================================================================================================================================================================
==========================================================================================================================================================================

# Use an official Java runtime as a parent image
FROM openjdk:11

# Set the working directory in the container
WORKDIR /workspace

# Install required tools
RUN apt-get update && apt-get install -y wget git

# Clone your fork of the repository
RUN git clone https://github.com/MichaelAkridge-NOAA/x3.git /workspace/x3

# Download required libraries
RUN wget -P /workspace/lib https://repo1.maven.org/maven2/commons-io/commons-io/2.11.0/commons-io-2.11.0.jar \
    && wget -P /workspace/lib https://repo1.maven.org/maven2/com/google/guava/guava/30.1.1-jre/guava-30.1.1-jre.jar

# Copy the scripts directory into the container
COPY images/gh_action_files/scripts /workspace/scripts

# Make the script executable
RUN chmod +x /workspace/scripts/convert_files.sh

# Compile the Java code from your repository
RUN javac -cp /workspace/x3/X3/src:/workspace/lib/commons-io-2.11.0.jar:/workspace/lib/guava-30.1.1-jre.jar /workspace/x3/X3/src/org/pamguard/x3/sud/ConvertSUDToWAV.java

# Default command
CMD ["java", "-cp", "/workspace/x3/X3/src:/workspace/lib/commons-io-2.11.0.jar:/workspace/lib/guava-30.1.1-jre.jar", "org.pamguard.x3.sud.ConvertSUDToWAV"]



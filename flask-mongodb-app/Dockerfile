# Use an official Python:3.9-slim image as a parent image
FROM python:3.9-slim

# Set the working directory in the container
WORKDIR /app

# Copy the requirements.txt file into the container at /app
COPY requirements.txt .

# Install the python dependencies specified in requirements.txt
RUN pip install --no-cache-dir -r requirements.txt

# Copy the current directory contents (application code) into the container at /app
COPY . .

# Expose port 5000 for the Flask application
EXPOSE 5000

# Set the environment variable for MongoDB URI (to be overridden in Kubernetes)
ENV MONGODB_URI="mongodb://admin:sapana@mongo-service:27017/"

# Define environment variable for Flask
ENV FLASK_APP=app.py
ENV FLASK_ENV=development

# Run the app when the container launches
CMD ["flask", "run", "--host=0.0.0.0"]












FROM python:3.12.2-slim-bullseye

# Set working directory
WORKDIR /usr/src/djangobnb_backend

# Correct ENV syntax (no spaces around `=`)
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Install netcat for database check
RUN apt-get update && apt-get install -y netcat

# Upgrade pip
RUN pip install --upgrade pip

# Copy only requirements first to leverage Docker cache
COPY djangobnb_backend/requirements.txt .

# Install Python dependencies
RUN pip install -r requirements.txt

# Copy entrypoint script and make it executable
COPY djangobnb_backend/entrypoint.sh .
RUN sed -i 's/\r$//g' entrypoint.sh && chmod +x entrypoint.sh

# Copy the rest of the codebase
COPY . .

# Use the entrypoint script
ENTRYPOINT ["/usr/src/djangobnb_backend/entrypoint.sh"]

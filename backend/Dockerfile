# Use official Python image
FROM python:3.10-slim

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Set working directory
WORKDIR /app

# Copy requirements first for caching
COPY requirements.txt .

# Install dependencies
RUN pip install --upgrade pip \
    && pip install --no-cache-dir -r requirements.txt

# Copy the backend code
COPY . .

# Expose Django default port
EXPOSE 8000

# Default command to run Django server
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]

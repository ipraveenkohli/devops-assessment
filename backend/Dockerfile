FROM python:3.11-slim AS builder

WORKDIR /app

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .
RUN pip install --upgrade pip \
    && pip install --prefix=/install -r requirements.txt


# ---------- Runtime stage ----------
FROM python:3.11-slim

# Create non-root user
RUN useradd -m django

WORKDIR /app

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Copy installed dependencies
COPY --from=builder /install /usr/local

# Copy project files
COPY . .

# Change ownership
RUN chown -R django:django /app

USER django

EXPOSE 8000

CMD ["python", "manage.py", "runserver"]

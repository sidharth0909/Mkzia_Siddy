FROM python:3.12-slim

WORKDIR /app

# System dependencies (curl for healthcheck)
RUN apt-get update && \
    apt-get install -y --no-install-recommends curl libgomp1 && \
    rm -rf /var/lib/apt/lists/*

# Install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy FastAPI app
COPY app.py .

# Models folder (mounted by docker-compose)
RUN mkdir -p /app/models

EXPOSE 8000

# Healthcheck (Docker + Cloud compatible)
HEALTHCHECK --interval=30s --timeout=5s --retries=3 \
  CMD curl -f http://localhost:8000/health || exit 1

# Start FastAPI
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]

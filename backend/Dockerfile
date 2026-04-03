FROM python:3.12-slim

WORKDIR /app

# System dependencies
RUN apt-get update && apt-get install -y --no-install-recommends \
    gcc libpq-dev libffi-dev \
    && rm -rf /var/lib/apt/lists/*

# Install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt \
    && pip install --no-cache-dir gunicorn reportlab

# Copy source code
COPY . .

EXPOSE 8000

CMD ["sh", "-c", "gunicorn main:app \
 --worker-class uvicorn.workers.UvicornWorker \
 --workers 4 \
 --bind 0.0.0.0:$PORT \
 --timeout 120 \
 --access-logfile -"]
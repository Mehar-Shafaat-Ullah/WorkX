
FROM python:3.10-slim

# Prevent prompts during install
ENV PYTHONUNBUFFERED=1 \
    PYTHONDONTWRITEBYTECODE=1

WORKDIR /app

RUN apt-get update && apt-get install -y \
    build-essential \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
EXPOSE 8000
RUN python manage.py collectstatic --noinput
CMD ["gunicorn", "src.wsgi:application", "--bind", "0.0.0.0:8000"]


# Usa una imagen base de Python
FROM python:3.12-slim

WORKDIR /app
ENV PYTHONPATH=/app

# Instalar dependencias del sistema mínimas
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copiar el código del servicio
COPY auth_service/ .

EXPOSE 8000

# Render inyecta PORT. En local, sin esa variable, sigue en 8000.
CMD ["sh", "-c", "python app/init_db.py && uvicorn app.main:app --host 0.0.0.0 --port ${PORT:-8000}"]

# Python base image

FROM python:3.10
WORKDIR /app-back

COPY requeriments.txt .
RUN pip install --no-cache-dir -r requeriments.txt
COPY . .

EXPOSE 8000
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "core.wsgi:application"]

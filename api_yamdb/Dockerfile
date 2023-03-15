FROM python:3.7-slim

WORKDIR /app

COPY requirements.txt .

RUN pip install --upgrade pip && \
    pip install -r /app/requirements.txt

COPY ./ /app

CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
#["gunicorn", "api_yamdb.wsgi:application", "--bind", "0.0.0.0:8000"]

# Use an official Python image as the base
FROM python:3.12-slim AS base

# Set the working directory in the container
WORKDIR /app

RUN apt-get update -y && \
    apt-get install -y --no-install-recommends \
    curl \
    && rm -rf  /var/lib/apt/lists/*

RUN curl -sSl https://install.python-poetry.org | python3 -

ENV PATH="/root/.local/bin:$PATH"

# Copy the rest of the application files 
COPY . . 

RUN poetry install

RUN chmod +x ./prestart.sh

# Expose the port on which the app runs 
EXPOSE 8000 

# Start the FastAPI server 
CMD ["sh", "-c", "poetry run bash ./prestart.sh && poetry run uvicorn app.main:app --host 0.0.0.0 --port 8000 --reload"]
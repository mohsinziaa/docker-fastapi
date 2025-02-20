# FastAPI Mock Model Prediction API

This project implements an asynchronous FastAPI-based API for simulating model predictions. It uses Redis for storing prediction statuses and results. The application supports both synchronous and asynchronous prediction processing.

## Features

- **Asynchronous and Synchronous Prediction**: You can request predictions either synchronously or asynchronously.
- **Redis Integration**: The application stores prediction status and results in Redis.
- **UUID for Prediction ID**: Each prediction request generates a unique ID.
- **Mock Model Prediction**: The application simulates a model prediction by generating random results.

## Requirements

- Python 3.7+
- Redis (locally or through an environment variable)
- FastAPI
- Uvicorn
- Pydantic

### Install dependencies:

```bash
pip install fastapi uvicorn redis pydantic
```

## Setup

1. **Redis Configuration**:
   Make sure you have a running Redis instance. You can configure the host and port of Redis through environment variables:

   - `REDIS_HOST` (default: `localhost`)
   - `REDIS_PORT` (default: `6379`)

   You can set them directly in your environment or use a `.env` file.

2. **Run the Application**:
   To run the application, use Uvicorn:

   ```bash
   uvicorn main:app --reload
   ```

   The FastAPI app will be available at `http://127.0.0.1:8000`.

## API Endpoints

### 1. `GET /`
Returns a welcome message.

**Response**:
```json
{
  "message": "Welcome to the Mock Model API!"
}
```

### 2. `POST /predict`
Accepts a prediction request and processes it asynchronously or synchronously.

**Request**:
- **Body**: A JSON payload with the `input` field (string).
- **Header**: Optionally, specify `async_mode` as `true` for asynchronous processing (default is synchronous).

**Example Request**:
```json
{
  "input": "Some input data"
}
```

**Response**:
```json
{
  "message": "Request received. Processing asynchronously.",
  "prediction_id": "UUID"
}
```

### 3. `GET /predict/{prediction_id}`
Check the status of a prediction by its ID.

**Response**:
- **If prediction is still processing**:
```json
{
  "detail": "Prediction is still processing."
}
```
- **If prediction is completed**:
```json
{
  "prediction_id": "UUID",
  "status": "completed",
  "output": {
    "status": "completed",
    "input": "Some input data",
    "result": "Random result"
  }
}
```

### 4. `GET /favicon.ico`
Returns a simple message for requests to `/favicon.ico`.

**Response**:
```json
{
  "message": "No favicon"
}
```

## Background Processing

For asynchronous processing, the prediction is handled in the background using FastAPI's `BackgroundTasks` feature. The prediction status is stored in Redis with a `processing` status until completed, and the result is saved with a `completed` status.


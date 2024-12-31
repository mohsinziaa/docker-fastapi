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

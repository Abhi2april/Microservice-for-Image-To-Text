# Image-to-Text Microservice Documentation

## Overview
This microservice provides an API for extracting text from images using OCR (Optical Character Recognition). It utilizes `FastAPI` for handling HTTP requests and `pytesseract` for text extraction.

## Dependencies
- `FastAPI`
- `pytesseract`
- `Pillow`
- `Jinja2`
- `pydantic`

Ensure these dependencies are installed before running the service.

## Environment Variables
The service relies on a `.env` file for configuration:
- `app_auth_token`: Authentication token for API access.
- `debug`: Enables debugging mode.
- `echo_active`: Enables the echo endpoint.
- `app_auth_token_prod`: Production authentication token.
- `skip_auth`: Skips authentication when enabled.

## API Endpoints

### 1. Home View
**Endpoint:** `GET /`
- Renders an HTML response from `templates/home.html`.
- Requires a `Settings` dependency.

### 2. Image-to-Text Prediction
**Endpoint:** `POST /`
- **Headers:**
  - `Authorization: Bearer <token>` (Required for authentication)
- **Body:**
  - `file`: Image file to process.
- **Response:**
  - Extracted text from the image.

### 3. Image Echo (Debugging Feature)
**Endpoint:** `POST /img-echo/`
- Saves the uploaded image to the `uploads/` directory.
- Returns the saved file.
- **Conditions:**
  - Requires `echo_active` to be `True`.
- **Response:**
  - Saved image file.

## Authentication
The service requires a valid authentication token in the `Authorization` header. If authentication fails, a `401 Unauthorized` response is returned.

## Error Handling
- **400 Bad Request:** If the uploaded file is not a valid image.
- **401 Unauthorized:** If authentication fails.
- **400 Invalid Endpoint:** If accessing a disabled feature.

## Running the Service
Ensure `FastAPI` is installed and run:
```sh
uvicorn main:app --reload
```


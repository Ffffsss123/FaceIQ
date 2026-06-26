# FaceIQ

FaceIQ is a funny web app that "tests" IQ by matching uploaded faces against a reference face embedding. It is built as a joke experiment: upload a photo, let the browser detect faces, and get a playful IQ-style result based on face similarity.

This is not a real IQ test, biometric assessment, medical tool, or scientific measurement.

## How It Works

1. The user uploads an image in the browser.
2. `face-api.js` detects faces and extracts face descriptors.
3. The descriptors are sent to the Flask backend at `/predict`.
4. The backend compares each descriptor with `embedding_IQ140.npy`.
5. The app returns a similarity score, a joke IQ value, and a result label.

## Tech Stack

- Python 3.10
- Flask
- SciPy / NumPy
- face-api.js in the browser
- Gunicorn for deployment
- Docker support

## Project Structure

```text
.
|-- app.py                    # Flask app and /predict endpoint
|-- utils.py                  # Face descriptor similarity logic
|-- embedding_IQ140.npy       # Reference embedding used for comparison
|-- templates/index.html      # Upload page and browser-side face detection
|-- static/                   # Local static assets and model files
|-- requirements.txt          # Python dependencies
|-- Dockerfile                # Container build
|-- Procfile                  # Gunicorn process for platforms like Heroku
`-- runtime.txt               # Python runtime version
```

## Run Locally

Create and activate a virtual environment:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Start the app:

```bash
python app.py
```

Then open:

```text
http://127.0.0.1:5000
```

## Run With Gunicorn

```bash
gunicorn app:app
```

## Run With Docker

Build the image:

```bash
docker build -t faceiq .
```

Run the container:

```bash
docker run -p 3000:3000 -e PORT=3000 faceiq
```

Then open:

```text
http://127.0.0.1:3000
```

## Notes

- The app currently loads face-api.js models from jsDelivr CDN in `templates/index.html`.
- The result is intentionally humorous and should not be treated as a real evaluation.
- Clear, front-facing photos work best for face detection.

GOOGLE_CLOUD_PROJECT="$(gcloud config get-value project)"
GOOGLE_CLOUD_PROJECT_NUMBER="$(gcloud projects describe $(gcloud config get-value project) --format='value(projectNumber)')"
GOOGLE_CLOUD_LOCATION="us-central1"
GOOGLE_GENAI_USE_VERTEXAI=true
MODEL="gemini-2.5-flash"
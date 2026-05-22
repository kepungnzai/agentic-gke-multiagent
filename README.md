GOOGLE_CLOUD_PROJECT="$(gcloud config get-value project)"
--------------------------------------------
GOOGLE_CLOUD_PROJECT_NUMBER="$(gcloud projects describe $(gcloud config get-value project) --format='value(projectNumber)')"
--------------------------------------------
GOOGLE_CLOUD_LOCATION="us-central1"
--------------------------------------------
GOOGLE_GENAI_USE_VERTEXAI=true
--------------------------------------------
MODEL="gemini-2.5-flash"
--------------------------------------------
Create our gke cluster
--------------------------------------------
gcloud container clusters create-auto adk-cluster \
  --location=$GOOGLE_CLOUD_LOCATION \
  --project=$GOOGLE_CLOUD_PROJECT


Get access to the gke cluster
--------------------------------------------
gcloud container clusters get-credentials adk-cluster --location="us-central1"   --project="project-00e3e1b1-5433-464c-b5e"


Build our image
--------------------------------------------
gcloud builds submit \
  --tag $GOOGLE_CLOUD_LOCATION-docker.pkg.dev/$GOOGLE_CLOUD_PROJECT/adk-repo/adk-agent:latest \
  --project=$GOOGLE_CLOUD_PROJECT \
  .
--------------------------------------------
Creating service account 
kubectl create serviceaccount adk-agent-sa
--------------------------------------------
Deploy our image
kubectl apply -f deployment.yaml




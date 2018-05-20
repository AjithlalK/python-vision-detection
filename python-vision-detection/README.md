# Python  Vision Detection App for detecting Text/Face expression/Landmark using Google Cloud Vision API deployed in Google App Engine

This  application allows a user to  perform text detection, landmark detection, and face expression detection 
using Google Machine learning Vision API.

## It detects

	1. How likely it is that the person is happy from photo of a person's face
	2. Extracts text within an image
	3. Popular natural and man-made structures within an image

Python Flask web framework with  jinja2 HTML templates and google cloud data store(NoSQL document database) is used in this application.

## Setup

Create your App Engine application:

    gcloud app create

Set an environment variable for your project ID, replacing `[YOUR_PROJECT_ID]`
with your project ID:

    export PROJECT_ID=[YOUR_PROJECT_ID]

## Getting the sample code

Run the following command to clone the Github repository:

    git clone https://github.com/AjithlalK/python-vision-detection.git

Change directory to the sample code location:

    cd python-vision-detection/python-vision-detection

## Authentication

Enable the APIs:

    gcloud services enable vision.googleapis.com
    gcloud services enable storage-component.googleapis.com
    gcloud services enable datastore.googleapis.com

Create a Service Account to access the Google Cloud APIs when testing locally:

    gcloud iam service-accounts create hackathon \
    --display-name "Codelab Service Account"

Give your newly created Service Account appropriate permissions:

    gcloud projects add-iam-policy-binding ${PROJECT_ID} \
    --member serviceAccount:hackathon@${PROJECT_ID}.iam.gserviceaccount.com \
    --role roles/owner

After creating your Service Account, create a Service Account key:

    gcloud iam service-accounts keys create ~/key.json --iam-account \
    codelab@${PROJECT_ID}.iam.gserviceaccount.com

Set the `GOOGLE_APPLICATION_CREDENTIALS` environment variable to point to where
you just put your Service Account key:

    export GOOGLE_APPLICATION_CREDENTIALS="/home/${USER}/key.json"

## Running locally

Create a virtual environment and install dependencies:

    virtualenv -p python3 env
    source env/bin/activate
    pip install -r requirements.txt

Create a Cloud Storage bucket. It is recommended that you name it the same as
your project ID:

    gsutil mb gs://${PROJECT_ID}

Set the environment variable `CLOUD_STORAGE_BUCKET`:

    export CLOUD_STORAGE_BUCKET=${PROJECT_ID}

Start your application locally:

    python main.py

Visit `localhost:8080` to view your application running locally. Press `Control-C`
on your command line when you are finished.

When you are ready to leave your virtual environment:

    deactivate

## Deploying to App Engine

Open `app.yaml` and replace <your-cloud-storage-bucket> with the name of your
Cloud Storage bucket.

Deploy your application to App Engine using `gcloud`. Please note that this may
take several minutes.

    gcloud app deploy

Visit `https://[YOUR_PROJECT_ID].appspot.com` to view your deployed application.





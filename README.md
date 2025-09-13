# nextjs-docker-GCP-GITHUb
create and host a contionously deployed next.js web app using with docker and github on google cloud

npx create-next-app@latest

cd/“project”

code .

Create file> Dockerfile

cd /Dockerfile 

"FROM node:18-alpine

RUN apk add --no-cache python3 make g++

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build

CMD ["npm", "start"]"

cd .dockerignore

"Docker

.dockerignore

node_modules"


cd/“project”

docker build -t “project-name” .

docker run -dp 3000:3000 "Project"   > check local host 3000

…. with gcloud….

> create project
>enable cloud Rundock
> enable Artifact Registry API
>enable Cloud Build API


————gcloud  CLI——————

cd /“project”

gcloud projects list

gcloud config set project "project-id"

gcloud artifacts repositories create project-docker-repo \
  --repository-format=docker \
  --location=us-west2 \
  --description="project Docker repository"

gcloud artifacts repositories list --location=us-west2

gcloud builds submit --region=REGION \
  --tag REGION-docker.pkg.dev/PROJECT_ID/REPO_NAME/IMAGE_NAME:TAG

    """PROJECT_ID → your Google Cloud project ID (from gcloud config get-value project)
    REPO_NAME → the Artifact Registry repository you created (e.g. my-docker-repo)
    IMAGE_NAME → the name of the Docker image (usually your app name)
    TAG → version label for the image (v1, latest, etc.)"""

    
gcloud run deploy SERVICE_NAME \
--image REGION-docker.pkg.dev/PROJECT_ID/REPO_NAME/IMAGE_NAME:TAG \

>default service name
> enable any api left
>choose region
>allow unauthenticated invocations = y

——No git—- changes——

gcloud artifacts repositories create“project-name”-docker-repo --repository-format=docker --location=us-west2 --description="Docker repository”

gcloud builds submit --region=us-west2 --tag ’”image-link”’:tag”number”’

____WITH Git-repo_____

cd/“project”

Create file>  cloud build.yaml

steps:

#build container image

- name: 'gcr.io-builders/docker'

  args: ['build’,’-t’,’”image-link”’:tag”number”’, '.']

#push to artificats registry

- name: 'gcr.io/cloud-builders/docker'

  args: ['push', ’”image-link”’:tag”number”’]

#deploy to gcloud run

- name: 'gcr.io/google.com/cloudsdktool/cloud-sdk'

  entrypoint: gcloud

  args: ['run', 'deploy’,’”Cloud Run image-name”’ , '--image',’”image-link”’:tag”number”’ , '--region', 'us-west2']

Images: 

- '’”image-link”’:tag”number”’'

___redeployment___

gcloud services enable cloudbuild.googleapis.com run.googleapis.com artifactregistry.googleapis.com

>>>>>in google cloud
>>>> Connect git repo, set up continuous deployment>> git>>> docker file.docker.
>>> edit deployment>> config>> yaml cloud build
>>>>>>>> Git push




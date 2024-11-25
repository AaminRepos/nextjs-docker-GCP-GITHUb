# nextjs-docker-GCP-GITHUb
create and host a contionously deployed next.js web app using with docker and github on google cloud

npm create-next-app@letest

cd/“project”

code .

Create file> Dockerfile

cd /Dockerfile 

FROM node:18-alpine

WORKDIR /app

COPY . .

RUN npm install --omit=dev

RUN npm run build

CMD ["npm", "start"]

cd/“project”

touch .dockerignore

cd /.dockerignore

Docker
.dockerignore
node_modules

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

gcloud config set “project-name”    ie. main gcloug project name

gcloud artifacts repositories create “project-name”-docker-repo --repository-format=docker --location=us-west2 --description="Docker repository”

gcloud artifacts repositories list location=us-west2

gcloud builds submit --region=us-west2 --tag ’”image-link”’:tag”number”’. ie. :tag1
. 
gcloud run deploy --image='’”image-link”’:tag”number”’'

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

>>>>>in google cloud
>>>>set up continuous deployment>> git>>> docker file.docker.
>>>edit deployment>> config>> yaml cloud build
>>>>>>>>Git push




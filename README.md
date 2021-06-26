# Node.js - Demo Web Application

## STEP 01: Build, Verify, Tag, Push Docker Image

Move Into Project Directory

    cd ./nodejs-demoapp

Build Docker Image

    docker build -t nodejs-demo-app .

Test Docker Image Locally 

    docker run -it -p 3000:3000 nodejs-demo-app:latest 

Access Via Web Browser

    http://localhost:3000/

Tag Docker Image

    docker tag nodejs-demo-app:latest ${ACR_REGISTRY}/nodejs-demo-app:latest 

Ex: docker tag nodejs-demo-app:latest dimuit86/nodejs-demo-app:latest 

Push Docker Image Dockerhub

In this step you need to create your own dockerhub repository.

    docker login
    docker push ${ACR_REGISTRY}/nodejs-demo-app:latest 

Ex: docker push dimuit86/nodejs-demo-app:latest 





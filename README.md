 Detailed Explanation of Steps Followed

1.  Set up Node.js Application
I developed a simple Node.js web application using the Express framework. The app listens on port 3000 and responds with a confirmation message when accessed via the browser. The core functionality is defined in server.js, and dependencies are declared in package.json.

2.  Create Dockerfile and Containerize the App
To containerize the app, I wrote a Dockerfile that:

Uses the official node:18 image as the base
Sets the working directory
Copies package.json and installs dependencies
Copies the app code into the image
Exposes port 3000
Specifies npm start as the run command
I then built the Docker image locally using:

docker build -t s223541137/kubernetes-nodejs-app .
3. Push Image to Docker Hub
After logging into Docker Hub, I pushed the built image:

docker push s223541137/kubernetes-nodejs-app
This made the image available publicly for Kubernetes to pull during deployment.

4.  Write Kubernetes Deployment Manifest
I created a k8s-deployment.yaml file that defines a Deployment with:

2 replicas of the Node.js app container
A selector that matches the pod labels
The image pulled from Docker Hub
Port mapping (containerPort: 3000)
Applied it using:

kubectl apply -f k8s-deployment.yaml
5. Create Kubernetes Service
I created a k8s-service.yaml file to expose the app. Initially, it used:

type: LoadBalancer
But because Docker Desktop doesn’t support external LoadBalancer IPs on macOS, I switched to NodePort or used kubectl port-forward for local testing.

6. Port Forward to Access App
To access the app in my browser, I ran:

kubectl port-forward pod/<pod-name> 8080:3000
This exposed the app locally on:

http://localhost:8080
Accessing this link displayed the app's success message, confirming it was running inside the Kubernetes cluster.

7. Verify Deployment
I used kubectl to confirm that the application was correctly deployed:

kubectl get pods
kubectl get services
This confirmed that both pods were running and that the service was forwarding traffic as expected.

8. Push Project to GitHub
I initialized a Git repository and committed all files:

git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/s223541137/sit323-2025-prac6p.git
git push -u origin main

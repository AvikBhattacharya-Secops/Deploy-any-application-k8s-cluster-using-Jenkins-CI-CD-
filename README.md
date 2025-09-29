✅ Final Output (in Bullet Points)

🔁 Code Cloned from GitHub repository:

https://github.com/AvikBhattacharya-Secops/complete-project-all.git

🛠️ Docker Image Built using application code:

Built image: avikbhattacharya056/my-calculator-image:<BUILD_NUMBER>

🚀 Docker Image Pushed to DockerHub:

Repository: https://hub.docker.com/r/avikbhattacharya056/my-calculator-image

Tag: Based on Jenkins BUILD_NUMBER (e.g., 21, 22, etc.)

☸️ Kubernetes Deployment Applied:

kubectl apply -f k8s-deployment.yaml executed inside Jenkins

Deployed image with latest build number to K8s cluster

🌐 Application Deployed on Kubernetes Cluster:

Pods running your app image in the K8s worker node

Accessible via NodePort / LoadBalancer / Ingress (based on your YAML config)

✅ Successful Jenkins Pipeline Run:

Stages executed: Checkout → Build → Push → Deploy

Jenkins logs show successful completion and image push

📦 Artifacts:

Docker image on DockerHub

Running application in K8s cluster

Deployment YAML applied to cluster

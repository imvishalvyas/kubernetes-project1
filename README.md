# Kubernetes Project 

This project demonstrates a simple **3-tier application** (Database, Backend, Frontend) deployed on Kubernetes.  
It is designed for testing purposes.

## 📂 Project Structure
```
├── backend
│   └── Dockerfile
├── frontend
│   ├── Dockerfile
│   └── index.html
├── k8s
│   ├── backend-deployment.yaml
│   ├── backend-service.yaml
│   ├── frontend-deployment.yaml
│   ├── frontend-service.yaml
│   ├── namespace.yaml
│   ├── postgres-configmap.yaml
│   ├── postgres-deployment.yaml
│   ├── postgres-secret.yaml
│   ├── postgres-service.yaml
│   └── pvc.yaml
└── README.md
```

# 1. Kubernetes Manifests (in k8s/)

- backend-deployment.yaml
- backend-service.yaml
- frontend-deployment.yaml
- frontend-service.yaml
- namespace.yaml
- postgres-configmap.yaml
- postgres-deployment.yaml
- postgres-secret.yaml
- postgres-service.yaml
- pvc.yaml


# 2 Backend Dockerfile
You can find backend Dockerfile in `backend` directory. Build and push to the dockerhub.
```
docker build -t imvishalvyas/backend:latest ./backend
docker push imvishalvyas/backend:latest
```

# 3. Frontend Dockerfile
You can find the Dockerfile in `frontend` directory.
```
docker build -t imvishalvyas/frontend:latest ./frontend
docker push imvishalvyas/frontend:latest
```

# 4. Deployments
After pushing the docker image, Update the `backend-deployment.yaml` file in k8s directory and add the docekrfile.
```
docker push imvishalvyas/backend:latest
```

# 5. Create postgres user, DB and password.
Here i have created the postgress db, user and password base64 format. you can find the details in `k8s/postgres.secret.yaml`

```
  POSTGRES_DB: YXBwX2Ri # base64 encoded "app_db"
  POSTGRES_USER: YXBwX3VzZXI= # base64 encoded "app_user"
  POSTGRES_PASSWORD: YXBwX3Bhc3M= # base64 encoded "app_pass"
```

Command to create base64.
`echo -n 'app_db' | base64`
`echo -n 'app_user' | base64`
`echo -n 'app_pass' | base64`


# 6. Apply Kubernetes manifests.
Apply all the files from `k8s` directory.
```
kubectl apply -f k8s/
```

# 7. Verify resources.
```
kubectl get all -n dev
```
You should see:

- `postgres` pod, pvc, service

- `backend` pod, service

- `frontend` pod, service (NodePort)



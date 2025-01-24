
# MLflow Demo Project  

This project demonstrates an MLflow setup with two components:  
1. **Deployment Folder**: Contains a `Dockerfile` and `launch.sh` for deploying the MLflow server.  
2. **Experimentation Folder**: Contains a Jupyter Notebook to showcase experiments and MLflow tracking.

---

## Project Structure
```
mlflow-demo/
├── deployment/
│   ├── Dockerfile
│   ├── launch.sh
├── experimentation/
│   ├── mlflow_experiment_notebook.ipynb
├── README.md
```

---

## Instructions for Local Deployment  

### 1. Build the Docker Image  
Navigate to the `deployment/` folder and build the Docker image:  
```bash
docker build . -t mlflowserverlocal
```

### 2. Run the Docker Container  
Run the container locally with the following command:  
```bash
docker run \
-p 5000:5000 \
-v $(pwd)/:$(pwd)/ \
mlflowserverlocal
```

- **Port Mapping**: Maps the container's internal port 5000 to your local available machine's port 5000.  
- **Volume Mapping**: Mounts the current directory to the container, enabling file sharing.  

Once the container is running, you can access the MLflow UI at:  
[http://localhost:5000](http://localhost:5001)  

---

## Deploying on the Cloud  

To deploy this project on the cloud:  

### 1. Push the Docker Image to a Cloud Container Registry  
Tag your image with your registry URL and push it:  
```bash
docker tag mlflowserverlocal <your-cloud-registry>/mlflowserver
docker push <your-cloud-registry>/mlflowserver
```

### 2. Set Up Cloud Resources   
- **Cloud Storage**: For saving and accessing MLflow artifacts and models. Examples:
  - AWS S3
  - Google Cloud Storage
  - Azure Blob Storage  

- **Setting Up a Backend Store**: Create a database for the backstore URI needed by mlflow (You can create your DB on the same cloud provider that has been used for the storage)

### 3. Update Environment Variables  
Modify the environment variables in the application to point to your cloud resources:  
- `MLFLOW_TRACKING_URI`: URL of your deployed API or MLflow server.  
- `ARTIFACT_STORE`: Cloud storage path for artifacts.  

### 4. Run the Application on Cloud  
Deploy the containerized app to a cloud platform like AWS ECS, GCP Cloud Run, or Azure Container Instances.  

---

## Key Notes  

- If you want to know more about cloud deployment, check out 
[my articlee](https://medium.com/towards-data-science/model-management-with-mlflow-azure-and-docker-2920b51a5bdd) published on towardsdatascienc.

---

# Minio 
![Minio](https://img.shields.io/badge/-Minio-D24939?style=for-the-badge&logo=amazon%20s3&logoColor=white)

Deploying standalone [minio](https://github.com/minio/minio) - A High Performance, Kubernetes Native Object Storage 

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [Minio](#minio)
    - [What is Minio](#what-is-minio)
    - [Deploy Via Kustomize](#deploy-via-kustomize)
    - [Minio Deployment](#minio-deployment)
- [Minio mc](#minio-mc)
    - [What is minio mc](#what-is-minio-mc)
    - [Deploy Via Kustomize](#deploy-via-kustomize-1)
    - [minio-mc Deployment](#minio-mc-deployment)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

### What is Minio
- MinIO is a High Performance Object Storage
- It is API compatible with Amazon S3 cloud storage service

### Deploy Via Kustomize

```bash
kustomize build minio | kubectl apply -f -
```

### Minio Deployment 
- Current deployment is made just for testing minio, there's no persistent storage
- All resources are created in **minio** namespace
- NodePort service exposes minio UI via the address http://<host>:31001
- Default login credentials are `minioadmin:minioadmin` and can be set using the ENV variables **[MINIO_ROOT_USER](https://docs.min.io/minio/baremetal/reference/minio-server/minio-server.html#envvar.MINIO_ROOT_USER)** and **[MINIO_ROOT_PASSWORD](https://docs.min.io/minio/baremetal/reference/minio-server/minio-server.html#envvar.MINIO_ROOT_PASSWORD)**

---

# Minio mc 

### What is mc
- mc is short for [minio client](https://github.com/minio/mc), it will be used for executing commands on minio deployment

### Deploy Via Kustomize

```bash
kustomize build minio-mc | kubectl apply -f -
```

### minio-mc Deployment 
- Minio Host is configured through the environment variable `MC_HOST_minio` Which point to the minio deployment above
- To execute any command just exec into the pod and run the desired mc command 

```bash
# List buckets 
mc ls minio

# Create a bucket 
mc mb minio/my-bucket

# Copy a file to the bucket 
mc cp sample.txt minio/my-bucket
```
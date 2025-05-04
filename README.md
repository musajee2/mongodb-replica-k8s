# MongoDB Replica Set on Kubernetes

This project demonstrates how to deploy a **MongoDB Replica Set** using **Kubernetes**, ensuring high availability, redundancy, and automatic failover with self-healing pods.

---

## 📦 Features

- 🧩 MongoDB configured as a **3-node replica set** (1 Primary, 2 Secondaries)
- 🐳 Deployment using **StatefulSets**
- 🔁 Automatic pod recovery and rejoining after failure
- 📂 Persistent storage using `PersistentVolumeClaims`
- 🌐 Internal DNS-based pod discovery via **Headless Service**

---

## 🛠️ Project Files

| File | Description |
|------|-------------|
| `mongo-service.yaml`       | Headless Service for MongoDB internal networking |
| `mongo-statefulset.yaml`   | StatefulSet defining 3 MongoDB pods with persistent volumes |
| `mongo-init.yaml` *(optional)* | Init container for one-time replica set initiation |
| `journal-report.md` or `.pdf` | Academic journal describing the task implementation |
| `screenshots/`             | Folder containing setup and verification screenshots |

---

## 🚀 Deployment Instructions

Run the following commands from the project root directory:

```bash
# Step 1: Create the Kubernetes namespace
kubectl create namespace mongodb-replica

# Step 2: Apply the headless service
kubectl apply -f mongo-service.yaml -n mongodb-replica

# Step 3: Deploy the StatefulSet
kubectl apply -f mongo-statefulset.yaml -n mongodb-replica

# (Optional) Step 4: Initiate replica set only once (if not yet initialized)
kubectl apply -f mongo-init.yaml -n mongodb-replica
To monitor pods:
kubectl get pods -n mongodb-replica -w
```

## ✅ Verification & Testing
To test if the replica set is working correctly:

kubectl exec -it mongo-0 -n mongodb-replica -- mongo

Inside the shell:
rs.status()

To simulate a failure and observe self-healing:
kubectl delete pod mongo-1 -n mongodb-replica

# Watch it restart and rejoin
kubectl get pods -n mongodb-replica -w

## 📚 Learnings & Observations
This project showcases Kubernetes' robust orchestration for stateful workloads like MongoDB:

StatefulSets manage stable identities and persistent volumes across restarts.

Replica set maintains high availability even if a node fails.

rs.status() confirms real-time role status (PRIMARY/SECONDARY).

Kubernetes simplifies recovery and auto-healing of critical services.

## 👨‍💻 Author
Muhammad Musa
📧 Email: musajee2002@gmail.com
🔗 GitHub: @musajee2

📝 License
This project is open-source and free to use for academic purposes.

---

Let me know if you want a `.md` file exported directly, or if you want to automatically include your screenshots with Markdown image links.







# EA3 Virtualización - Despliegue de WordPress y MySQL en Kubernetes

## 📁 Estructura del repositorio
```bashg
.
├── 📄manual-pv.yaml               # PersistentVolumes para MySQL y WordPress
├── 📄mysql-deployment.yaml        # Service y Deployment de MySQL
├── 📄mysql-pvc.yaml               # PersistentVolumeClaim de MySQL
├── 📄wordpress-deployment.yaml    # Service (NodePort) y Deployment de WordPress
├── 📄wordpress-pvc.yaml           # PersistentVolumeClaim de WordPress
└── 📄namespaces.yaml              # Namespaces "mysql" y "wordpress"
```
---

## Pasos para desplegar

### 1. Crear los namespaces
```bash
kubectl apply -f namespaces.yaml
```
---
### 2. Crear los volúmenes persistentes (hostPath)
```bash
kubectl apply -f manual-pv.yaml
```
### 3. Desplegar la base de datos MySQL
```bash
kubectl apply -f mysql-pvc.yaml
kubectl apply -f mysql-deployment.yaml
```
### 4. Verifica que esté funcionando:

```bash
kubectl get pods -n mysql
kubectl get svc -n mysql
```
### 5. Desplegar WordPress

```bash
kubectl apply -f wordpress-pvc.yaml
kubectl apply -f wordpress-deployment.yaml
```
### 6. Verifica que esté funcionando:
```bash
kubectl get pods -n wordpress
kubectl get svc -n wordpress
```
---
## Prueba la aplicación de WordPress

Usa la IP del nodo + el puerto `30080` para acceder desde tu navegador:

```
http://<NODE-IP>:30080
```
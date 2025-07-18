# ✅ Sesión 2: Pods y Contenedores en Kubernetes  
**Duración:** 30 minutos  
**Objetivo:** Comprender qué es un Pod, cómo se relaciona con los contenedores, y cómo gestionarlos con comandos y archivos YAML.

---

## 📌 1. ¿Qué es un Pod?

Un **Pod** es la **unidad más pequeña de ejecución en Kubernetes**.

🔹 Puede contener **uno o más contenedores** (generalmente uno).  
🔹 Comparte:
- Red
- Sistema de archivos (si se desea)
- Ciclo de vida

> ⚠️ Los contenedores dentro de un mismo Pod pueden comunicarse por `localhost`.

---

## 📌 2. ¿Por qué no usar contenedores directamente?

Kubernetes **no gestiona contenedores directamente**, sino **Pods**:
- Aísla la lógica de red y almacenamiento del contenedor
- Permite **ejecutar múltiples contenedores acoplados** (como sidecars)
- Define el entorno con mayor precisión (probes, recursos, volúmenes)

---

## 📌 3. Crear un Pod simple con kubectl

Creamos un Pod ejecutando un contenedor NGINX:

```bash

# Se crea un pod con una imagen nginx.
kubectl run mi-nginx --image=nginx --port=80

# Lista los pods del cluster.
kubectl get pods

# Devuelve información más detallada del pod.
kubectl describe pod mi-nginx

# Devuelve los logs del pod.
kubectl logs mi-nginx

# Accedemos a la consola del pod
kubectl exec -it mi-nginx -- /bin/bash

# Eliminamos un pod
kubectl delete pod mi-nginx

```

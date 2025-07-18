# KUBERNETES DESDE CERO

Esto es un experimento, enviandole propmts a Chatgpt para que de un pensum que seguir e ir realizando.

En princpio, el temario de este curso es el siguiente:

## 📚 Curso de Kubernetes con Minikube y Podman  
**Duración:** 10 sesiones (30 minutos cada una)  
**Nivel:** Principiante → Intermedio  
**Requisitos previos:**  
- Conocimientos básicos de Linux y CLI  
- Instalación de **Minikube**, **kubectl**, **Podman**  

---

## ✅ Plan de Aprendizaje

---

### **Sesión 1: Introducción a Kubernetes**
**Objetivo:** Entender qué es Kubernetes, por qué se usa y su arquitectura básica.  

#### **Temas:**
- ¿Qué es Kubernetes? ¿Por qué usarlo?
- Componentes principales:  
  - **Master Node:** API Server, Scheduler, Controller Manager, etcd  
  - **Worker Node:** Kubelet, Kube-proxy, contenedores  
- Objetos básicos: Pods, Deployments, Services  
- ¿Qué es Minikube y por qué lo usamos?  

#### **Práctica:**
```bash
# Iniciar clúster con Podman como driver
minikube start --driver=podman

# Ver información del clúster
kubectl cluster-info
kubectl get nodes


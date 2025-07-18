# Manifests

Los manifiestos son ficheros en formato yml que ayudan a pasar de una forma más descriptiva el estado y las caracteristicas que se esperan de un pod.

Hay muchos tipos de manifests ya que se separan por su kind, cada kind se encarga de realizar tareas especificas dentro del cluster como pudieran ser la configuración de redes, ejecuciones de los pods, agregar datos de segmentación, labels, entre muchas cotras cosas que se iran definiendo a lo largo del curso.

## Campos obligatorios

Los manifiestos tienen muchos campos que se pueden consultar en la documentación, pero cualquier manifest debe tener como mínimo los siguientes campos:

- apiVersion: Define la versión del motor de kubernetes. Útil para garantizar la retrocompatibilidad.
- kind: Define el tipo de manifest, puede ser pod, namespace, network, etc... Hay muchos tipos diferentes de kinds.
- metadata: Campos que se utilizan para identificar, segmentar, ordenar etc,,, en kubernets.

- (opcional) spec: si bien este campo no es obligatorio, lo más común es que este presente en los manifest. Este campo define las especificaciones del pod, como los contenedores a ejecutar por ejemplo.


En el siguiente ejemplo, se puede ver un manifest que levanta un pod con nginx.
``` yml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-manual
spec:
  containers:
    - name: nginx
      image: nginx
      ports:
        - containerPort: 80
```

## Convensiones de nombrado de ficheros y estructura de proyectos.

Por convensión se sigue el siguiente nombrado de los ficheros:

- <nombre_pod>-pod.yaml
- <nombre_deployment>-deployment.yaml
- <nombre_service>-service.yaml
- .... etc....

Por convensión, se define el kind en el nombre del fichero seguido del nombre del mismo.

## Estructura de archivos

La estructura más común den un proyecto kubernetes es la siguiente.

k8s/
├── nginx-pod.yaml
├── nginx-service.yaml
├── nginx-deployment.yaml
└── config/
    └── nginx-configmap.yaml


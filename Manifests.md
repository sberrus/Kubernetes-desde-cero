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

## Probes

Las probes son caracteristicas de kubernetes que ayudan a controlar y monitorear el estado del contenedor y además, permiten reaccionar a ciertos eventos como fallos, startup, reinicios etc...

### Tipos de probes

Los probes más conocidos y que suelen estar presentes en la mayoría de containers son liveness y readines.

A continuación se definen estos probes y los más utilizados:

- Liveness: Este se usa para saber si el contenedor esta vivo. Si falla, se reinicia el contenedor.
- Readiness: Este define si elcontenedor esta listo para recibir tráfico. En el caso de que no lo este, es excluido del servicio.
- Startup: Este controla si el contenedor termina de arrancar correctamente. Es comúnmente usado para los pods que suelen tener arranques lentos, poder saber y reaccionar para cuando este haya terminado.

### Métodos de los probes

Las probes dependiendo del estado del ciclo de vida del contenedor, van a realizar ciertas tareas; estas tareas llamadas métodos son los que nosotros definimos para decirle al probe "prueba esto, si no hay problemas puedes marcar el probe como ok".

Los métodos en cuestión son:

httpGet: Define la configuración para hacer una llamada httpGet al contenedor para evaluar si esta ok.
tcpSocket: Intenta abrir una conexión tcp para saber si el pod en cuestión puede recibir tráfico.
exec: Ejecuta un comando o un script dentro del contenedor.

Cada tipo de probe tiene sus métodos los cuales son los que se ejecutan para evaluar el estado del contenedor.

### Buenas prácticas

- Por lo menos ten configuradas las probes de readiness y liveness para tener controlado que el contenedor esta funcionando y listo para manejar tráfico.
- Usar startup solo cuando se sabe que el pod suele ser lento a la hora de arrancar.
- Usa el método correcto tomando en cuenta que es lo que se espera del contenedor. Si es una API, lo suyo es tener un httpGet a un endpoint para saber si esta up, o un tcpSocket de manera que sepamos que se puede servir contenido etc...
- Evitar que los probes sean demasiado frecuentes, dependiendo del caso vas a querer que las comprobaciones se hagan más rápido o lentas dependiendo del contenedor.
- En el caso de los httpGet, no usar / sino a nivel de la app, definir endpoints que sean más explicitos para saber el estado de salud del contendor como /healt o /ready
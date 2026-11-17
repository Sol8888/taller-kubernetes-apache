# Apache en Kubernetes con Deployment y ReplicaSet

## Objetivo
Desplegar Apache HTTP Server en Minikube y demostrar el uso de
Deployment, ReplicaSet, escalado y reemplazo automatico de Pods.

## Usos de Apache
- Alojar sitios web y paginas estaticas.
- Servir aplicaciones web.
- Actuar como proxy inverso mediante configuracion adicional.

## Componentes
- Deployment apache: administra el despliegue de la aplicacion.
- ReplicaSet: mantiene la cantidad deseada de Pods.
- Service NodePort: permite acceder a Apache desde fuera del cluster.
- ConfigMap apache-pagina: contiene la pagina HTML personalizada.

## Archivos
- apache.yml: Deployment inicial con 2 replicas y Service NodePort.
- index.html: pagina personalizada.
- pagina-configmap.yml: ConfigMap que contiene el HTML.
- pagina-patch.yml: conecta el ConfigMap con los contenedores de Apache.

## Requisitos
Docker Desktop, Minikube y PowerShell.

## Despliegue
Ejecutar desde la carpeta del repositorio:

```powershell
$mk = "C:\Program Files\Kubernetes\Minikube\minikube.exe"
& $mk start --driver=docker
& $mk kubectl -- apply -f apache.yml
& $mk kubectl -- apply -f pagina-configmap.yml
& $mk kubectl -- patch deployment apache --type=strategic --patch-file pagina-patch.yml
& $mk kubectl -- rollout status deployment/apache --timeout=180s
& $mk service apache

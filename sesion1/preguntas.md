## **Ejercicios:**

1. Tienes que lograr desplegar una aplicación en tu Docker Hub, crea el Dockerfile de tu aplicación y luego asignale el tag ckad, posteriormente salva tu imagen en un archivo backup.tar y finalmente subela a tu repositorio en Docker Hub.
   
2. Crea un namespace con el nombre dev-environment, despliega un pod usando la imagen gcr.io/google-samples/hello-app:1.0, genera el yaml de manera imperativa, si quieres validar el despliegue usa Port-Forward en el puerto 8080 del Pod.
    * https://kubernetes.io/docs/tasks/access-application-cluster/port-forward-access-application-cluster/
  
3. Genera el yaml para desplegar el Pod que subiste a tu Docker Hub.
   
4. Despliega un pod que use la imagen nginx:alp1ne, corrige el nombre de ser necesario para desplegar correctamente el pod.
   
5. Lista todos los pods del namespace kube-system y ubicalos en el archivo pods.txt

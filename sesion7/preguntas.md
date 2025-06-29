## **Ejercicios:**

1. Crea un Pod llamado cache-app que use la imagen nginx.
   * Usa un volumen emptyDir para montar un directorio /cache donde se almacenen archivos temporales.
   * Borra el Pod y verifica que los datos se hayan perdido.
2. Despliega un Pod llamado logger con la imagen httpd.
   * Usa un volumen hostPath para montar /var/log/httpd desde el nodo en /usr/local/apache2/logs dentro del contenedor.
   * Accede al nodo y confirma que los logs se están escribiendo en /var/log/httpd.
3. Despliega un PVC que tenga las siguientes características.
   * 2Gi de almacenamiento.
   * Despliega un pod que se conecte al PVC y escribe un archivo dentro.
   * Elimina el pod y crea un nuevo pod verificando que el PVC persistio los datos.
4. Despliega un pod llamado multi-volume-pod que monte un volumen emptyDir en /data/temp y un hostPath en /data/logs.
5. Despliega un StatefulSet con 3 réplicas de redis usando un volume para /data.
   * Verifica que cada Pod (redis-0, redis-1, redis-2) tenga su propio PVC.
   * Escala a 5 replicas y verifica que los pods se nombren secuencialmente.
   * El puerto de redis es el 6379
   * Puedes usar el cliente de redis para hacer pruebas: kubectl run redis-client --rm -it --image=redis -- bash
   * Comando: redis-cli -h redis-0.redis y ejecutar ping 
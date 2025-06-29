## **Ejercicios:**

1. En el control plane de tu cluster, crea un static pod llamado static-server que ejecute la imagen nginx:latest. El pod debe ser gestionado desde el archivo static-server.yaml.
2. Crea un Deployment llamado rolling-deployment con la imagen httpd y 3 réplicas.
   * Realiza un Rolling Update para actualizar la imagen a httpd:2.4.63.
   * Supervisa el estado de tu Update.
   * Actualiza la imagen a una versión incorrecta, ejemplo httpd:unknow.
   * Usa el comando adecuado para realizar un rollback hacía la versión anterior.
3. Crea un Pod llamado multi-ckad con dos contenedores:
   * Contenedor web con la imagen httpd:latest.
   * Contenedor batch con la imagen busybox, ejecutando el comando sh -c "echo Segundo container' && sleep 3600".
4. Crea un ConfigMap llamado app-config basado en un archivo de configuración, luego crea un Pod llamado cfgmap-pod que monte los valores del ConfigMap como variable de entorno.
5. Crea un Secret llamado db-secret, codifica sus valores en Base64 y crea un Pod llamado secret-pod que use este Secret para configurar sus variables de entorno.
6. Crea un Secret llamado init-secret con la clave mensaje cuyo valor sea Examen CKAD, luego crea un Pod llamado init-secret-pod con las siguientes características:
   * Un Init Container que use la imagen busybox y escriba el valor del Secret en un archivo /tmp/secret.
   * Un contenedor principal que use la imagen nginx y lea el archivo /tmp/secret al iniciarse.
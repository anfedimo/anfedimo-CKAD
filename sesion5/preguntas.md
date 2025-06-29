## **Ejercicios:**

1. Crea un Service de tipo ClusterIP llamado web-clusterip que exponga un Pod web-pod con la imagen nginx.
   * El Service debe estar en el puerto 8080 y mapearse al puerto 80 del contenedor.
   * Realiza pruebas de conexión con curl desde otro pod usando el service anterior.
   * Puedes usar otro pod con la imagen de nginx que ya tiene curl instalado.
2. Despliega un Deployment nodeport-app con 3 réplicas de la imagen httpd.
   * Crea un Service NodePort que lo exponga en el puerto 30080.
   * Verifica la conexión exponiendo con minikube.
3. Despliega el archivo pregunta3.yaml que contiene un Service y Deployment.
   * Valida la conexión desde otro pod y de ser posible identifica los errores en el manifiesto.
4. Despliega dos aplicaciones (nginx y httpd) con sus respectivos services.Crea un ingress que tenga configurado el service nginx accesible en /nginx y httpd accesible en /apache.
5. Despliega el archivo pregunta5.yaml y valida que estén funcionando de manera correcta.

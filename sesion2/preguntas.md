## **Ejercicios:**

1. Despliega un replicaset de nombre server-rs en el nuevo namespace que use la imagen de nginx y tenga 5 replicas.

2. Dentro del namespace dev-environment, migra el pod que has creado previamente de tu aplicación y conviertelo en un deployment que tenga 3 replicas. Comprueba que se mantenga la cantidad de replicas al eliminar una.
   
3. Despliega una aplicación que use la imagen httpd y asegura que tenga desplegado un pod en cada nodo del cluster. Usa el objeto correspondiente para esta tarea.
   
4. Crea un job que cumpla con ejecutarse 5 veces y tenga la posibilidad de tener 2 ejecuciones en paralelo.
   
5. Programa una tarea que se ejecute cada 2 minutos, configura un timeout de 5 segundos al job y que se mantengan solamente los últimos 2 jobs successfull. 
   * Puedes usar el siguiente comando en tu imagen busybox “date; echo Hello mitocode!!”


## **Ejercicios:**

1. Crea un pod de nombre ckad-server que use la imagen nginx:alpine, configura los siguientes labels app=server / env=certi y luego comparte los comandos que usas para listar los pods por label.
2. En un nodo configura un Taint con el siguiente valor key=ckad:NoSchedule y crea un pod que use la imagen redis y logra que se despliegue dentro de este nodo.
3. Configura un nodo con un label tecnologia=kubernetes y crea un deployment de nombre deploy-mitocode con 3 replicas y que use la imagen httpd, el deployment debe tener un node affinity para ser desplegado en el nodo con la etiqueta anterior.
4. Despliega un pod mitocode-resource que use la imagen que tienes en tu docker hub y configura los valores cpu request: 100m, cpu limit: 500m, memory request: 128Mi y memory limit: 512Mi.
5. En el namespace dev-environment configura un limit range por contenedor que tenga limite maximo de 1 CPU y 1Gi y despliega un pod que infriga estas reglas.
6. Crea un Resource Quota que permita solo desplegar 3 pods en el namespace dev-environment y despliega un deployment con 5 replicas.



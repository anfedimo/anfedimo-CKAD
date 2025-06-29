## **Ejercicios:**

1. Crea dos versiones de una aplicación (blue y green) con Deployments separados, configura un Service para enrutar el tráfico solo a la versión blue y luego actualiza el Service para enrutar el tráfico a la versión green.
2. Crea un Deployment con una versión estable. Crea un segundo Deployment con la versión canary pero con solo el 10% de las réplicas. Incrementa gradualmente el tráfico de 50% y luego a 80%.
3. Crea y despliega un helm chart que exponga una aplicación que use la imagen kennethreitz/httpbin.
   * El puerto de exposición del contenedor es 80.
   * La aplicación debe tener un deployment, un service y un ingress.
   * Asignale un values.yaml por default.
4. Modifica algún valor de tu archivo values.yaml y realiza un upgrade de tu chart usando helm upgrade.
5. Crea y despliega una aplicación que use la imagen kennethreitz/httpbin usando kustomize.
   * La aplicación debe tener un deployment y un service.
   * Debes tener 2 ambientes, staging y producción.
   * Usa al menos un transformation.
6. Crea un Custom Resource Definition con las siguientes características:
   * Name: mitocode.cka.example.com, Group : cka.example.com, 
   * Schema: <pais: string><nombre: string>, Scope: Namespaced, Kind: Mitocode
7. Genera un manifiesto YAML para desplegar un recurso del CRD.

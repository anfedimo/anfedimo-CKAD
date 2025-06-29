## **Ejercicios:**

1. Crear un ClusterRole que permita a un ServiceAccount eliminar Pods en un Namespace específico.
   * Crea un ClusterRole llamado pod-deleter que permita eliminar pods.
   * Crea un ServiceAccount llamado pod-admin en el namespace critical-apps.
   * Asigna el ClusterRole solo al namespace critical-apps mediante un RoleBinding.
   * Prueba el acceso usando kubectl auth can-i delete pods --as=system:serviceaccount:critical-apps:pod-admin -n critical-apps.
2. Crea un ServiceAccount llamado reader-ckad y asignale un Role que permita listar y leer logs de los pods. Despliega un Pod que use reader-ckad e intenta ejecutar kubectl get pods..
3. Crea un Pod que deba cumplir las siguientes reglas: 
   * No corra como root (runAsNonRoot: true).
   * Tener un usuario específico (runAsUser: 2000). 
   * No permitir escalamiento de privilegios (allowPrivilegeEscalation: false).
   * Usar un sistema de archivos de solo lectura (readOnlyRootFilesystem: true).
4. Crea una NetworkPolicy que permita tráfico al pod db-app solo desde el namespace trusted.
5. Define una NetworkPolicy que solo permita tráfico de Pods con app=frontend hacia app=backend.
6. Define una NetworkPolicy que permita que solo un Pod acceda a 8.8.8.8 (Google DNS).
 

# 🧠 Laboratorio de Kubernetes por Sesiones

Este repositorio contiene una colección completa de manifiestos YAML agrupados por sesiones temáticas. Cada uno permite ejercitar buenas prácticas de despliegue, seguridad, red, almacenamiento y operación de clústeres Kubernetes modernos.

Incluye ejemplos aplicados, recomendaciones basadas en OWASP Kubernetes Top 10 y una arquitectura recomendada para entornos reales.

---

## 🗂️ Estructura por Sesiones

```bash
.
├── sesion1/     -> Introducción y fundamentos
├── sesion2/     -> Controladores de Pods
├── sesion3/     -> Scheduling y recursos
├── sesion4/     -> ConfigMaps y Secrets
├── sesion5/     -> Servicios, redes e Ingress
├── sesion6/     -> Helm, Kustomize y despliegue continuo
├── sesion7/     -> Almacenamiento persistente
├── sesion8/     -> Seguridad, RBAC y políticas de red
├── sesion9/     -> Observabilidad y autocuración
```

---

## 🏗️ Arquitectura de Buenas Prácticas

```plaintext
[Dev/CI] --> [Repo Git] --(CI/CD)--> [Cluster K8s]
                                          |
                +-------------------------+------------------------+
                |                         |                        |
          [Namespace App]          [Namespace Logging]      [Namespace Ingress]
                |                         |                        |
        +-------+--------+           +----+-----+           +------+------+
        | Deployment     |           | DaemonSet|           | Ingress     |
        | + PVC + Config |           | + Loki   |           | Controller  |
        +----------------+           +----------+           +-------------+
```

- Despliegues declarativos, almacenamiento persistente con PVC, configuración externa con ConfigMaps y Secrets.
- Seguridad con RBAC, SecurityContext, NetworkPolicy.
- Logging centralizado y probes para autocuración.

---

## 📘 Detalle por manifiesto

### 🔹 `deployment.yaml`
Crea un Deployment que asegura que un número de réplicas esté corriendo constantemente. Permite actualizaciones declarativas (rolling update) y rollbacks automáticos.

**Ejemplo**: Una app web de frontend con 3 réplicas y actualización continua.

---

### 🔹 `replicaset.yaml`
Controlador que asegura un número específico de pods corriendo. No gestiona actualizaciones como un Deployment.

**Uso práctico**: Para cargas estables sin necesidad de actualizar.

---

### 🔹 `job.yaml`
Ejecuta tareas finitas como scripts de backup o migración de base de datos. Corre una vez y finaliza.

**Ejemplo**: Limpieza de archivos temporales cada noche.

---

### 🔹 `cronjob.yaml`
Ejecuta un Job en un horario definido como cron. Muy útil para tareas repetitivas.

**Ejemplo**: Un cronjob que cada día a medianoche hace respaldo de una base de datos.

---

### 🔹 `daemonset.yaml`
Asegura que un pod se ejecute en todos los nodos del clúster. Ideal para monitoreo, logs o agentes de seguridad.

**Ejemplo**: Agente de Promtail en cada nodo para enviar logs a Loki.

---

### 🔹 `stateful.yaml`
Despliega pods con identidad y almacenamiento persistente garantizados. Requiere PVCs y se usa con bases de datos como PostgreSQL o MongoDB.

**Ejemplo**: Un clúster de Cassandra o Redis con volúmenes persistentes.

---

### 🔹 `service.yaml`, `nodePort.yaml`, `ingress.yaml`
- `service.yaml`: expone una app internamente.
- `nodePort.yaml`: abre un puerto en el nodo para acceso externo.
- `ingress.yaml`: gestiona rutas HTTP usando host/path.

**Ejemplo**: Servicio frontend expuesto en `example.com/app`.

---

### 🔹 `env.yaml`, `static.yaml`, `multi-pod.yaml`, `init-pod.yaml`
Manejan configuración externa:
- `env.yaml`: define variables de entorno.
- `static.yaml`: configura un ConfigMap plano.
- `multi-pod.yaml`: múltiples pods montan el mismo ConfigMap.
- `init-pod.yaml`: preconfigura datos antes de que inicie el contenedor principal.

**Ejemplo**: Montar archivo `.env` con parámetros de entorno.

---

### 🔹 `pv.yaml`, `pvc.yaml`, `hostpath.yaml`, `emptydir.yaml`
Volúmenes:
- `pv.yaml`: volumen persistente definido por el admin.
- `pvc.yaml`: reclamo de volumen (PVC).
- `hostpath.yaml`: usa una ruta local del nodo.
- `emptydir.yaml`: volumen efímero que se borra al reiniciar el pod.

**Ejemplo**: Guardar archivos subidos por usuarios en un PVC montado.

---

### 🔹 `resource.yaml`, `crd.yaml`, `kustomization.yaml`
- `crd.yaml`: define un recurso personalizado.
- `resource.yaml`: crea una instancia del CRD.
- `kustomization.yaml`: personaliza despliegues usando overlays.

**Ejemplo**: Definir y gestionar `BackupPolicy` como CRD.

---

### 🔹 `quota.yaml`, `request.yaml`, `limitrange.yaml`
Gestionan uso de recursos:
- `quota.yaml`: impone límites por namespace.
- `request.yaml`: peticiones mínimas por contenedor.
- `limitrange.yaml`: define límites por defecto.

**Ejemplo**: Evitar que un pod consuma toda la RAM del nodo.

---

### 🔹 `nodeaffinity.yaml`, `nodename.yaml`, `tolerations.yaml`
Control del scheduling:
- `nodeaffinity.yaml`: asigna pods por etiquetas de nodo.
- `nodename.yaml`: fuerza ubicación por nombre de nodo.
- `tolerations.yaml`: permite correr en nodos con taints.

**Ejemplo**: Agendar pods GPU en nodos con etiquetas `accelerator=gpu`.

---

### 🔹 `securityContext.yaml`, `deploySecurity.yaml`
Define cómo se ejecuta un contenedor:
- `runAsUser`, `readOnlyRootFilesystem`, `capabilities`.

**Ejemplo**: Ejecutar como usuario no root con acceso limitado al sistema de archivos.

---

### 🔹 `networkPolicy.yaml`
Restringe el tráfico entre pods, namespaces y servicios.

**Ejemplo**: Permitir acceso solo desde el pod `frontend` al `backend`.

---

### 🔹 `role.yaml`, `roleBinding.yaml`, `clusterRole.yaml`, `clusterRoleBinding.yaml`
Permisos:
- `role*`: control de acceso a nivel de namespace.
- `clusterRole*`: acceso global.

**Ejemplo**: Solo el pod `job-runner` puede crear deployments.

---

### 🔹 `log.yaml`, `trouble.yaml`, `self-healing.yaml`
- `log.yaml`: revisa salida de logs.
- `trouble.yaml`: simula fallos.
- `self-healing.yaml`: incluye probes (`liveness` y `readiness`).

**Ejemplo**: Detectar cuelgue de aplicación y reiniciar el pod automáticamente.

---

## 🛡️ OWASP K8s Top 10 y Manifiestos Relacionados

| Riesgo OWASP                           | Manifiestos Clave |
|----------------------------------------|--------------------|
| 1. RBAC excesivo                       | `role*`, `clusterRole*` |
| 2. Contenedores privilegiados          | `securityContext.yaml` |
| 3. Servicios expuestos                 | `nodePort.yaml`, `ingress.yaml` |
| 4. Tráfico sin restricción             | `networkPolicy.yaml` |
| 5. Configuración insegura de pods      | `deploySecurity.yaml`, `init-pod.yaml` |
| 6. Sin límites de recursos             | `quota.yaml`, `limitrange.yaml` |
| 7. Falta de probes                     | `self-healing.yaml` |
| 8. Falta de registros                  | `log.yaml` |
| 9. Namespaces mal usados               | Usar `namespace` por sesión |
| 10. Despliegues no auditados           | `blue-green.yaml`, `canary.yaml`, `bitnami.yaml` |

---

## ✅ Requisitos y herramientas

- Kubernetes v1.25+
- `kubectl`, `helm`, `kustomize`
- Opcional: Minikube o kind para pruebas locales

---

## 👨‍💻 Autor
Fernando Díaz Moreno ([GitHub @anfedimo](https://github.com/anfedimo))

[![GitHub followers](https://img.shields.io/github/followers/anfedimo?style=social)](https://github.com/anfedimo)


---

## 🔁 Integraciones Avanzadas: ArgoCD, Istio y Kyverno

Estas herramientas fortalecen la seguridad, automatización y observabilidad en clústeres productivos de Kubernetes.

---

### 🔄 ArgoCD (GitOps para Kubernetes)

**Propósito:** Automatiza el despliegue y sincronización del estado deseado (manifiestos) desde Git.

**Aplicación:**
- Se recomienda usar ArgoCD para gestionar todos los manifiestos de este repositorio.
- Puedes organizar cada sesión como un `Application` de ArgoCD apuntando a una ruta del repositorio.

**Ejemplo de Application:**
```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: app-sesion2
spec:
  destination:
    server: https://kubernetes.default.svc
    namespace: sesion2
  source:
    repoURL: https://github.com/usuario/k8s-lab
    targetRevision: HEAD
    path: sesion2
  project: default
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
```

---

### 🌐 Istio (malla de servicios)

**Propósito:** Provee control de tráfico, seguridad mTLS, observabilidad y políticas en la capa de red.

**Aplicación:**
- Aplica a manifiestos que involucran servicios, Ingress, pruebas de red y despliegues (`sesion5`, `sesion6`, `sesion9`).
- Permite tráfico seguro entre microservicios mediante `VirtualService`, `Gateway`, `DestinationRule`.

**Ejemplo de VirtualService para Ingress:**
```yaml
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  name: frontend-vs
spec:
  hosts:
    - "example.com"
  gateways:
    - istio-ingressgateway
  http:
    - match:
        - uri:
            prefix: /app
      route:
        - destination:
            host: frontend
            port:
              number: 80
```

---

### 🛡️ Kyverno (políticas declarativas de seguridad)

**Propósito:** Define políticas de validación, mutación y generación en clústeres K8s.

**Aplicación:**
- Recomendado para validar que los manifiestos cumplan con OWASP Top 10.
- Puede proteger recursos como `Deployment`, `Pod`, `Ingress`, `Service`.

**Ejemplo de política: forzar `runAsNonRoot`:**
```yaml
apiVersion: kyverno.io/v1
kind: ClusterPolicy
metadata:
  name: require-non-root
spec:
  validationFailureAction: enforce
  rules:
    - name: validate-run-as-non-root
      match:
        resources:
          kinds:
            - Pod
      validate:
        message: "runAsNonRoot debe estar habilitado."
        pattern:
          spec:
            securityContext:
              runAsNonRoot: true
```

---

## 🔐 Mejores Prácticas Combinadas

| Herramienta | Beneficio Clave | Manifiestos Asociados |
|-------------|------------------|------------------------|
| ArgoCD      | GitOps, automatización continua | Todos los `deployment.yaml`, `kustomization.yaml` |
| Istio       | Seguridad, tráfico controlado, observabilidad | `ingress.yaml`, `service.yaml`, `deployment.yaml` |
| Kyverno     | Seguridad declarativa y validación | `securityContext.yaml`, `deploySecurity.yaml`, `networkPolicy.yaml`, `quota.yaml` |

---

## 📌 Recomendación de Flujo DevSecOps

```text
Git Push --> ArgoCD (sync) --> Kyverno (política segura) --> Istio (exposición y control)
```

Esto garantiza:
- Automatización de despliegue confiable
- Validación antes de aplicar
- Seguridad en la comunicación entre servicios


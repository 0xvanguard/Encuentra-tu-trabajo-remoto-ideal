# VanguardOps — IT Support Automation Platform

> Centraliza tickets de soporte, ejecuta runbooks y elimina trabajo repetitivo de mesa de ayuda. Pensado para equipos de IT pequeños que no quieren contratar un L1 por cada cliente nuevo.

![status](https://img.shields.io/badge/status-active-brightgreen)
![python](https://img.shields.io/badge/python-3.10%2B-blue)
![docker](https://img.shields.io/badge/docker-ready-blue)
![license](https://img.shields.io/badge/license-MIT-lightgrey)

![VanguardOps — overview](docs/img/overview.png)
*<sub>Reemplazar con captura del dashboard / flujo de tickets / ejecución de runbook.</sub>*

---

## El problema

Una mesa de ayuda IT típica gasta entre el 40% y el 60% de su tiempo en tareas repetitivas: reseteo de contraseñas, alta y baja de usuarios, recolección de logs, diagnóstico básico de red, instalación de software estándar. Cada una de esas tareas individualmente cuesta poco; sumadas cuestan mucho. Y se hacen mal cuando el técnico está ocupado o cansado.

## La solución

VanguardOps centraliza tickets en una capa común y ejecuta **runbooks** automáticos para los casos repetitivos. Los runbooks son piezas de Python contenedorizadas que:

- Diagnostican el problema en base a la información del ticket.
- Ejecutan los pasos de remediación seguros, con logging detallado.
- Devuelven el resultado al ticket original y notifican al técnico.
- Escalan al humano cuando el ticket cae fuera de patrón conocido.

El técnico humano deja de gastar tiempo en tareas mecánicas y se enfoca en los casos que realmente requieren criterio.

## Para quién

- **Equipos de IT internos** de empresas medianas que ya tienen sistema de tickets (Zendesk, Freshdesk, Jira Service Management) y necesitan reducir backlog.
- **MSPs** (Managed Service Providers) que atienden múltiples clientes y necesitan estandarizar respuestas.
- **Startups en crecimiento** que aún no tienen una mesa de ayuda madura y quieren saltar directamente a operaciones automatizadas.

## Qué resuelve hoy

- **Ingesta de tickets** desde APIs de los principales proveedores (Zendesk, Freshdesk, Jira SM) o vía webhook genérico.
- **Clasificación automática** del ticket según patrón (regex y reglas declarativas en YAML; opcional clasificador con LLM).
- **Catálogo de runbooks** versionado: reseteo de contraseña, alta/baja de usuarios, recolección de logs, diagnóstico de red básico, instalación de software empaquetado.
- **Ejecución segura** dentro de contenedores con permisos mínimos por runbook.
- **Auditoría completa**: cada runbook deja traza de qué hizo, cuándo y por orden de quién.
- **API REST** para integraciones externas y panel web ligero para operadores.

## Stack técnico

- **Python 3.10+** con FastAPI.
- **Docker / docker-compose** para empaquetado de la plataforma y aislamiento de runbooks.
- **PostgreSQL** para persistencia de tickets, ejecuciones y catálogo.
- **Redis** para cola de trabajos.
- **Celery** o **RQ** para ejecución asíncrona.
- **YAML** para definición declarativa de runbooks.
- **Pydantic** para validación de inputs.
- **OpenAPI / Swagger** auto-generado.

## Cómo correrlo en 60 segundos

```bash
git clone https://github.com/0xvanguard/VanguardOps.git
cd VanguardOps
cp .env.example .env
docker compose up -d
```

Abre `http://localhost:8000/docs` para la API y `http://localhost:8000/ui` para el panel.

Crear un ticket de prueba:

```bash
curl -X POST http://localhost:8000/tickets \
  -H "Content-Type: application/json" \
  -d '{"title":"Necesito reset de password","body":"Olvidé mi contraseña del correo corporativo","reporter":"empleado@empresa.com"}'
```

VanguardOps detecta el patrón "reset de password" y dispara el runbook correspondiente.

## Arquitectura (alto nivel)

```
┌─────────────────┐    ┌────────────────────┐    ┌──────────────────┐
│  Ticket sources │───▶│  Ingest API        │───▶│  Classifier      │
│  (Zendesk, Jira,│    │  (FastAPI)         │    │  (rules + LLM)   │
│  webhook genér.)│    │                    │    │                  │
└─────────────────┘    └────────────────────┘    └──────────────────┘
                                                         │
                                                         ▼
                       ┌────────────────────┐    ┌──────────────────┐
                       │  Audit log + DB    │◀───│  Runbook engine  │
                       │  (PostgreSQL)      │    │  (Celery + Docker│
                       └────────────────────┘    │   sandboxing)    │
                                                 └──────────────────┘
                                                         │
                                                         ▼
                                                 ┌──────────────────┐
                                                 │  Notify back to  │
                                                 │  ticket source   │
                                                 └──────────────────┘
```

## Catálogo inicial de runbooks

| ID | Qué hace | Riesgo |
|---|---|---|
| `password-reset-ad` | Reset de password en Active Directory + envío al usuario por canal seguro. | Bajo |
| `user-onboard` | Crea usuario en Google Workspace + asigna grupos según rol. | Medio |
| `user-offboard` | Suspende usuario + revoca tokens + transfiere drive a manager. | Medio-alto |
| `net-diag-basic` | Ping/traceroute/dns/MTU desde host de prueba. | Bajo |
| `log-bundle` | Recolecta logs estandarizados de un host y los empaqueta. | Bajo |
| `software-install` | Instala paquete versionado desde catálogo aprobado. | Medio |

## Roadmap corto

- [ ] Soporte para más proveedores de tickets (ServiceNow, HubSpot Service).
- [ ] Editor visual de runbooks (drag & drop).
- [ ] Métricas Prometheus (tiempo medio de resolución, % de tickets autoresueltos).
- [ ] Modo *dry-run* para validar runbooks antes de ejecutarlos contra producción.
- [ ] Plantillas de runbooks aportadas por la comunidad.

## Limitaciones conocidas

- El clasificador opcional con LLM requiere API key externa; el modo solo-reglas funciona offline.
- Los runbooks corren con los permisos que el operador le otorgue al contenedor; mal configurado puede dar más acceso del necesario. Las plantillas vienen con permisos mínimos por defecto.
- Aún no hay panel multi-tenant; cada despliegue atiende a un solo equipo.

## Licencia

MIT. Si lo usas en producción, abre un issue contando cómo te fue: alimenta el roadmap.

## Contacto

Construido por [Tu Nombre](https://github.com/0xvanguard) — abierto a contratos para personalizar runbooks, integrar VanguardOps con stacks específicos o hacer onboarding a equipos.

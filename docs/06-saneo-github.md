# Doc 06 — Saneo del GitHub: dejar de autosabotearte

Hoy tu perfil tiene **~19 repos públicos**. Solo 4 tienen contenido sustancial. El resto está actuando como ruido y, peor, como **señal negativa** para reclutadores técnicos.

> Cuando un reclutador entra a tu perfil, no examina los 19 repos. Abre los **3 primeros que ve**. Si los abre y encuentran cascarones vacíos, cierra el tab y pasa al siguiente candidato. No importa que más abajo tengas oro.

## Inventario actual y decisión por repo

> **Convención:**
> - **MANTENER PÚBLICO** = repo con contenido vendible. Pulir README.
> - **PRIVAR** = pasarlo a privado. Sigue existiendo para ti, deja de mostrar al exterior.
> - **ARCHIVAR** = mantener público pero marcado como archivado. Útil cuando hay aprendizaje genuino y quieres mostrar exploración, pero no quieres que parezca actividad reciente.
> - **ELIMINAR** = solo cuando el repo es claramente experimental sin valor histórico.

| # | Repo | Tamaño | Decisión | Justificación |
|---|---|---|---|---|
| 1 | **Security-Checklist-Ecommerce** | 48 MB | MANTENER PÚBLICO + reemplazar README con la versión premium | Pieza vendible B2B. Es el activo #1. |
| 2 | **VanguardOps** | 31 MB | MANTENER PÚBLICO + README premium | Activo #2, demuestra automation real. |
| 3 | **InfraSight** | 17 MB | MANTENER PÚBLICO + README premium pendiente | Activo #3, infra/monitoring. Hacer README v2 después de los 3 prioritarios. |
| 4 | **Attack-Surface-Validation-Lab.** | 5 MB | MANTENER PÚBLICO + README premium | Activo #4, security recon. **Cuidado:** el nombre tiene un punto al final, considera renombrarlo a `Attack-Surface-Validation-Lab` (sin punto). |
| 5 | **SentinelOps** | 65 KB | PRIVAR | Solapa con Sentinel-Lab y ThreatWatch. Decide cuál es la versión definitiva y privatiza las otras dos. |
| 6 | **OSINTX-Intelligence-Console** | 3 KB | PRIVAR (por ahora) | Solo cascarón. Reactivar como público cuando tenga 3+ features funcionales. |
| 7 | **Sentinel-Lab** | 2 KB | PRIVAR | Cascarón duplicado de SentinelOps. |
| 8 | **ThreatWatch-Detection-Core** | 2 KB | PRIVAR | Cascarón. |
| 9 | **Baseline-Hardening-Manager** | 2 KB | PRIVAR | Cascarón duplicado conceptual de Security-Checklist. |
| 10 | **Analizador-Estático-de-APKs-para-Cazar-Malware** | 1 KB | PRIVAR | Vacío. |
| 11 | **Analizador-de-Red-Local-y-Escáner-de-Puertos-Móvil** | 64 KB | PRIVAR (por ahora) | Kotlin/móvil. Si lo retomas, lo despublicas. |
| 12 | **Arquitectura-del-Protocolo-Iron-Bind-** | 24 KB | PRIVAR | Solo arquitectura sin código real. Mantener privado mientras maduras. |
| 13 | **Crear-y-Vender-plantillas-de-Configuracion-Segura** | 102 KB | PRIVAR | Nombre poco profesional ("Crear y Vender"). Si quieres mantener el contenido, créalo de cero como repo nuevo con nombre técnico (`secure-config-templates`). |
| 14 | **Script-de-Hardening-Bastionado-para-Servidores-Linux** | 31 KB | RENOMBRAR Y PULIR o PRIVAR | Nombre largo, en español, con palabras pomposas. Si tiene contenido útil, renombrar a `linux-hardening-baseline` y poner README serio. Si no, privar. |
| 15 | **Laboratorio-Vulnerable-Automatizado** | 24 KB | PRIVAR | Cascarón. |
| 16 | **-Offensive-Defense-Pipeline-Public** | 10 KB | RENOMBRAR Y PULIR o PRIVAR | El nombre empieza con guion (mal). Renombrar a `offensive-defense-pipeline`. Verificar contenido real antes de decidir. |
| 17 | **ESTRATEGIA-BILLONARIOS** | 268 KB | PRIVAR | Nombre poco profesional, no aporta a perfil tech. |
| 18 | **ROADMAP-CREA-TU-AGENTE-DESDE-EL-DIA-1** | 60 KB | PRIVAR | Nombre clickbait, no aporta. |
| 19 | **Encuentra-tu-trabajo-remoto-ideal** | (este repo) | MANTENER PÚBLICO si quieres usarlo como blog técnico, o PRIVAR | Útil para ti, mixto para perfil profesional. |

## Resultado deseado del saneo

Después del saneo, tu perfil público debería mostrar **5–7 repos máximo**, todos con README serio y código real. Eso da una señal completamente distinta:

```
Antes:  19 repos · 4 con contenido · 15 cascarones        →  "este perfil es ruido"
Después: 5–7 repos · todos con README serio + screenshots →  "este perfil sabe lo que hace"
```

## Pasos exactos para ejecutarlo (orden importa)

### Paso 1 — Privar/archivar lo que sobra (15 minutos)

Para cada repo en la lista marcado como PRIVAR:

1. Abre `https://github.com/0xvanguard/<repo>/settings`.
2. Scroll abajo hasta `Danger Zone`.
3. Click en `Change repository visibility` → `Private` → confirmar.

> Privar conserva el código, no destruye nada. Si en 6 meses descubres que un repo privado tenía oro, lo vuelves a público.

### Paso 2 — Renombrar lo que se queda con nombre malo (10 minutos)

Para repos con nombres en español pomposos o con caracteres raros:

1. `https://github.com/0xvanguard/<repo>/settings`.
2. Sección `Repository name` → renombrar.
3. Si el repo es de los públicos que se quedan (Attack-Surface-Validation-Lab.), renombra al nombre limpio.

Renombrados sugeridos:
- `Attack-Surface-Validation-Lab.` → `attack-surface-validation-lab`
- `Security-Checklist-Ecommerce` → `security-checklist-ecommerce`
- `VanguardOps` → `vanguardops` (o mantenerlo CamelCase, ambos son aceptables; CamelCase queda mejor visualmente)

> Convención: **kebab-case en minúsculas** es estándar moderno en GitHub. Pero CamelCase para nombres de producto queda más profesional. Elige uno y aplícalo a todos los repos públicos.

### Paso 3 — Pulir README de los 4 repos sustanciales (1–2 días, no 1 hora)

Usa los archivos en `docs/03-readmes-premium/`:

1. **Security-Checklist-Ecommerce** → reemplazar README con `Security-Checklist-Ecommerce.md`.
2. **VanguardOps** → reemplazar README con `VanguardOps.md`.
3. **Attack-Surface-Validation-Lab** → reemplazar README con `Attack-Surface-Validation-Lab.md`.
4. **InfraSight** → escribir README v2 siguiendo la misma estructura. Pendiente, hacerlo después de los 3 prioritarios.

Para cada uno:
- Crear capturas reales en `docs/img/` del repo destino.
- Verificar que los comandos `pip install` / `docker build` realmente funcionan.
- Eliminar cualquier referencia mock que no esté implementada (mejor un README más corto y honesto que uno largo con features que no existen).

### Paso 4 — Crear archivo de perfil `0xvanguard/0xvanguard` (15 minutos)

GitHub permite tener un repo con tu username como nombre, cuyo README aparece en la portada de tu perfil. Es la primera cosa que ve cualquier reclutador.

Crear repo `0xvanguard/0xvanguard` con README como este:

```markdown
# Hola — soy [Tu Nombre] 👋

**Python Automation Engineer · Backend & Cloud Security**
Bogotá, Colombia · Remoto LATAM/USA

Construyo backends, integraciones e internal tools en Python con
seguridad por defecto, contenedorizadas con Docker y desplegadas
sobre GCP/Firebase.

## Proyectos destacados

- 🛡️ **[Security Checklist E-commerce](https://github.com/0xvanguard/Security-Checklist-Ecommerce)** — Auditor CLI + web de tiendas online con reporte PDF.
- ⚙️ **[VanguardOps](https://github.com/0xvanguard/VanguardOps)** — Plataforma de automatización de soporte IT.
- 📡 **[InfraSight](https://github.com/0xvanguard/InfraSight)** — Monitorización remota de endpoints distribuidos.
- 🔍 **[Attack Surface Validation Lab](https://github.com/0xvanguard/Attack-Surface-Validation-Lab.)** — Recon y validación de superficie de ataque.

## Stack

`Python` · `Docker` · `Firebase` · `GCP` · `FastAPI` · `Linux` · `Bash` · `PostgreSQL` · `Redis`
Aplicado a: backend services · automation · CI/CD · cloud security · hardening · attack surface management

## Disponibilidad

Empleo remoto full-time, contratos freelance B2B, consultoría puntual.
Cobro internacional vía Wise / Payoneer / Deel.

📩 [tu_email]   ·   💼 [linkedin.com/in/tu-handle](https://linkedin.com/in/tu-handle)
```

> Esto es lo más alto de ROI por minuto invertido. Reclutadores entran a tu perfil y leen esto antes que cualquier repo.

### Paso 5 — Pin de los repos correctos (2 minutos)

En la portada de tu perfil GitHub, click en `Customize your pins` y elige exactamente estos 4–6, en este orden:

1. Security-Checklist-Ecommerce
2. VanguardOps
3. Attack-Surface-Validation-Lab
4. InfraSight
5. (opcional) Otro repo público que sobreviva al saneo

> Sin estos pins, GitHub te muestra los más recientes, que pueden ser justo los cascarones que privaste. Pin manual obligatorio.

## Consideraciones importantes

### Sobre eliminar vs privar

**No elimines nada.** Privar es reversible y barato; eliminar pierde historial, issues, stars y commits. Si un día retomas el repo, prefieres tener el historial.

### Sobre commits diarios y "green squares"

Algunos consultores recomiendan commitear todos los días para tener el calendario verde. Mi recomendación contraria: **calidad sobre cantidad**. Un calendario con 3 commits/semana en repos serios pesa más que 30 commits/semana en cascarones. Reclutadores técnicos huelen el "commit-spam".

### Sobre repos en español vs inglés

Los repos públicos serios deberían tener:
- **Nombre en inglés** (kebab-case o CamelCase, no mezclar).
- **Descripción en inglés** corta.
- **README** en inglés como principal, español como sección secundaria si quieres alcanzar mercado dual.
- **Comentarios de código** en inglés.

Excepciones: proyectos que son *deliberadamente* localizados (ej: `infrasight` que tienes en español puede mantenerse así si su mercado es 100% LATAM). Pero los 3 del top 3 deberían ser bilingües o solo inglés.

### Sobre las stars y forks (0 en todo)

No te angusties por eso ahora. Stars son consecuencia de visibilidad sostenida (publicar en LinkedIn, en Reddit, en Hacker News, en Discord). Va a pasar cuando:
- Tu LinkedIn empiece a publicar contenido sobre estos repos.
- Tus README estén pulidos.
- Hagas 1–2 publicaciones tipo "construí X, lo abrí en GitHub" en comunidades relevantes.

Mientras tanto, **stars 0 es invisible, no es negativo**. Lo realmente negativo son los cascarones públicos.

## Checklist de saneo en 1 día (3–4 horas reales)

- [ ] Privar los 12 repos de la lista marcados PRIVAR.
- [ ] Renombrar los 4 repos públicos al esquema definitivo.
- [ ] Crear el repo de perfil `0xvanguard/0xvanguard` con README de portada.
- [ ] Pinar los 4–6 repos finales en orden.
- [ ] Reemplazar el README de los 3 repos prioritarios con la versión premium de `docs/03-readmes-premium/`.
- [ ] Subir capturas a `docs/img/` de cada repo prioritario (mínimo 1 por repo).
- [ ] Verificar que `pip install` / `docker build` reales funcionan en los 3 repos prioritarios.
- [ ] Verificar que `LICENSE` y `.gitignore` están presentes en los 4 públicos.
- [ ] Refrescar la bio del propio perfil GitHub (la línea corta arriba, no el README).

Tiempo estimado: 3–4 horas concentradas. Después de esto, tu perfil pasa de **"junior con ruido"** a **"junior con foco"**.

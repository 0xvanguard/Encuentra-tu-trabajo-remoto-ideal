# Doc 03 — READMEs premium para los 3 repos clave

Tres repos elegidos como punta de lanza del portafolio. Cada uno tiene un README listo para reemplazar el actual. El objetivo es que un reclutador en 30 segundos entienda **qué hace, para quién, con qué stack y por qué importa**.

## Repos cubiertos

1. **Security-Checklist-Ecommerce.md** — auditor CLI + web de tiendas online con reporte PDF. Vendible B2B.
2. **VanguardOps.md** — plataforma de automatización de soporte IT (lo que llamabas "TicketBot").
3. **Attack-Surface-Validation-Lab.md** — laboratorio de reconocimiento y validación de superficie de ataque.

## Por qué estos tres y no otros

| Repo | Por qué entra | Para qué tipo de vacante vende |
|---|---|---|
| Security-Checklist-Ecommerce | El más sustancial (48 MB) y el más fácil de vender a un fundador o CTO de e-commerce. | AppSec junior, DevSecOps, freelance B2B, automation con foco security. |
| VanguardOps | Es tu pieza de "automation real" más cargada (31 MB). Demuestra que sabes diseñar plataforma, no solo scripts. | Backend Python, Automation Engineer, Internal Tools Engineer. |
| Attack-Surface-Validation-Lab. | Habla en idioma de pentesters y AppSec. Te diferencia del backend dev plano. | DevSecOps junior, AppSec, Cloud Security, contractor de pentesting. |

## Reemplazado: OSINTX queda fuera del top 3

Originalmente habíamos hablado de incluir OSINTX-Intelligence-Console como "Shadowbroker / OSINT Case Tracker", pero hoy pesa 3 KB y no tiene contenido sustancial. Mientras esté así, restará credibilidad al perfil. Queda en el GitHub como exploración, no como pieza vendible. Cuando le agregues 3–5 features funcionales y un demo, revisamos su promoción al top 3.

## Estructura común que sigue cada README

1. **Título + tagline en una línea** (lo que se ve cuando alguien lo abre).
2. **Badges**: lenguaje, licencia, estado (en producción / en construcción / lab interno).
3. **Demo / screenshots** arriba, antes del texto. Lo visual gana 10x al texto.
4. **¿Qué problema resuelve?** Una línea concreta.
5. **¿Para quién?** Audiencia clara.
6. **Stack técnico**.
7. **Cómo correrlo en 60 segundos** (pasos copy-paste, sin trampas).
8. **Arquitectura** simple (diagrama o lista).
9. **Roadmap** corto y honesto (2–4 ítems próximos).
10. **Contribuir / contacto**.

## Cómo aplicar estos READMEs

1. Abre el repo correspondiente en GitHub.
2. Reemplaza el README actual con el archivo de esta carpeta (mismo nombre).
3. Crea las imágenes que se referencian en `/docs/img/` o `/screenshots/` del propio repo. Si todavía no tienes capturas reales:
   - Tomas una captura de la CLI corriendo (terminal con asciinema o un PNG simple).
   - Tomas una captura de la salida (PDF de reporte, dashboard, JSON de respuesta).
   - Las subes al repo y referencias con `![alt](docs/img/nombre.png)`.
4. Commitea con mensaje claro: `docs: replace README with portfolio-grade version`.

> **Importante:** los enlaces a screenshots dentro de los READMEs apuntan a archivos que aún no existen en cada repo. Tienes que crearlos en el repo destino o ajustar las rutas. No subas un README que dispare imágenes rotas.

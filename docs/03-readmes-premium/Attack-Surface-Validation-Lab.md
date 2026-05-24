# Attack Surface Validation Lab

> Entorno de reconocimiento y validación de seguridad que evalúa la superficie de ataque de un activo antes de un despliegue. Un paso entre el OSINT crudo y el pentest formal.

![status](https://img.shields.io/badge/status-active-brightgreen)
![python](https://img.shields.io/badge/python-3.10%2B-blue)
![license](https://img.shields.io/badge/license-MIT-lightgrey)
![lab](https://img.shields.io/badge/use-authorized%20targets%20only-orange)

![Attack Surface Validation Lab — workflow](docs/img/workflow.png)
*<sub>Reemplazar con captura de un escaneo terminado / consola con hallazgos / dashboard.</sub>*

---

## El problema

Antes de poner un servicio en producción —una API nueva, un dominio recién registrado, una infraestructura que se va a exponer a internet— alguien debería preguntarse: *¿qué le ve un atacante desde afuera?* En la mayoría de equipos esa pregunta se responde con un escaneo manual apurado o no se responde.

## La solución

Un laboratorio que automatiza el reconocimiento externo de un objetivo autorizado y consolida los hallazgos en un reporte navegable. Sirve como:

- **Validación previa a despliegue**: confirmar que no hay subdominios olvidados, puertos abiertos no esperados o configuraciones defectuosas antes de pasar a producción.
- **Punto de partida para un pentest**: el pentester arranca con la superficie ya enumerada en lugar de gastar el primer día en recon.
- **Verificación periódica**: detectar derivas en la superficie de ataque (un dominio nuevo que apareció, un servicio que cambió de versión).

## Para quién

- **AppSec / DevSecOps engineers** que quieren un baseline reproducible para sus servicios.
- **Pentesters junior y consultores freelance** que necesitan automatizar la fase de recon.
- **Equipos de plataforma** que quieren validar despliegues en CI/CD antes de exponerlos.

## Qué hace hoy

- Enumeración de subdominios combinando fuentes pasivas (CRT.sh, Subfinder-style sources) y activas (DNS bruteforce con wordlists).
- Resolución y deduplicación de hosts vivos.
- Escaneo de puertos top-N con detección de servicios.
- Fingerprinting de tecnologías (versiones de servidores web, frameworks expuestos en headers o cuerpos de respuesta).
- Detección de cabeceras de seguridad faltantes en endpoints HTTP/HTTPS.
- Identificación de assets no documentados que deberían levantar sospecha (entornos *staging*, *dev*, *test* expuestos sin querer).
- Consolidación de hallazgos en JSON, Markdown y HTML navegable.

## Stack técnico

- **Python 3.10+** como orquestador.
- **Docker** para encapsular cada herramienta y ejecutar en sandbox.
- **DNSPython, httpx, requests** para resolución y sondeo.
- Integraciones con binarios estándar: `nmap`, `subfinder` (opcional), `httpx-toolkit` (opcional).
- **Jinja2** para templates de reporte.
- **SQLite** para persistencia local del histórico.

## Cómo correrlo en 60 segundos

```bash
git clone https://github.com/0xvanguard/Attack-Surface-Validation-Lab..git
cd Attack-Surface-Validation-Lab.
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python -m asv_lab scan --target ejemplo-autorizado.com --output ./out
```

Con Docker:

```bash
docker build -t asv-lab .
docker run --rm -v "$PWD/out:/out" asv-lab \
  scan --target ejemplo-autorizado.com --output /out
```

Abrir `out/report.html` en el navegador.

## Arquitectura (alto nivel)

```
┌─────────────────┐    ┌────────────────────┐    ┌──────────────────┐
│   Target input  │───▶│  Recon orchestrator│───▶│  Findings store  │
│   (CLI / file)  │    │  (Python)          │    │  (SQLite + JSON) │
└─────────────────┘    └────────────────────┘    └──────────────────┘
                              │   │   │                  │
                              ▼   ▼   ▼                  ▼
                       ┌────────┐┌────────┐┌────────┐┌──────────────┐
                       │Subdom. ││Port    ││Tech    ││ Reporter     │
                       │enum    ││scanner ││fingerp.││ (Markdown +  │
                       │module  ││module  ││module  ││  HTML)       │
                       └────────┘└────────┘└────────┘└──────────────┘
```

## Política de uso responsable

Esta herramienta se ejecuta solo contra **objetivos autorizados** (los que tú o tu organización poseen, o los que un cliente te ha autorizado por escrito a evaluar). Escanear infraestructura ajena sin permiso constituye delito en la mayoría de jurisdicciones.

El repo no incluye payloads ofensivos ni explotación. Es estrictamente reconocimiento y validación.

## Roadmap corto

- [ ] Diff entre escaneos consecutivos (qué cambió en la superficie de ataque desde la última corrida).
- [ ] Enriquecimiento con información de CVEs para tecnologías detectadas.
- [ ] Integración con CI/CD para bloquear despliegues si aparecen hallazgos críticos.
- [ ] Soporte de objetivos múltiples desde archivo de scope.
- [ ] Plantilla de reporte adicional optimizada para entrega a cliente (PDF con resumen ejecutivo).

## Limitaciones conocidas

- No hace explotación ni autenticación. Si necesitas validar lo que hay detrás del login, esto no es suficiente.
- El bruteforce DNS depende de la wordlist; con wordlists pequeñas puede dejar subdominios sin descubrir.
- El fingerprinting es conservador: prefiere "no detectado" a falsos positivos.

## Licencia

MIT. Úsalo, fórkalo, mejóralo. Si lo usas profesionalmente y te resulta útil, una mención al repo me ayuda a sostener el proyecto.

## Contacto

Construido por [Tu Nombre](https://github.com/0xvanguard) — disponible para integrar este lab en pipelines de CI/CD, customizar reportes y entregar auditorías puntuales a clientes B2B.

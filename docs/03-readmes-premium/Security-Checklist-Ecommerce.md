# Security Checklist E-commerce

> Audita una tienda online y entrega un reporte PDF priorizado por riesgo. Pensado para agencias y pymes que necesitan cerrar brechas antes de que las explote alguien.

![status](https://img.shields.io/badge/status-active-brightgreen)
![python](https://img.shields.io/badge/python-3.10%2B-blue)
![license](https://img.shields.io/badge/license-MIT-lightgrey)

![Security Checklist E-commerce — demo](docs/img/demo.png)
*<sub>Reemplazar con captura real de la herramienta corriendo o del reporte PDF generado.</sub>*

---

## El problema

La mayoría de tiendas Shopify, WooCommerce y Magento se publican con configuraciones por defecto inseguras: cabeceras HTTP sin endurecer, endpoints administrativos expuestos, certificados TLS débiles y dependencias sin parchear. Las agencias que las construyen rara vez auditan esto antes de entregar al cliente. El resultado: brechas, fraude de tarjetas, defacement y pérdida de reputación.

## La solución

Una herramienta CLI con interfaz web opcional que recibe la URL de una tienda online y produce un reporte PDF con:

- Hallazgos clasificados como **Crítico / Alto / Medio / Bajo / Informativo**.
- Evidencia técnica de cada hallazgo (request, response, configuración detectada).
- Recomendación accionable para cada uno (qué cambiar, dónde, cómo verificar).
- Resumen ejecutivo de una página, pensado para que el dueño del negocio entienda el riesgo sin saber HTTP.

## Para quién

- **Agencias de e-commerce** que necesitan ofrecer auditorías rápidas como upsell.
- **Dueños de tiendas online** que quieren un check independiente antes de campañas de alto tráfico.
- **AppSec / DevSecOps engineers** que quieren un punto de partida automatizable para auditar muchas tiendas.

## Qué audita hoy

- Cabeceras HTTP de seguridad: `Strict-Transport-Security`, `Content-Security-Policy`, `X-Frame-Options`, `X-Content-Type-Options`, `Referrer-Policy`, `Permissions-Policy`.
- Configuración TLS: versiones soportadas, cifrados habilitados, validez del certificado.
- Exposición de endpoints sensibles típicos: `/wp-admin`, `/admin`, `/.git`, `/.env`, archivos de backup.
- Detección de plataforma (Shopify, WooCommerce, Magento, PrestaShop) y revisión de configuraciones específicas por plataforma.
- Análisis de dependencias del front-end visibles (versiones de jQuery, librerías JS conocidas con CVEs).
- Generación de reporte PDF con plantilla profesional.

## Stack técnico

- **Python 3.10+**
- **Requests / httpx** para sondeo HTTP.
- **BeautifulSoup** para parsing del front-end.
- **OpenSSL bindings** para inspección TLS.
- **WeasyPrint** o **ReportLab** para PDF.
- **Click** para CLI.
- **FastAPI** (opcional) para la interfaz web.
- **Docker** para empaquetado reproducible.

## Cómo correrlo en 60 segundos

```bash
git clone https://github.com/0xvanguard/Security-Checklist-Ecommerce.git
cd Security-Checklist-Ecommerce
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python -m security_checklist scan https://tienda-objetivo.com --output reporte.pdf
```

Con Docker:

```bash
docker build -t security-checklist .
docker run --rm -v "$PWD/out:/out" security-checklist \
  scan https://tienda-objetivo.com --output /out/reporte.pdf
```

## Arquitectura (alto nivel)

```
┌──────────────┐    ┌────────────────┐    ┌──────────────────┐
│   CLI / Web  │───▶│  Scan Engine   │───▶│   Findings DB    │
│   (Click /   │    │  (checks por   │    │   (in-memory /   │
│   FastAPI)   │    │  categoría)    │    │   SQLite)        │
└──────────────┘    └────────────────┘    └──────────────────┘
                            │                      │
                            ▼                      ▼
                    ┌────────────────┐    ┌──────────────────┐
                    │ Plugins por    │    │  PDF Reporter    │
                    │ plataforma     │    │  (WeasyPrint /   │
                    │ (Shopify, Woo) │    │  ReportLab)      │
                    └────────────────┘    └──────────────────┘
```

## Roadmap corto

- [ ] Plugins adicionales para BigCommerce y Tiendanube.
- [ ] Integración con APIs de CVE (NVD) para enriquecer hallazgos de dependencias.
- [ ] Modo *diff*: comparar dos escaneos de la misma tienda en el tiempo.
- [ ] Generación de checklist accionable en formato Markdown para el equipo de devs.
- [ ] Hooks de CI/CD para escaneo automático antes de cada deploy.

## Limitaciones conocidas

- Solo audita lo que es **visible públicamente**. No reemplaza un pentest autenticado.
- El detector de plataforma es heurístico: tiendas muy customizadas pueden no clasificarse correctamente.
- El reporte PDF depende de WeasyPrint/ReportLab; algunas plantillas necesitan fuentes locales adicionales.

## Licencia

MIT. Si lo usas comercialmente y te resulta útil, una mención al repo me ayuda a seguir mejorándolo.

## Contacto

Construido por [Tu Nombre](https://github.com/0xvanguard) — abierto a colaboración, contratos B2B y consultoría puntual sobre auditorías de e-commerce.

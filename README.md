# 🌍 Fichas Departamentales de Riesgo - UNGRD (Automatización Quarto)

Este proyecto automatiza la conversión, procesamiento y publicación de las **Fichas Departamentales de Caracterización de Escenarios de Riesgo** de la UNGRD. Transforma documentos de Microsoft Word (`.docx`) colaborativos alojados en Google Drive en un sitio web estático, interactivo y estructurado utilizando **Quarto** y **GitHub Pages**.

## 🚀 Arquitectura y Flujo de Trabajo

El sistema funciona bajo un modelo de Integración y Despliegue Continuo (CI/CD) adaptado para gestión documental:

1. **Almacenamiento (Google Drive):** Los funcionarios de la UNGRD redactan y actualizan las fichas en formato `.docx` dentro de una carpeta compartida. Esta es la "fuente de la verdad" del texto.
2. **Motor de Procesamiento (Google Colab):** Un script en Python actúa como puente (ETL). Se conecta al Drive, descarga los documentos y utiliza **Pandoc** para convertirlos a Markdown (`.qmd`). 
3. **Limpieza y Estructuración (Python):** El script limpia la "basura" del Word (como Tablas de Contenido estáticas), formatea las tablas en formato Grid, extrae las imágenes a carpetas locales relativas e inyecta niveles de encabezados (`#`, `##`) para la navegación web.
4. **Control de Versiones (GitHub):** El script hace `push` automático de los archivos `.qmd` estructurados a este repositorio.
5. **Despliegue Automático (GitHub Actions):** Al detectar cambios en la rama `main`, un *workflow* instala Quarto, renderiza el sitio web completo y lo publica en **GitHub Pages**.

## 🛠️ Tecnologías Utilizadas

* **Python 3:** Orquestación y limpieza de texto mediante Expresiones Regulares (Regex) y manipulación de cadenas.
* **Pandoc:** Motor de conversión profunda de `.docx` a formato Markdown.
* **GitPython:** Para la automatización de *commits* y *pushes* desde la nube.
* **Quarto:** Sistema de publicación científica y técnica para generar el HTML final.
* **GitHub Actions:** CI/CD para la compilación del sitio web.

## 📂 Estructura del Repositorio

```text
fichas-ungrd/
├── _quarto.yml               # Configuración global del sitio web interactivo
├── .github/
│   └── workflows/
│       └── publish.yml       # Script de GitHub Actions para el despliegue
├── fichas/                   # Fichas departamentales generadas
│   ├── cordoba/
│   │   ├── index.qmd         # Archivo Markdown renderizado
│   │   └── media/            # Imágenes extraídas del documento original
│   └── ... (otros departamentos)
└── README.md                 # Esta documentación

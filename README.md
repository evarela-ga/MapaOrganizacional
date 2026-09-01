# Mapa Organizacional GoodApps — GitHub Pages

Organigrama interactivo de GoodApps (GRH-RE-1) para hosting estático, sin base de datos.
Los datos viven en archivos JSON de texto plano dentro del mismo repositorio.

## Contenido

| Archivo | Qué es |
|---|---|
| `index.html` | Versión **anónima** (sin nombres) — página principal |
| `nominal.html` | Versión **nominal** (con colaboradores) — uso interno |
| `goodapps-org-data.json` | "Base de datos" en texto de la versión anónima |
| `goodapps-org-data-nominal.json` | "Base de datos" en texto de la versión nominal |
| `legajo.html` | **Legajo de Colaboradores** (sueldos, monotributo, prepaga, antigüedad, fotos) — CONFIDENCIAL |
| `goodapps-people-data.json` | "Base de datos" en texto del legajo |
| `fotos/` | Fotos de colaboradores: `<id>.jpg` (el id figura en el Excel de relevamiento) |

## Cómo publicarlo en GitHub Pages

1. Creá un repositorio en GitHub (por ejemplo `organigrama`). Si vas a subir la versión
   nominal o el legajo, hacelo **privado** (contiene datos personales — Ley 25.326); GitHub Pages
   sobre repos privados requiere plan Pro/Team.
2. Subí estos cuatro archivos a la raíz del repositorio (o a una carpeta `/docs`).
3. En **Settings → Pages**, en *Build and deployment* elegí *Deploy from a branch*,
   rama `main` y carpeta `/ (root)` (o `/docs` si usaste esa carpeta). Guardá.
4. En un minuto la página queda en `https://<usuario>.github.io/<repo>/`
   (la nominal en `https://<usuario>.github.io/<repo>/nominal.html`).

Requiere internet para cargar React y lucide desde CDN (cdnjs / jsdelivr).

## Cómo se guardan los datos

- **Automático (por navegador):** cada cambio se guarda solo en el `localStorage`
  del navegador de quien edita. Al recargar, la página usa la copia más reciente
  entre lo local y el JSON del repositorio.
- **Publicar para todos:** botón **Guardar** → descarga el JSON de datos
  (`goodapps-org-data*.json`). Subí ese archivo al repositorio reemplazando el
  existente (arrastrándolo en la web de GitHub y *Commit changes*). Al cargar,
  la página lee ese JSON y todos ven la misma versión.
- **Menú de descarga (⭳):** exportar Datos (JSON) / SVG / PNG, **Importar JSON**
  (cargar un archivo de datos) y **Restablecer datos locales** (vuelve al JSON
  publicado del repositorio).

## Notas

- La FUM del bloque ISO (GRH-RE-1) se actualiza sola al guardar.
- Si dos personas editan a la vez, vale el último JSON subido al repositorio:
  conviene que una sola persona (People/Dirección) publique los cambios.

## Legajo de Colaboradores (`legajo.html`)

- Lista por área con foto (o iniciales si no hay foto) y ficha completa al hacer clic:
  contacto, fecha de ingreso con **antigüedad calculada sola**, sueldo, premios,
  comisiones, prepaga, tipo y categoría de monotributo, observaciones.
- Todo se edita con doble clic; mismo esquema de guardado (localStorage + `goodapps-people-data.json`).
- **Fotos:** subí a `fotos/` un JPG por persona con el nombre `<id>.jpg`
  (por ejemplo `lorena.jpg`, `laura.jpg`, `bria.jpg`); la página la toma sola,
  tanto en el organigrama nominal futuro como en el legajo.
- **Este archivo contiene datos salariales: solo repositorio privado.**

## Asistente IA ("Preguntale al mapa")

- Botón ✨ en la barra del organigrama: abre un chat para consultar el mapa
  ("¿quién reporta a la COO?", "¿qué puestos están vacantes?", "¿cuántos seniors hay?").
- En GitHub Pages usa la **API de OpenAI**: pegá tu API key en el campo del panel.
  La key se guarda SOLO en el localStorage de ese navegador — **nunca** se escribe en
  los JSON ni en el repositorio. No comitees la key en ningún archivo.
- El modelo es configurable (por defecto `gpt-4o-mini`). Cada consulta envía a OpenAI
  el contenido del mapa (en la versión nominal incluye nombres y niveles): usalo con
  criterio de confidencialidad.

### Clave compartida del sitio (opcional)

Para que cualquier persona con acceso al sitio use la IA sin pegar su propia key:
renombrá `goodapps-ai-config.example.json` a `goodapps-ai-config.json` y poné tu
API key adentro. Las tres vistas la toman automáticamente y ocultan el campo de key.

**ADVERTENCIA:** en un repositorio público esa key queda visible para TODO internet
(OpenAI además la revoca automáticamente al detectarla). Usala únicamente en un
repositorio privado, con un límite de gasto configurado en OpenAI, y rotala si se filtra.

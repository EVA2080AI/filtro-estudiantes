# 📚 Filtro Estudiantes – Clase Copilot

Formulario para registrar la **intención de proyecto** de estudiantes de la clase de Microsoft Copilot.

## ✨ Funcionalidades
- Registro por nombre, apellido y **grupo (1–10)**
- Dropdown con **tipos de proyecto** (datos, automatización, contenido, código, etc.)
- Selector de **nivel de acceso a Copilot**
- Envío automático a **Google Sheets**
- Tabla de filtros en tiempo real

## 🚀 Cómo conectar Google Sheets

1. Abre [Google Sheets](https://sheets.google.com) y crea una hoja con estas columnas:
   `Nombre | Apellido | Grupo | Proyecto | Nivel Copilot | Descripción | Fecha`

2. Ve a **Extensiones → Apps Script** y pega este código:

```javascript
function doPost(e) {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  const data  = JSON.parse(e.postData.contents);
  sheet.appendRow([
    data.nombre, data.apellido, data.grupo,
    data.proyecto, data.nivel, data.descripcion, data.fecha
  ]);
  return ContentService
    .createTextOutput(JSON.stringify({ status: 'ok' }))
    .setMimeType(ContentService.MimeType.JSON);
}
```

3. Haz clic en **Implementar → Nueva implementación** → tipo **Aplicación web**
   - Ejecutar como: **Yo**
   - Acceso: **Cualquier usuario**
4. Copia la URL generada y pégala en `index.html` donde dice `TU_URL_DE_APPS_SCRIPT_AQUI`

## 🌐 Ver en vivo
Disponible en GitHub Pages: `https://<tu-usuario>.github.io/filtro-estudiantes/`

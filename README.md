# CatastroMap Padilla — Red de Agua Potable

Visor GIS web para el seguimiento de la construcción de la red de agua potable del Municipio de Padilla, Chuquisaca, Bolivia.

---

## 📁 Estructura de archivos

```
catastro-padilla/
├── index.html          ← Aplicación principal (no editar salvo configuración)
├── README.md           ← Este archivo
└── data/               ← PON AQUÍ TUS ARCHIVOS GEOJSON
    ├── red_distribucion.geojson
    ├── zanjas_abiertas.geojson
    ├── tendido_tuberia.geojson
    ├── zanjas_tapadas.geojson
    ├── valvulas.geojson
    ├── camaras.geojson
    └── predios.geojson
```

---

## 🗺️ Capas disponibles

| Capa | Color | Descripción |
|---|---|---|
| Red de Distribución | 🔵 Azul claro | Tuberías principales y secundarias |
| Zanjas Abiertas | 🟠 Naranja | Zanjas excavadas, aún sin tubería |
| Tendido de Tubería | 🟢 Verde limón | Tubería instalada, zanja aún abierta |
| Zanjas Tapadas | 🟣 Violeta | Tramos completamente terminados |
| Válvulas y Llaves | 🟡 Amarillo | Puntos de control de la red |
| Cámaras de Inspección | 🟢 Verde | Cámaras rompe-presión y de inspección |
| Predios / Acometidas | 🩷 Rosa | Lotes con acometida domiciliaria |

---

## ⚙️ Cómo conectar tus datos GeoJSON reales

1. Crea la carpeta `data/` junto al archivo `index.html`
2. Coloca tus archivos `.geojson` exportados desde QGIS con los nombres exactos listados arriba
3. En `index.html`, al final del script, cambia:
   ```js
   loadDemo();
   ```
   por:
   ```js
   loadFromFiles();
   ```
4. Descomenta la función `loadFromFiles()` y adáptala a tus datos

---

## 🚀 Publicar gratis en GitHub Pages (30 minutos)

1. Crea una cuenta en https://github.com
2. Crea un repositorio nuevo (ej: `catastro-padilla`)
3. Sube todos los archivos (index.html + carpeta data/)
4. Ve a **Settings → Pages → Source → main branch**
5. Tu mapa estará en: `https://TU-USUARIO.github.io/catastro-padilla/`

---

## 📍 Configuración del centro del mapa

En `index.html` busca la sección `CONFIG`:

```js
const CONFIG = {
  center: [-19.3069, -64.3036],  // Latitud, Longitud de Padilla
  zoom: 15,                       // 14-16 para nivel calle
};
```

---

## 🔧 Propiedades recomendadas en tus GeoJSON

### Líneas (red, zanjas, tendido)
```json
{
  "id": "T-001",
  "diametro": "110 mm",
  "material": "PVC",
  "longitud": "250 m",
  "fecha": "2025-10-01",
  "cuadrilla": "A",
  "observacion": "Sin novedad"
}
```

### Puntos (válvulas, cámaras)
```json
{
  "id": "V-001",
  "tipo": "Válvula compuerta",
  "diametro": "110 mm",
  "estado": "Abierta",
  "instalacion": "2025-10-03"
}
```

### Polígonos (predios)
```json
{
  "id": "P-001",
  "propietario": "Juan Mamani",
  "catastro": "15-001",
  "acometida": "Pendiente"
}
```

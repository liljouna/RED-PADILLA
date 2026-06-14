# 🔥 Activar Firebase (tiempo real entre todos los celulares)

## Paso 1 — Crear proyecto Firebase (gratis)
1. Ve a https://console.firebase.google.com
2. Clic en **"Agregar proyecto"**
3. Nombre: `catastro-padilla`
4. Desactiva Google Analytics (no es necesario)
5. Clic en **Crear proyecto**

## Paso 2 — Crear base de datos Firestore
1. En el menú izquierdo: **Firestore Database**
2. Clic en **Crear base de datos**
3. Selecciona **Modo de prueba** (permite lectura/escritura libre por 30 días)
4. Elige región: `us-central1`
5. Clic en **Habilitar**

## Paso 3 — Obtener configuración
1. En el menú izquierdo: ⚙️ **Configuración del proyecto**
2. Baja hasta **"Tus apps"** → clic en **</>** (Web)
3. Nombre de la app: `catastro-web`
4. Clic en **Registrar app**
5. Copia el bloque `firebaseConfig` que aparece

## Paso 4 — Pegar en index.html
Abre `index.html` y busca esta sección:

```js
const FB_CONFIG = {
  apiKey:            "TU_API_KEY",
  authDomain:        "TU_PROJECT.firebaseapp.com",
  projectId:         "TU_PROJECT_ID",
  storageBucket:     "TU_PROJECT.appspot.com",
  messagingSenderId: "TU_SENDER_ID",
  appId:             "TU_APP_ID"
};
const USE_FIREBASE = false; // ← Cambia esto
```

Reemplaza los valores con los de tu proyecto y cambia `false` por `true`:
```js
const USE_FIREBASE = true;
```

## Paso 5 — Reglas de seguridad Firestore
En Firebase Console → Firestore → **Reglas**, pega esto:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /registros_padilla/{doc} {
      allow read, write: if true; // Acceso libre (equipo interno)
    }
  }
}
```

## Paso 6 — Subir index.html actualizado a GitHub
Arrastra el nuevo `index.html` al repositorio GitHub (reemplaza el anterior).
GitHub Pages actualizará el sitio en ~2 minutos.

## ✅ Resultado
- Cualquier persona del equipo que abra la URL podrá:
  - Ver los registros de todos en tiempo real
  - Agregar zanjas, tendidos, válvulas desde el celular
  - Los datos se sincronizan automáticamente cuando hay señal
  - Sin señal: los datos se guardan localmente y suben cuando vuelve internet

## 📱 Sin Firebase (modo offline)
Si no configuras Firebase, la app igual funciona:
- Los registros se guardan en el celular (localStorage)
- Cada persona ve solo sus propios registros
- No hay sincronización entre dispositivos

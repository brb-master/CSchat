# Nuestro chat 💙💗

## 1. Firebase (gratis, 5 minutos)
1. Entra en https://console.firebase.google.com → **Crear proyecto** (sin Analytics).
2. **Compilación → Firestore Database → Crear base de datos** (modo producción, región europe-west).
3. Pestaña **Reglas** y pega esto, luego **Publicar**:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{db}/documents {
    match /messages/{id} { allow read, create: if true; }
  }
}
```
4. **Configuración del proyecto (rueda) → Tus apps → Web (</>)** → registra la app y copia el `firebaseConfig`.
5. Pégalo en `index.html` (sección `firebaseConfig`).

## 2. GitHub Pages
1. Crea un repo nuevo y sube `index.html` y este README (Add file → Upload files).
2. **Settings → Pages → Branch: main / root → Save**.
3. Tu chat estará en `https://TU_USUARIO.github.io/NOMBRE_REPO/`.

## Usuarios
- bilal / bilal123 (azul)
- anna / anna123 (rosa)

## Uso
- 📎 sube fotos, gifs o archivos (máx ~700 KB por mensaje).
- Pega un link normal y sale clicable; pega un link directo a un gif (termina en .gif o de media.giphy.com) y se ve animado.

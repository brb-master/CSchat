# Nuestro chat 💙💗

## 1. Firebase Authentication (seguridad)
1. Firebase Console → **Compilación → Authentication → Comenzar → Email/contraseña → Habilitar**.
2. Pestaña **Usuarios → Añadir usuario** (2 usuarios, con contraseñas fuertes):
   - `bilal@nuestrochat.app`
   - `anna@nuestrochat.app`
3. En **Configuración → Acciones del usuario**, desactiva "Permitir crear usuarios" si aparece la opción.
4. En **Authentication → Configuración → Dominios autorizados** deja solo `TU_USUARIO.github.io`.

## 2. Reglas de Firestore (Firestore → Reglas → Publicar)
```
rules_version = '2';
service cloud.firestore {
  match /databases/{db}/documents {
    function member() {
      return request.auth != null &&
        request.auth.token.email in ['bilal@nuestrochat.app','anna@nuestrochat.app'];
    }
    function who() { return request.auth.token.email.split('@')[0]; }

    match /messages/{id} {
      allow read: if member();
      allow create: if member() && request.resource.data.user == who();
      allow update: if member() && (
        request.resource.data.diff(resource.data).affectedKeys().hasOnly(['readBy','readAt','reactions']) ||
        (resource.data.user == who() &&
         request.resource.data.diff(resource.data).affectedKeys().hasOnly(['text','edited']))
      );
      allow delete: if member() && resource.data.user == who();
    }
    match /presence/{u} { allow read: if member(); allow write: if member() && u == who(); }
    match /plans/{id}   { allow read, write: if member(); }
    match /config/{id}  { allow read, write: if member(); }
  }
}
```

## 3. Restringe la API key (Google Cloud)
console.cloud.google.com → APIs y servicios → Credenciales → tu "Browser key" →
**Restricciones de sitio web** → añade `https://TU_USUARIO.github.io/*`.

## 4. GIFs (opcional)
Crea una API key gratis en https://developers.giphy.com y pégala en `GIPHY_KEY` dentro de `index.html`.

## 5. GitHub Pages
Sube TODOS los archivos a la raíz del repo: `index.html`, `sw.js`, `manifest.json`, `icon-192.png`, `icon-512.png`, `README.md`.

## Instalar como app
- Android (Chrome): menú ⋮ → **Instalar app**.
- iPhone (Safari): Compartir → **Añadir a pantalla de inicio** (necesario para notificaciones en iOS 16.4+).

## Uso
- Toca un mensaje: reaccionar, responder, editar o borrar (editar/borrar solo los tuyos).
- 😊 emojis y GIFs · 📍 ubicación · 📝 planes pendientes · toca "días juntos" para poner la fecha.

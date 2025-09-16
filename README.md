# cburgher.github.io — Apple Universal Links (AASA)

Este repo sirve los archivos `apple-app-site-association` (AASA) desde GitHub Pages para habilitar Universal Links en iOS.

## Estructura

- `.nojekyll`: evita que Jekyll procese y oculte rutas con punto (`.well-known`).
- `apple-app-site-association`: archivo AASA en raíz (sin extensión).
- `/.well-known/apple-app-site-association`: copia del AASA en la ruta estándar.

## Qué editar

1. Reemplaza `TEAMID.BUNDLEID` por tu App ID:
   - `TEAMID` = Team ID de tu cuenta Apple Developer.
   - `BUNDLEID` = Bundle Identifier (ej. `com.tuapp.ios`).
   - Formato final: `TEAMID.com.tuapp.ios`.
2. Ajusta `paths` si no quieres permitir todos los paths (`"*"`). Por ejemplo:
   ```json
   "paths": ["/ul/*", "/promo/*", "NOT /privado/*"]
   ```

> Puedes añadir múltiples apps creando más objetos en `details`.

## Publicación

1. Confirma que el repo se llama exactamente `cburgher.github.io` y es público.
2. Sube cambios a `main`:
   ```bash
   git add .
   git commit -m "Add AASA files and nojekyll"
   git push origin main
   ```
3. En Settings → Pages, verifica que la fuente sea la rama `main` (carpeta `/` raíz). Para repos de usuario suele quedar automático.
4. Espera ~1–5 minutos a que se propague.

## Verificación rápida

- Abre en Safari (o `curl`) estas URLs y verifica que devuelven JSON:
  - https://cburgher.github.io/apple-app-site-association
  - https://cburgher.github.io/.well-known/apple-app-site-association

> Nota: GitHub Pages puede servir el archivo con `content-type` genérico; iOS lo acepta a partir de iOS 12/13. Lo importante es que el JSON sea válido y accesible sin redirecciones.

## Configuración en iOS

1. En tu target iOS: Signing & Capabilities → `Associated Domains`.
2. Añade: `applinks:cburgher.github.io` (y cualquier subdominio adicional si aplica).
3. Build e instala en un dispositivo.

## Prueba de Universal Links

- Envía o abre un enlace que coincida con `paths` (p.ej. `https://cburgher.github.io/ul/demo`).
- Al tocar, debería abrir tu app si está instalada; si no, abrir Safari.

## Notas

- Mantener ambos AASA (raíz y `/.well-known/`) mejora compatibilidad con diferentes versiones de iOS.
- No uses extensión `.json`; el nombre debe ser exactamente `apple-app-site-association`.


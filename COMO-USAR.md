# CronOS — Guía rápida

CronOS ya es una **PWA** (aplicación web instalable). Esta carpeta contiene todo lo necesario:

```
CronOS/
├─ index.html              ← la app
├─ manifest.webmanifest    ← nombre, íconos, colores
├─ service-worker.js       ← permite usarla sin conexión
└─ icons/                  ← íconos del cronómetro
```

## Lo importante que debes saber

Una PWA necesita servirse por **HTTPS** (o `localhost`) para poder instalarse y
funcionar sin conexión. Si abres `index.html` con doble clic (`file://`),
la app funciona, pero **no** podrás instalarla ni generar el APK. Hay que
"publicarla" en una URL. A continuación, de lo más simple a lo más completo.

---

## Opción A — Probarla e instalarla en el celular (sin APK)

1. Publica la carpeta en cualquier hosting estático gratuito:
   - **Netlify Drop**: arrastra la carpeta `CronOS` a https://app.netlify.com/drop
   - o **GitHub Pages**: sube la carpeta a un repo y actívalo en Settings → Pages.
   - o **Cloudflare Pages**, **Vercel**, etc. Todos sirven.
2. Abre la URL resultante en **Chrome** (Android) o **Safari** (iPhone).
3. Instálala:
   - **Android/Chrome**: menú ⋮ → *Instalar aplicación* / *Agregar a pantalla de inicio*.
   - **iPhone/Safari**: botón Compartir → *Agregar a inicio*.

Queda como un ícono propio, a pantalla completa y funciona sin internet.
Para muchos usos, esto ya reemplaza a un APK.

---

## Opción B — Generar el APK con PWABuilder (recomendado, sin programar)

Una vez que tienes la URL pública (paso A.1):

1. Entra a **https://www.pwabuilder.com**
2. Pega la URL de tu PWA y dale *Start*.
3. Te analizará el manifest e íconos (ya están listos). Elige **Android** →
   *Generate Package*.
4. Descargas un `.zip` con el **APK** (y un `.aab` para la Play Store si algún día
   quieres publicarla).
5. Pasa el APK al teléfono e instálalo (activa "Instalar apps de orígenes
   desconocidos" en Ajustes la primera vez).

> El APK que genera es una *TWA* (Trusted Web Activity): básicamente tu PWA
> envuelta en una app Android nativa.

---

## Opción C — Bubblewrap (línea de comandos, de Google)

Si prefieres hacerlo tú con herramientas:

```bash
npm install -g @bubblewrap/cli
bubblewrap init --manifest https://TU-URL/manifest.webmanifest
bubblewrap build      # produce el APK firmado
```

Requiere tener instalado el JDK y el Android SDK.

---

## Opción D — Capacitor (máximo control, para crecer a futuro)

Si más adelante quieres funciones nativas (vibración, notificaciones, etc.):

```bash
npm init -y
npm install @capacitor/core @capacitor/cli @capacitor/android
npx cap init CronOS com.tuusuario.cronos --web-dir=.
npx cap add android
npx cap copy
npx cap open android     # abre Android Studio para compilar el APK
```

---

## Notas

- **Fuentes sin conexión**: las tipografías se cargan desde Google Fonts. Sin
  internet, la app usa fuentes del sistema (se ve perfecta igual). Si quieres que
  las fuentes funcionen 100% offline, se pueden incrustar en el proyecto; pídemelo.
- El nombre, color e íconos del APK salen del `manifest.webmanifest`. Si cambias
  algo ahí, regenera el APK.
- Cambié el `theme_color` y `background_color` al negro de la app; puedes
  ajustarlos al gusto.

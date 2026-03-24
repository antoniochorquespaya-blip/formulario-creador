# 🚀 GUÍA PASO A PASO — Formulario del Creador

## ¿Qué es esto?

Una web con tu formulario de 24 preguntas que puedes compartir por link.
Incluye un panel admin protegido con contraseña donde ves todas las respuestas.
Opcionalmente te llega un email cada vez que alguien lo rellena.

---

## PASO 1: Crear cuenta en Vercel (hosting gratuito)

1. Ve a **https://vercel.com**
2. Haz clic en **"Sign Up"**
3. Elige **"Continue with GitHub"** (si no tienes GitHub, créate una cuenta en github.com primero — es gratis)
4. Autoriza Vercel

---

## PASO 2: Subir tu proyecto a GitHub

1. Ve a **https://github.com** y haz login
2. Haz clic en el botón **"+"** arriba a la derecha → **"New repository"**
3. Ponle de nombre: `formulario-creador`
4. Déjalo en **Public** o **Private** (da igual)
5. Haz clic en **"Create repository"**
6. En la página que aparece, haz clic en **"uploading an existing file"**
7. Arrastra TODOS los archivos de la carpeta que te he dado:
   - `public/index.html`
   - `vercel.json`
8. Haz clic en **"Commit changes"**

**IMPORTANTE**: Asegúrate de que `index.html` quede dentro de una carpeta `public/`.
La estructura debe ser:
```
formulario-creador/
├── public/
│   └── index.html
└── vercel.json
```

---

## PASO 3: Desplegar en Vercel

1. Ve a **https://vercel.com/dashboard**
2. Haz clic en **"Add New" → "Project"**
3. Busca tu repositorio `formulario-creador` y haz clic en **"Import"**
4. En "Framework Preset" selecciona **"Other"**
5. En "Output Directory" pon: **public**
6. Haz clic en **"Deploy"**
7. Espera 30 segundos... ¡LISTO!

Vercel te dará un link tipo: `https://formulario-creador.vercel.app`

---

## PASO 4: Compartir los links

- **Formulario para creadores**: `https://tu-dominio.vercel.app`
- **Panel admin**: `https://tu-dominio.vercel.app?admin`

La contraseña por defecto del admin es: **obs2024**
(la puedes cambiar editando el archivo index.html, línea de ADMIN_PASSWORD)

---

## PASO 5 (OPCIONAL): Configurar notificaciones por email

Si quieres recibir un email cada vez que alguien rellene el formulario:

### 5a. Crear cuenta en EmailJS (gratis hasta 200 emails/mes)

1. Ve a **https://www.emailjs.com** y crea una cuenta
2. En el dashboard, ve a **"Email Services"** → **"Add New Service"**
3. Elige **Gmail** (o el que uses)
4. Conecta tu cuenta de Gmail
5. Apunta el **Service ID** (ej: `service_abc123`)

### 5b. Crear template de email

1. Ve a **"Email Templates"** → **"Create New Template"**
2. Pon este contenido:

**Subject:** `Nueva respuesta: {{creator_name}} — {{project_name}}`

**Body:**
```
¡Nueva respuesta al formulario!

Creador: {{creator_name}}
Proyecto: {{project_name}}
Preguntas respondidas: {{answered_count}}
Fecha: {{date}}

═══════════════════════════════════
RESPUESTAS COMPLETAS
═══════════════════════════════════

{{full_responses}}
```

3. En **"To Email"** pon: `{{to_email}}`
4. Guarda y apunta el **Template ID** (ej: `template_xyz789`)

### 5c. Obtener tu Public Key

1. Ve a **"Account"** → **"API Keys"**
2. Copia tu **Public Key**

### 5d. Meter las claves en el código

Abre `public/index.html` y busca la sección CONFIG al principio del script.
Rellena los 4 campos:

```javascript
const CONFIG = {
  ADMIN_PASSWORD: "obs2024",
  EMAILJS_PUBLIC_KEY: "TU_PUBLIC_KEY_AQUI",
  EMAILJS_SERVICE_ID: "TU_SERVICE_ID_AQUI",
  EMAILJS_TEMPLATE_ID: "TU_TEMPLATE_ID_AQUI",
  NOTIFY_EMAIL: "tuemail@gmail.com",
};
```

Guarda, sube los cambios a GitHub, y Vercel se actualiza solo.

---

## NOTAS IMPORTANTES

### Sobre las respuestas
- Las respuestas se guardan en el **localStorage del navegador**
- Esto significa que las respuestas se guardan en el dispositivo de cada persona
- Las respuestas del ADMIN se ven en el navegador donde se recibieron
- **Para un uso con 5-20 creadores, la mejor forma de recoger respuestas es por EMAIL** (Paso 5)
- Cada vez que un creador envíe el formulario, recibirás el email completo con todas sus respuestas

### Sobre la contraseña del admin
- Cámbiala en el código antes de publicar
- Busca `ADMIN_PASSWORD: "obs2024"` y pon la que quieras

### Dominio personalizado (opcional)
- Si quieres un dominio tipo `formulario.tuchorpa.com`:
  1. En Vercel → Settings → Domains
  2. Añade tu dominio
  3. Configura los DNS que te indica Vercel

### Actualizar el formulario
- Si quieres cambiar preguntas, edita el archivo `index.html`
- Sube los cambios a GitHub
- Vercel detecta el cambio y despliega automáticamente

---

## ¿Problemas?

- **No se ve la web**: Comprueba que `index.html` está dentro de `public/`
- **No llegan emails**: Verifica las claves de EmailJS y que el template tenga los campos correctos
- **Se olvidó la contraseña admin**: Edítala en el código y sube a GitHub


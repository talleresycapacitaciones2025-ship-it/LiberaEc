# 🌸 LiberaEc – Acompañamiento seguro contra la violencia de género en Ecuador

LiberaEc es un **chatbot inteligente** diseñado para brindar acompañamiento, información y orientación a mujeres en situación de violencia de género en Ecuador. Utiliza **IA generativa (Groq)** para responder con empatía, recursos legales y pasos concretos, priorizando la seguridad y confidencialidad de la usuaria.

🔒 **Privacidad total**: Las conversaciones no se almacenan en ningún servidor. Solo se procesan en el momento a través de Cloudflare Workers.

---

## 📲 Descarga la APK (Android)

Instala LiberaEc directamente en tu dispositivo Android.

> ⚠️ **Nota de seguridad**: Es posible que Android te muestre una advertencia al instalar una APK fuera de Play Store. Debes habilitar "Orígenes desconocidos" o "Permitir instalación de aplicaciones desconocidas" en los ajustes de tu dispositivo.

### 📥 Enlace directo de descarga

🔗 **[Descargar LiberaEc v1.0.0 APK](https://github.com/talleresycapacitaciones2025-ship-it/LiberaEc/releases/download/v1.0.0/LiberaEc-v1.0.0.apk)**

*(Si el enlace no funciona, ve a la sección de **Releases** y descarga el archivo manualmente)*

### 🔄 Otras versiones

Todas las versiones APK publicadas están disponibles en:  
👉 [https://github.com/talleresycapacitaciones2025-ship-it/LiberaEc/releases](https://github.com/talleresycapacitaciones2025-ship-it/LiberaEc/releases)

---

## 📱 Características principales

- 🧠 **Respuestas con IA** usando el modelo `llama-3.3-70b-versatile` de Groq.
- 💬 **Modo test** (6 preguntas para detectar señales de violencia).
- 📚 **Explicación de tipos de violencia**: psicológica, física, sexual, económica, vicaria y digital.
- 🚨 **Recursos de emergencia**: 911, 147 (Línea Mujer), 1800 VIOLETA, Fiscalía 1800-354-378.
- 🧼 **Botón limpiar chat** para reiniciar la conversación.
- 🔴 **Botón "Salir rápido"** que redirige a Google.
- 📱 **Diseño responsive** – móviles y ordenadores.
- 🌍 **Desplegable en GitHub Pages** y **APK para Android**.

---

## 🏗️ Arquitectura del proyecto
Frontend (HTML/CSS/JS) → GitHub Pages
↓
Cloudflare Worker (proxy a Groq)
↓
Groq API (llama-3.3-70b-versatile)

---

🔧 Cómo se construyó LiberaEc (con 🧠💜)
El proyecto se desarrolló siguiendo una arquitectura simple pero robusta, priorizando la privacidad, la velocidad y la accesibilidad desde cualquier dispositivo.

🧱 Frontend 100% estático
Se escribió un único archivo index.html con HTML5, CSS (variables, flexbox, diseño responsive) y JavaScript vanilla. No se usaron frameworks ni dependencias externas para mantener ligereza y facilitar su despliegue en cualquier servidor web.

🤖 Conexión con IA a través de Groq
Se integró el modelo llama-3.3-70b-versatile de Groq, que ofrece respuestas rápidas, gratuitas y de alta calidad. Para evitar exponer la clave API en el cliente, se creó un Cloudflare Worker que actúa como proxy: recibe el mensaje desde el frontend, añade un system prompt especializado en violencia de género y leyes ecuatorianas, llama a Groq y devuelve la respuesta al chat.

📝 Prompt del sistema optimizado
El systemPrompt se diseñó con instrucciones muy concretas: validación emocional, prioridad de seguridad, uso de negritas, listas y emojis suaves, prohibición de frases genéricas, y explicación detallada de casos como violencia vicaria o violencia digital. Se incluyó un ejemplo de respuesta ideal para guiar al modelo.

✨ Procesamiento del texto en el frontend
Para que las respuestas de Groq (que vienen en Markdown simple) se vean correctamente, se implementó una función formatMarkdown() que convierte **negritas** en <strong> y transforma títulos con ### en negritas también, todo antes de inyectar el HTML en el chat.

🔴 Botón de “Salir rápido”
Se añadió un botón flotante rojo que, al pulsarlo, cambia la opacidad de la página y redirige a https://www.google.com en 150 ms. Esto permite a la usuaria ocultar la conversación de forma inmediata si alguien se acerca.

🧹 Limpieza del chat
Se incorporó un botón “Limpiar” en el menú inferior que vacía el contenedor del chat, reinicia el estado del test interactivo y vuelve a mostrar el mensaje de bienvenida con las opciones iniciales. Esto mejora la usabilidad en conversaciones largas.

📊 Test de violencia integrado
El test consiste en 6 preguntas con respuestas “Sí”, “No” o “No estoy segura”. Al finalizar, se muestra un resultado orientativo y se ofrecen recursos de ayuda. Todo el estado del test se maneja localmente en el frontend, sin llamadas a la IA.

📲 Generación de la APK para Android
Una vez finalizada la versión web, se utilizó la herramienta Web2APK para empaquetar el sitio (alojado en GitHub Pages) en una aplicación nativa Android. La APK resultante se firmó y se subió a la sección Releases de GitHub, con un enlace directo de descarga.

🛡️ Control de errores y fallback local
El Worker incluye un try/catch que, si Groq falla o la API key no está configurada, devuelve respuestas locales predefinidas (básicas pero útiles) para no dejar a la usuaria sin orientación. En el frontend también se capturan errores de red y se muestran mensajes amigables.

🔒 Privacidad desde el diseño
No se utiliza ningún sistema de almacenamiento de conversaciones (ni local, ni en servidor). Cada mensaje se envía directamente al Worker, se procesa y se olvida. El botón de limpiar chat elimina cualquier rastro visual en el dispositivo.

Este enfoque permitió crear una herramienta funcional, segura y accesible sin costes de infraestructura, utilizando solo servicios gratuitos (GitHub Pages, Cloudflare Workers, Groq) y código abierto. 💜🚀

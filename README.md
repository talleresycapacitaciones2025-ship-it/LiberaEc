# 🌸 LiberaEc – Acompañamiento seguro contra la violencia de género en Ecuador

LiberaEc es un **chatbot inteligente** diseñado para brindar acompañamiento, información y orientación a mujeres en situación de violencia de género en Ecuador. Utiliza **IA generativa (Groq)** para responder con empatía, recursos legales y pasos concretos, priorizando la seguridad y confidencialidad de la usuaria.

🔒 **Privacidad total**: Las conversaciones no se almacenan en ningún servidor. Solo se procesan en el momento a través de Cloudflare Workers.

---

## 📱 Características principales

- 🧠 **Respuestas con IA** usando el modelo `llama-3.3-70b-versatile` de Groq.
- 💬 **Modo test** (6 preguntas para detectar señales de violencia).
- 📚 **Explicación de tipos de violencia**: psicológica, física, sexual, económica, vicaria y digital.
- 🚨 **Recursos de emergencia**: 911, 147 (Línea Mujer), 1800 VIOLETA, Fiscalía 1800-354-378.
- 🧼 **Botón limpiar chat** para reiniciar la conversación.
- 🔴 **Botón "Salir rápido"** que redirige a Google para proteger la privacidad.
- 📱 **Diseño responsive** – funciona en móviles y ordenadores.
- 🌍 **Desplegable en GitHub Pages** y **APK para Android** (generada con Web2APK).

---

## 🏗️ Arquitectura del proyecto
Frontend (HTML/CSS/JS) → GitHub Pages
↓
Cloudflare Worker (proxy a Groq)
↓
Groq API (llama-3.3-70b-versatile)

- **Frontend**: Interfaz de chat, test, botones de recursos y limpieza.
- **Worker**: Recibe el mensaje, añade un `system_prompt` especializado (leyes ecuatorianas, violencia vicaria, etc.), llama a Groq y devuelve la respuesta.
- **Groq**: Modelo de IA gratuito (veloz y sin costo en el plan actual).

---

## 🚀 Despliegue en GitHub Pages

1. **Clona o descarga este repositorio**.
2. **Sube los archivos** (principalmente `index.html`) a un repositorio público en GitHub.
3. Activa **GitHub Pages**:
   - Ve a `Settings` → `Pages`
   - En "Branch", selecciona `main` y la carpeta `/ (root)`
   - Guarda.
4. Tu página estará disponible en `https://TU_USUARIO.github.io/NOMBRE_REPO/`

---

## ⚙️ Configuración del Cloudflare Worker (obligatorio para la IA)

LiberaEc necesita un Worker que actúe como proxy a Groq. Sigue estos pasos:

1. Crea una cuenta en [Cloudflare](https://workers.cloudflare.com/) (gratuita).
2. Crea un nuevo Worker con el nombre que elijas (ej. `liberaec-ai`).
3. Copia el código del Worker (se encuentra en el archivo `worker.js` de este repositorio) y pégalo en el editor.
4. **Añade la variable de entorno**:
   - Ve a `Settings` → `Variables`
   - Agrega `GROQ_API_KEY` con tu clave de Groq (consíguela gratis en [console.groq.com](https://console.groq.com/)).
5. Despliega el Worker y anota su URL (ej. `https://liberaec-ai.tu-usuario.workers.dev`).
6. **En el `index.html`** modifica la línea:
   ```javascript
   const url = 'https://liberaec-ai.talleresycapacitaciones2025.workers.dev/chat';

  Reemplázala con la URL de tu propio Worker.

  📦 Convertir la web en APK
Ya puedes generar un archivo .apk usando herramientas como Web2APK o PWA Builder.
Pasos rápidos (Web2APK):

Ve a web2apk.com.
Introduce la URL de tu GitHub Pages (ej. https://tusuario.github.io/LiberaEc/).
Personaliza el nombre, icono, etc.
Genera la APK y descárgala.

Para distribuirla, súbela a GitHub Releases (explicado más abajo).

  🛠️ Personalización avanzada
Modificar el prompt del Worker
El archivo worker.js contiene la variable systemPrompt. Puedes editarla para:

Ajustar el tono (más cálido, más directo).

Añadir nuevas leyes o recursos.

Incluir ejemplos de respuestas (few-shot).

Cambiar el modelo de Groq
Dentro del Worker, busca model: "llama-3.3-70b-versatile". Otros modelos válidos:

llama-3.1-8b-instant (más rápido)

mixtral-8x7b-32768 (buen equilibrio)

📄 Licencia
Este proyecto se distribuye bajo la licencia MIT. Puedes usarlo, modificarlo y redistribuirlo libremente, siempre que mantengas la atribución original.


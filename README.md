# 🚀 AI Lead Scraper & Qualifier (n8n + LLM)

Este proyecto es una automatización avanzada construida en **n8n** diseñada para transformar el proceso de prospección comercial B2B. Utiliza scraping de resultados de búsqueda y análisis web mediante Inteligencia Artificial para encontrar, auditar y calificar negocios locales de forma totalmente automática.

---

## 🎯 Descripción del problema y solución

**El Problema:**
La prospección B2B tradicional para agencias de marketing y desarrollo web es un proceso extremadamente lento, manual y poco escalable. Un vendedor o consultor debe buscar negocios en Google Maps, entrar a sus páginas web una por una, auditar visualmente el sitio para encontrar deficiencias (falta de llamados a la acción, mala experiencia móvil, problemas de SEO local, diseño desactualizado), y luego redactar un mensaje personalizado para intentar captar la atención del dueño. Este proceso manual consume horas de trabajo diario, limita drásticamente el volumen de leads que se pueden contactar y a menudo resulta en mensajes genéricos de bajo impacto. Además, es muy difícil priorizar qué negocios tienen el mayor potencial de convertirse en clientes sin realizar primero esa auditoría manual que consume tanto tiempo.

**La Solución:**
Este flujo automatizado resuelve el cuello de botella de la prospección delegando la investigación y el análisis a un agente de Inteligencia Artificial. El sistema recibe una consulta (ej. "clínicas dentales en Buenos Aires"), extrae masivamente los datos de Google Places (incluyendo teléfono y dirección) y visita automáticamente la página web de cada negocio. Una vez allí, un modelo de lenguaje (LLM) asume el rol de un Auditor Senior: lee el contenido del sitio, evalúa su calidad técnica y comercial (UX/UI, CRO, SEO), le asigna un "Lead Score" basado en la urgencia de sus problemas, y redacta un mensaje de ventas altamente personalizado y persuasivo. Finalmente, el sistema consolida toda esta inteligencia en una base de datos de Supabase y una hoja de Google Sheets, entregándole al equipo de ventas un pipeline de leads calificados, con sus problemas detectados y el argumento comercial listo para ser enviado, reduciendo el tiempo de prospección de horas a segundos.

---

## ⚙️ Arquitectura y Tecnologías

El flujo de trabajo se compone de los siguientes nodos e integraciones:

*   **n8n (Self-Hosted):** Motor principal de orquestación y automatización del flujo.
*   **Serper API (Google Places/Search):** Utilizado para el scraping de negocios locales, obteniendo nombres, direcciones, teléfonos y URLs.
*   **HTTP Requests:** Para extraer el HTML y contenido de las páginas web de los leads encontrados.
*   **IA Agent (LangChain / Groq / Gemini):** Procesamiento de lenguaje natural mediante un prompt de ingeniería avanzada para auditar la web, extraer insights comerciales y redactar mensajes personalizados.
*   **Supabase Vector Store:** Almacenamiento de embeddings y contexto histórico (RAG) para mejorar la toma de decisiones del agente.
*   **Google Sheets:** Destino final de los datos tabulados (Lead Score, Problemas Detectados, Servicio Potencial, Mensaje de Prospección y datos de contacto) para su fácil gestión por parte del equipo de ventas.

---

## 🧠 Características Principales

*   **Auditoría Multidimensional:** Evalúa CRO, UX/UI, SEO On-page y adecuación al rubro del negocio.
*   **Puntuación Inteligente (Lead Scoring):** Clasifica los leads no por lo "mala" que sea la web, sino por el tamaño de la oportunidad comercial.
*   **Manejo de Errores y Límites:** Implementación de nodos `Wait` y configuración de reintentos (`Retry On Fail`) para respetar los rate limits de las APIs gratuitas.
*   **Búsqueda de Rescate:** Si un negocio no tiene web registrada en Google Maps, el sistema realiza una segunda búsqueda orgánica para intentar localizar su Instagram o sitio oculto.
*   **Prevención de Alucinaciones:** Prompt estrictamente diseñado para forzar respuestas en formato JSON puro y basar las auditorías únicamente en evidencia comprobable del texto de la web.

---

## 🛠️ Cómo utilizar este repositorio

1.  Descarga el archivo `Extracción de Leads.json` incluido en este repositorio.
2.  Importa el archivo directamente en tu instancia de n8n.
3.  Configura tus propias credenciales en los nodos correspondientes (Serper API, tu proveedor de LLM y Google Sheets).
4.  Ajusta el nodo inicial de búsqueda con el rubro y ciudad que desees prospectar.

# SHOPMIND EXPERIENCE 5.0 · Guía docente

Simulador para estudiantes de **E-Shopper y Metaverso**. Los estudiantes aprenden **cómo un eCommerce convierte comportamiento en recomendaciones**, acompañados por el **Prof. HARVEY IA** (tutor virtual con IA del profesor Harvey Sanabria). Hay cinco misiones de 20 puntos cada una (100 en total) y se aprueba con **80 %**.

## El recorrido: un rol nuevo en cada misión

| # | Misión | Rol del estudiante | Qué comprende |
|---|---|---|---|
| 1 | Descifra los datos | Analista de datos junior | Actividad ≠ conversión; leer gráficos |
| 2 | Domina el ranking Elo | Analista de algoritmos | Probabilidad esperada, ajuste Elo y por qué un ranking global no es personalización |
| 3 | Conviértete en eShopper | Cliente incógnito | Cómo sus acciones reordenan su TOP 5; personalizado vs. popularidad |
| 4 | Diseña el algoritmo | Ingeniero(a) de recomendación | Equilibrar relevancia, presupuesto y descubrimiento con pesos |
| 5 | Decide como gerente | Gerente comercial | Decisiones con evidencia y ética de datos |

## Novedades de la versión 5

- **Explicación del porqué en todo el simulador.**
  - Cada producto recomendado muestra una barra con lo que aporta el interés, el presupuesto y la popularidad, y un botón **«¿Por qué?»**.
  - Cada duelo Elo muestra la probabilidad esperada y el cálculo exacto del ajuste.
- **Prof. HARVEY IA integrado en el recorrido**, no solo como chat lateral:
  - «Analizar mi error con el Prof. HARVEY IA» después de cada respuesta. El intento ya queda cerrado, así que el Prof. HARVEY IA puede explicarla a fondo.
  - «¿Cómo leo este gráfico?», «Analizar el cambio» y «Pedir una pista» en los momentos clave.
  - **Retroalimentación formativa de las reflexiones y argumentos.** No pone nota y el estudiante puede mejorar su texto y volver a pedirla.
- **Reto de la misión 4 rediseñado.** Valentina, presupuesto de $150.000, tiene que cumplir tres objetivos a la vez. Los pesos iniciales no lo cumplen y solo cerca del 6 % de las combinaciones lo logra.
  - Puntaje del reto: 10 pts en máximo 3 evaluaciones, 7 pts en la 4.ª o 5.ª y 5 pts después.
  - Antes, los pesos iniciales ya ganaban el reto sin hacer nada.
- **Conceptos clave y rol** al inicio de cada misión.
- **Protección de la calificación:**
  - Las respuestas correctas ya no están en texto plano en el HTML.
  - El registro lleva un sello: si alguien edita su puntaje desde la consola del navegador, el reporte muestra «⚠ El registro fue modificado».
  - El reporte incluye el número de intento, la respuesta elegida en cada pregunta, los pesos con que se logró el reto y cuántas retroalimentaciones se pidieron.
- **Proxy mejorado:** límite de uso por estudiante (antes Render agrupaba a todo el curso en una sola IP), modos de revisión y retroalimentación, y una guía pedagógica por misión.

## Uso sin IA

Abre `index.html` en Chrome o Edge. Todo funciona sin internet y el Prof. HARVEY IA da **pistas locales**, que no son respuestas de IA.

## Conectar el Prof. HARVEY IA a OpenAI en Render (paso a paso)

> ⚠ **Nunca pegues la API key en `index.html`, en GitHub ni en `.env.example`.** Solo va en Render.

1. **Crea una clave nueva** en platform.openai.com → *API keys*. En **Billing → Limits** pon un **límite de gasto mensual**, por ejemplo USD 10.
2. **Sube la carpeta `api/` a un repositorio de GitHub** (puede ser privado). El `.gitignore` ya excluye el archivo `.env`.
3. En **render.com** → *New* → **Web Service** → conecta ese repositorio.
   - *Runtime*: Node · *Build command*: `npm install` · *Start command*: `npm start`
   - Si `api/` está dentro de un repositorio más grande, pon *Root Directory* = `api`.
4. En **Environment** agrega:
   - `OPENAI_API_KEY` = tu clave nueva
   - `ALLOWED_ORIGINS` = el dominio de tu página, por ejemplo `https://tu-usuario.github.io` (sin barra al final)
   - Opcionales: `OPENAI_MODEL` (por defecto `gpt-4.1-mini`), `MAX_HOURLY_PER_IP` (40) y `MAX_DAILY_REQUESTS` (1500)
5. Abre `https://TU-SERVICIO.onrender.com/health`. Debe responder `"apiConfigured": true`.
6. En `index.html` busca `const NEXO_API_URL = '';` y escribe dentro de las comillas `https://TU-SERVICIO.onrender.com/api/tutor`.
7. Publica `index.html` en GitHub Pages y haz una pregunta al Prof. HARVEY IA.

**Plan gratuito de Render:** el servicio «se duerme» tras 15 minutos sin uso. La primera pregunta puede tardar ~40 s y el Prof. HARVEY IA lo indica con «Tutor IA despertando». **Abre la página unos minutos antes de la clase** para despertarlo.

**Costo estimado:** con `gpt-4.1-mini`, un curso de 40 estudiantes con ~20 consultas cada uno suele costar menos de 1 USD. Verifícalo en tu panel de uso.

## Evaluación

- Cada misión aporta hasta 20 puntos. Solo se califica el **primer intento** de cada pregunta.
- **El Prof. HARVEY IA nunca cambia puntajes.** Las reflexiones y argumentos no se califican automáticamente: quedan en el reporte para tu revisión, junto con la retroalimentación que recibió el estudiante.
- «Volver a intentar» borra las respuestas y aumenta el **número de intento** que aparece en el reporte. Tú decides si aceptas intentos adicionales.

### Límites honestos de la protección

El simulador funciona completo en el navegador, sin servidor de calificación. Eso implica tres cosas:
- Un estudiante sin conocimientos técnicos **no puede** ver las respuestas con «Ver código fuente» ni editar su nota sin que se note.
- Alguien con conocimientos de programación avanzados podría, con esfuerzo, descifrar la protección o borrar los datos del navegador para empezar como «intento 1».
- La constancia es **pedagógica**, no una certificación verificada.

**Recomendación:** pide el **PDF del reporte** como entrega y revisa el número de intento, la integridad y las reflexiones. Si necesitas una garantía total, el siguiente paso es calificar en el servidor de Render.

## Archivos

- `index.html`: el simulador. Los datos están incorporados y la carpeta `datos/` solo sirve de referencia.
- `api/`: el proxy del Prof. HARVEY IA para Render. **No** publiques `api/.env`.
- `../DOCENTE_privado/clave_respuestas.json`: la **clave de respuestas legible**, solo para ti. **No la publiques.**
- `../SHOPMIND_V4_respaldo_original/`: copia de la versión 4. Contiene una API key comprometida y las respuestas en texto plano, así que **no la publiques**.

## Pruebas recomendadas antes de clase

- Haz el recorrido completo con respuestas correctas e incorrectas y genera el PDF.
- Misión 4: confirma que 50/30/20 **no** cumple el reto y prueba tu propia solución.
- Abre la página en un celular (375 px) y abre y cierra el chat.
- Con la API conectada: pide una pista, usa «Analizar mi error» y pide retroalimentación de una reflexión.

**Privacidad:** informa a los estudiantes que, si el Prof. HARVEY IA está conectado, sus preguntas y reflexiones se procesan mediante OpenAI. No envía nombres. Pídeles que no escriban datos personales en el chat.

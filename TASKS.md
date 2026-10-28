# TASKS — Rumbo

Hazlas en orden, en la rama `claude/rumbo-noche`. Al terminar cada una: `npm run build` y `npm run test` en verde, marca `[x]`, commit y push.
Si una tarea se bloquea, haz un fallback, anótalo en `NOTES.md` y sigue con la siguiente.

## T01 · Base del proyecto
- [ ] Lee `CLAUDE.md`, `docs/PRD.md` y este archivo completos antes de escribir código.
- [ ] Instala dependencias. Agrega Vitest con el script `npm run test` si no existe.
- [ ] Crea `NOTES.md` (secciones: Decisiones, Supuestos, Pendientes para el equipo) y `.env.example` con `VITE_N8N_WEBHOOK_URL` y `VITE_MOJOAUTH_API_KEY`.
- **Aceptación:** `npm run build` y `npm run test` pasan; `.env` está en `.gitignore`.

## T02 · Datos
- [ ] `questions.ts`: las 20 preguntas con el texto exacto del PRD, su etapa y el tipo RIASEC de cada opción.
- [ ] `careers.json` con 20 carreras que cubran los 6 tipos: Medicina, Enfermería, Psicología, Pedagogía, Biotecnología, Ciencia de Datos, Ingeniería en Computación, Actuaría, Ingeniería Mecatrónica, Ingeniería Civil, Arquitectura, Gastronomía, Diseño Gráfico, Comunicación y Medios Digitales, Derecho, Relaciones Internacionales, Administración de Empresas, Mercadotecnia, Finanzas, Contaduría.
- [ ] Por carrera: perfil RIASEC de 6 valores, `matematicas` (`alto | medio | bajo`), 2–3 ramas con trabajos y `valores` (`dinero | impacto | libertad | estabilidad`), salarios (o `null`) y 3 universidades (una pública, una privada, una internacional) con becas.
- [ ] Perfiles RIASEC: si existe `data/onet/`, calcúlalos desde ahí; si no, estímalos con tu conocimiento de O\*NET y marca `"fuente": "aproximado"`.
- [ ] Un test valida el esquema de todas las carreras.
- **Aceptación:** el test de esquema pasa; ningún costo, salario o beca está inventado (lo dudoso va en `null` con `"verificar": true`).

## T03 · Scoring
- [ ] Funciones puras en `scoring.ts` con las fórmulas 1–8 de `CLAUDE.md`.
- [ ] Al menos 10 tests: perfil claramente I da carrera dominante I en el top 3; perfil plano da explorador; todo "Nada" da explorador sin dividir entre cero; Pearson con desviación 0 da `r = 0`; ajuste −5 y −10 de matemáticas; mezcla 70/30 con TikTok; desempate del código Holland.
- **Aceptación:** todos los tests pasan; el % nunca sale de 0–100.

## T04 · Recomendación
- [ ] `recommend.ts`: top 3, perfil explorador, orden de ramas por valores, desempate a menos de 3 puntos, filtros de las preguntas 18–20.
- [ ] Universidad sueño, ideal y segura para la carrera #1, respetando presupuesto, ubicación e inglés. Si un filtro deja 0 universidades, relájalo y muestra una nota ("No encontramos opciones con ese presupuesto; estas son las más cercanas").
- **Aceptación:** tests de cada filtro y del caso sin resultados.

## T05 · TikTok
- [ ] `parse.ts` tolerante: extrae búsquedas, hashtags favoritos y links con like buscando llaves de forma recursiva.
- [ ] `src/demo/tiktok-export.json`: export de ejemplo realista y su clasificación RIASEC precalculada.
- [ ] Tests con el ejemplo, con un JSON vacío y con un archivo que no es JSON.
- **Aceptación:** ningún archivo hace tronar la app; si no hay señales, sigue sin TikTok y lo avisa.

## T06 · Pipeline y modo demo
- [ ] `pipeline.ts`: n8n con timeout de 5 s → pipeline local → caché.
- [ ] Perfil demo (persona ficticia de 17 años en CDMX) cuyo top 3 sea coherente y atractivo para el pitch.
- [ ] `?demo=1` precarga las respuestas y avanza solo.
- [ ] Test: el resultado en caché es idéntico al que calcula el pipeline local con el perfil demo.
- **Aceptación:** sin internet y sin `.env`, el flujo completo funciona.

## T07 · Interfaz
- [ ] Landing ("Descubre tu ruta"), login, consentimiento del tutor y aviso de privacidad.
- [ ] Cuestionario: una pregunta por pantalla, avance automático, botón para regresar, barra de progreso con 3 etapas.
- [ ] Subida opcional de TikTok con tutorial de 3 pasos para descargar el export.
- [ ] Pantalla de carga de 8 a 12 s con 3 pasos.
- [ ] Resultado: perfil en una línea, top 3 con % y desglose, nota de matemáticas si aplica, universidades con costo y becas (link oficial), escenarios a 20 años en 3 tarjetas, audio, botón de PDF y botón de contacto simulado.
- [ ] Aplica completa la sección "Diseño" de `CLAUDE.md`: paleta, tipografía, ruta trazada, hexágono RIASEC y número de % animado.
- [ ] Capturas a 375 px y 1280 px de cada pantalla en `docs/capturas/`, revisadas y corregidas.
- **Aceptación:** el flujo se ve pulido a 375 px y en escritorio, cumple la sección Diseño y no hay errores en consola.

## T08 · Textos
- [ ] `explain.ts`: por qué hace match (cita 1 respuesta y 1 señal de TikTok si existe), ramas y escenarios, por plantilla y determinista.
- [ ] `prompts.ts`: prompts de Gemma para clasificar TikTok, explicar el match y escribir el guion del audio (máximo 40 palabras, segunda persona, desde 2045). Las cifras siempre vienen del catálogo.
- **Aceptación:** sin Gemma, cada carrera del catálogo tiene textos completos y naturales.

## T09 · Audio
- [ ] Reproductor que arranca con el toque a "Ver mi resultado"; fallback a `speechSynthesis` en `es-MX` si no existe `public/demo/yo-2045.mp3`.
- [ ] Guarda en `src/demo/` el guion del perfil demo para generarlo después en ElevenLabs.
- **Aceptación:** con y sin mp3 se escucha algo, sin errores.

## T10 · PDF
- [ ] PDF "Mi Rumbo" generado en el navegador con las secciones 1–7 del PRD; secciones 8 y 10 si hay tiempo.
- [ ] QR a `window.location.origin + "/demo/yo-2045.mp3"`.
- **Aceptación:** se descarga sin errores con el perfil demo y con un perfil explorador.

## T11 · n8n
- [ ] `n8n/rumbo-workflow.json` importable: Webhook → Code (mismo scoring) → Gemma 4 → títulos de TikTok → Firecrawl → ElevenLabs → Respond. Credenciales como placeholders.
- [ ] `docs/n8n-setup.md`: cómo importarlo, qué credenciales poner y cómo conectar la URL al front.
- **Aceptación:** el JSON es válido y la respuesta del webhook tiene el mismo formato que espera `pipeline.ts`.

## T12 · Revisión final
- [ ] Recorre el flujo completo con `?demo=1` y con respuestas nuevas; si hay Playwright disponible, agrega una prueba de humo.
- [ ] Revisa cada pantalla contra el PRD: preguntas exactas, textos en español sin errores, nada en inglés, nada que diga "lorem" o "TODO" visible.
- [ ] `README.md` (qué es, cómo correrlo, herramientas, atribución de O\*NET bajo CC BY 4.0) y `LICENSE` MIT.
- [ ] `NOTES.md` final con "Pendientes para el equipo en la mañana", en orden de prioridad.
- [ ] Abre un pull request de `claude/rumbo-noche` a `main` con un resumen de lo hecho. No lo fusiones: lo revisa el equipo. Si desde la sesión no puedes abrirlo, anótalo en `NOTES.md`: el equipo lo abre con el botón de la sesión.
- **Aceptación:** build, tests y lint en verde; el demo corre de punta a punta sin internet.

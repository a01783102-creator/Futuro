# Rumbo — contexto para Claude

## Qué es
Rumbo ayuda a alumnos de prepa en México a elegir carrera. El alumno contesta 20 preguntas de opción múltiple, opcionalmente sube su export de TikTok, y recibe su top 3 de carreras con % de match, universidades, becas, escenarios a 20 años, un PDF y un audio de su "yo del 2045".

Es el proyecto del equipo para Hacktoberfest México 2026. Se presenta con un **demo en vivo de 60 segundos**.

- **Producto:** `docs/PRD.md` es la fuente de verdad (preguntas exactas, fórmulas, pantallas, PDF, guion del demo).
- **Técnica:** este archivo. Si chocan, el PRD manda en producto y este archivo en técnica.
- **Plan de trabajo:** `TASKS.md`, en orden.

## Prioridad absoluta
Un demo que corre de punta a punta **sin errores, aunque no haya internet ni API keys**.
Robusto > bonito > completo. Nada en pantalla puede romperse frente al jurado.

## Stack (no cambiar)
El repo lo creó Lovable y está sincronizado con Lovable en la rama `main`: Vite + React + TypeScript + Tailwind + shadcn/ui.
- No cambies de framework ni de gestor de paquetes. No renombres ni muevas archivos de configuración ni `src/components/ui/`.
- Agrega dependencias solo si son necesarias. Deben funcionar 100% en el navegador.
- Interfaz en español de México, tono cercano de chavo de prepa, tuteo. Mobile first: todo debe verse bien a 375 px de ancho.

## Reglas de trabajo (vas a trabajar solo toda la noche)
1. Sigue `TASKS.md` en orden. Marca una tarea `[x]` solo cuando se cumple su criterio de aceptación.
2. Trabaja en la rama `claude/rumbo-noche`, nunca directo en `main` (Lovable sincroniza `main`). Después de cada tarea: `npm run build` y `npm run test` deben pasar (y `npm run lint` si existe). Luego commit (`T03: scoring RIASEC`) y push a esa rama.
3. **No pidas confirmación.** Toma la decisión más razonable y anótala en `NOTES.md` (decisiones, supuestos, pendientes del equipo).
4. Si algo te bloquea (falta una key, la red está bloqueada, una librería falla): haz un fallback, anótalo en `NOTES.md` y sigue con lo siguiente. Nunca te quedes detenido.
5. **No inventes datos.** Universidades, becas, costos y salarios: solo los que conozcas con alta confianza y con URL oficial. Lo que no, va en `null` con `"verificar": true`, y la interfaz muestra "Por confirmar". Las cifras nunca las genera un modelo.
6. **Nunca subas secretos.** Crea `.env.example`; confirma que `.env` está en `.gitignore`.
7. Antes de terminar, haz la revisión final de T12 completa.

## Diseño (esto decide si ganamos)
El jurado juzga en 60 segundos y en una pantalla. Tiene que verse como un producto de verdad, no como una plantilla de shadcn.

**Concepto: "tu ruta, trazada".** Una línea de ruta conecta toda la experiencia, del presente (prepa, 2026) al futuro (2045).

- **Firma visual:** la barra de progreso del cuestionario es un camino que se va trazando con 3 paradas (las 3 etapas). En el resultado, la ruta a 2045 es una línea que se dibuja con hitos: prepa → universidad → primer trabajo → 2045.
- **Paleta** (como variables de tema de shadcn en `index.css`):
  - Noche `#0E1424`: fondo del landing y de la pantalla de resultado.
  - Papel `#FAF7F2`: fondo claro del cuestionario.
  - Amanecer `#FF6B3D`: el único acento fuerte (botones principales y la ruta).
  - Verde agua `#2BB3A3`: match alto y estados de éxito.
  - Texto `#0E1424` sobre claro y `#F4F1EA` sobre noche.
  - Tipos RIASEC (solo en la gráfica): R `#D9633A`, I `#3E6FD8`, A `#B34FC4`, S `#2BA58F`, E `#E3A72F`, C `#5B6B82`.
- **Tipografía:** Bricolage Grotesque (títulos, 700–800) y DM Sans (texto), instaladas con Fontsource por npm para que funcionen sin internet. Si un paquete no existe, usa la fuente del sistema y anótalo en `NOTES.md`.
- **Pantalla de resultado (la estrella del demo):** fondo noche; top 3 en tarjetas grandes; el % como número gigante que cuenta de 0 a su valor; hexágono RIASEC en SVG propio (sin librerías pesadas); la ruta a 2045 dibujándose.
- **Movimiento:** transiciones de 150 a 300 ms; la ruta se dibuja con `stroke-dashoffset`. Respeta `prefers-reduced-motion`.
- **Íconos:** `lucide-react`. Nada de emojis como íconos.
- **Accesibilidad:** contraste AA, botones de al menos 44 px de alto, foco visible, texto de al menos 14 px en móvil.
- **Evita:** degradados morados genéricos, sombras pesadas, más de un color de acento, tarjetas idénticas sin jerarquía, texto de relleno.
- **Revisión visual obligatoria:** si puedes instalar Playwright, toma capturas de cada pantalla a 375 px y 1280 px, míralas y corrige hasta que se vea pulido. Guárdalas en `docs/capturas/` para que el equipo las revise.

## Arquitectura
Las llaves de Gemma, Firecrawl y ElevenLabs viven **solo en n8n**, nunca en el navegador (las variables `VITE_` son públicas).

La URL del webhook de n8n y la llave pública de MojoAuth van en `src/config.ts`, leyendo `VITE_N8N_WEBHOOK_URL` y `VITE_MOJOAUTH_API_KEY` si existen y con valor vacío por defecto. Así el equipo las puede pegar mañana desde Lovable editando un solo archivo.

```
Front (React) ──POST respuestas + señales de TikTok──▶ n8n webhook
      │                                                 (Gemma 4, Firecrawl, ElevenLabs)
      │◀──────────── ruta + textos + URL del audio ──────────┘
      │
      ├─ sin URL de n8n en config, falla o tarda > 5 s ─▶ pipeline local (mismo scoring, textos por plantilla)
      └─ si el pipeline local falla ─────────────────────────▶ resultado en caché de src/demo/
```

Estructura sugerida:
- `src/lib/riasec/questions.ts` — las 20 preguntas con el texto exacto del PRD.
- `src/lib/riasec/scoring.ts` — funciones puras y testeadas (fórmulas abajo).
- `src/lib/recommend.ts` — filtros, orden de ramas, desempates, perfil explorador.
- `src/lib/tiktok/parse.ts` — parser del export.
- `src/lib/explain.ts` — textos por plantilla (fallback determinista).
- `src/lib/prompts.ts` — prompts de Gemma que también usa n8n.
- `src/lib/pipeline.ts` — n8n → local → caché.
- `src/data/careers.json` — catálogo curado.
- `src/demo/` — perfil demo: respuestas, export de TikTok de ejemplo, resultado esperado.
- `n8n/rumbo-workflow.json` — workflow importable.

## Fórmulas (no las cambies)
Tipos en orden fijo: `R, I, A, S, E, C`.
1. **Etapa 1 (preguntas 1–12):** Nada 0, Poco 1, Me late 2, Me encanta 3. Cada pregunta suma a su tipo (mapa en el PRD).
2. **Etapa 2 (13–15):** la opción elegida suma 2 a su tipo. Puntaje bruto por tipo: 0 a 12.
3. **Perfil explorador:** si `max − min < 3`, el resultado es "perfil explorador": 3 carreras cuyo tipo dominante sea distinto (la de mayor match en cada uno), con la etiqueta "Para explorar" en vez de %.
4. **Distribución:** `q = bruto / suma(bruto)`. Si la suma es 0, perfil explorador.
5. **TikTok (opcional):** `k` = distribución de 6 tipos que suma 1. `p = 0.7·q + 0.3·k`; sin TikTok, `p = q`.
6. **Código Holland:** 3 tipos más altos de `p`. Empates: gana el que más se eligió en la etapa 2; si sigue empatado, el orden fijo.
7. **Match:** `r = correlación de Pearson(p, perfil_carrera)`; si alguna desviación estándar es 0, `r = 0`. `match = round(50 + 50·r)`, acotado a 0–100.
8. **Ajuste por matemáticas (pregunta 16):** si la carrera es `"alto"`: opción 3 ("Me cuestan, pero le echo ganas") −5; opción 4 ("Me cuestan mucho") −10. Se muestra en el desglose junto con una nota honesta.
9. **Valores (17):** no cambia el %. Ordena las ramas (las que incluyen el valor elegido van primero) y desempata carreras a menos de 3 puntos de distancia.
10. **Filtros (18–20):** solo eligen universidades, no cambian el %. Lo detalla el PRD.

## TikTok
El export de TikTok trae links y fechas, no descripciones. Las señales con texto son: historial de búsquedas, hashtags favoritos y títulos de videos con like.
- El parser debe ser **tolerante**: la estructura cambia según la versión del export. Busca las llaves de forma recursiva y nunca truena con un archivo raro; si no encuentra nada, sigue sin TikTok y lo avisa con amabilidad.
- En modo real, n8n obtiene los títulos de hasta 50 links con like y Gemma clasifica todo. En modo local, se usa la clasificación precalculada del perfil demo.
- El archivo se procesa en memoria y no se guarda.

## Demo
- `?demo=1` en la URL precarga las respuestas del perfil demo y avanza solo.
- La pantalla de carga dura de 8 a 12 s con 3 pasos visibles, aunque el resultado ya esté listo.
- El resultado en caché debe ser **exactamente** lo que calcula el pipeline con el perfil demo. Un test lo verifica.
- Audio: `public/demo/yo-2045.mp3`. Si no existe, usa `speechSynthesis` con voz `es-MX`. Los navegadores bloquean el autoplay sin interacción, así que el audio arranca con el toque al botón "Ver mi resultado".
- Login: MojoAuth real si existe `VITE_MOJOAUTH_API_KEY`; si no, un login de demostración.
- El botón "Quiero que me contacten" solo muestra una confirmación; no envía nada.

## Diferencias con el PRD ya resueltas (sigue esto)
- **Audio:** el PRD dice "arranca solo", pero los navegadores bloquean el autoplay; arranca con el toque a "Ver mi resultado".
- **Salarios del catálogo:** el PRD muestra `0` como ejemplo; usa `null` con `"verificar": true` cuando no haya dato confiable.
- **Futuro de 10, 20 o 50 preguntas:** no se construye esta noche. Solo deja las preguntas 1 a 6 cubriendo los 6 tipos, como ya están.
- **Validación con nuestra historia y la encuesta:** la hace el equipo, no tú.

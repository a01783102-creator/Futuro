# Rumbo — guía del equipo

## Cómo está armado
- **Lovable** es donde vive la app y donde cualquiera del equipo la edita visualmente.
- **GitHub** guarda el código. Lovable y GitHub se sincronizan solos en la rama `main`.
- **Claude Code en la nube** (claude.ai/code) programa sobre GitHub mientras dormimos, en la rama `claude/rumbo-noche`. Cuando fusionamos su pull request, los cambios aparecen en Lovable.

## Esta noche (Barroso, unos 20 minutos)
1. **Lovable:** crea un proyecto nuevo y pega el texto de `PROMPT_LOVABLE.md`.
2. **Conecta GitHub en Lovable** (botón de GitHub del proyecto). Lovable crea el repo.
3. **Sube a la raíz del repo** desde github.com ("Add file → Upload files"): `CLAUDE.md`, `TASKS.md`, `GUIA_EQUIPO.md` y la carpeta `docs` con `PRD.md`.
4. **Crea el archivo de permisos** en github.com: "Add file → Create new file", nombre `.claude/settings.json`, y pega el contenido del archivo `.claude/settings.json` del zip. Esto evita que Claude se detenga a pedir permiso para correr `npm` y `git`.
5. **Abre claude.ai/code**, conecta GitHub (autoriza la Claude GitHub App en el repo) y elige el repo.
6. **Configuración de la sesión:**
   - Entorno: **Default**, con acceso a red **Trusted** (deja instalar paquetes de npm).
   - Modo de permisos: **Auto**. Si no aparece, usa **Accept edits**; el archivo de permisos cubre el resto.
   - Modelo: el más capaz que te deje elegir.
7. **Pega el texto de `PROMPT_INICIO.md`** y envía. Revisa 5 minutos que arranque bien (que lea los archivos y cree la rama) y vete a dormir.

## Mañana temprano
1. Abre la sesión en claude.ai/code (también desde el celular) y lee `NOTES.md` en la rama `claude/rumbo-noche`.
2. Si no terminó, escríbele: "Sigue con TASKS.md desde donde te quedaste".
3. Revisa las capturas en `docs/capturas/` y prueba el demo.
4. Fusiona el pull request a `main` en GitHub. En un minuto aparece en Lovable.

## Mañana, ya con todo el equipo
Cada quien toma una parte:

| Quién | Qué | Dónde |
|---|---|---|
| 1 | Pulir diseño y textos | Lovable (esto también cuenta para el reto de Lovable) |
| 2 | Importar `n8n/rumbo-workflow.json`, poner llaves de Gemma, Firecrawl y ElevenLabs, y pegar la URL del webhook | n8n, y pegar la URL en `src/config.ts` desde Lovable |
| 3 | Generar el audio del yo del 2045 con el guion de `src/demo/`, subirlo como `public/demo/yo-2045.mp3`, poner la llave de MojoAuth, revisar los datos "Por confirmar" | ElevenLabs, MojoAuth, Lovable |

Todos: escribir su historia de cómo eligieron carrera, hacer la mini encuesta en el evento, grabar el video de respaldo y ensayar el guion 3 veces.

## Reglas para no pisarnos
- Mientras Claude trabaja de noche, nadie edita en Lovable.
- Mañana, una sola persona edita en Lovable a la vez, o cada quien en una parte distinta de la app.
- Las llaves secretas (Gemma, Firecrawl, ElevenLabs) solo van en n8n, nunca en el código. La URL del webhook y la llave pública de MojoAuth sí van en `src/config.ts`.

## Compartir con el equipo
- **Lovable:** invítalos al proyecto o al workspace de Lovable.
- **GitHub:** agrégalos como colaboradores del repo (Settings → Collaborators).
- **PRD:** el documento de Claude se comparte con su botón de compartir.

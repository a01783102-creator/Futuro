# Rumbo · PRD Hacktoberfest México 2026

## Resumen

**Rumbo** le da a cada alumno de prepa su top 3 de carreras, la universidad y la beca para llegar, y un audio de su yo del 2045, en unos 5 minutos.

**Tagline:** No te decimos qué estudiar. Te enseñamos quién puedes llegar a ser.

**El problema.** Tres de cada 10 estudiantes que entran a licenciatura en México dejan la carrera durante el primer año, en públicas y privadas, según la SEP ([El Cronista](https://www.cronista.com/mexico/actualidad-mx/alerta-en-la-sep-expertos-advierten-que-el-sistema-educativo-esta-en-problemas-y-revelan-las-razones-que-podrian-hundir-la-educacion/)). Entre 30% y 40% de los jóvenes se equivocan al elegir por presión familiar ([Expansión](https://expansion.mx/carrera/2019/08/06/test-es-momento-de-cambiar-de-carrera)). Los tests vocacionales gratis dicen "eres social" y ahí se quedan.

**La solución.** El alumno contesta 20 preguntas de opción múltiple y, si quiere, sube su export de TikTok. Rumbo calcula su perfil con el modelo RIASEC, lo cruza con datos oficiales de ocupaciones (O\*NET) y le entrega una ruta completa: carrera, universidad, país, becas, salarios y trayectoria a 20 años, en pantalla y en PDF.

Nombres alternativos si el equipo prefiere otro: **YoFuturo**, **Brújula**, **Trayecto**.

## Usuario y propuesta de valor

El usuario es el alumno de prepa (15 a 18 años) y es gratis para él; quien paga es la universidad, solo cuando el alumno decide contactarla.

| Actor | Qué necesita | Qué le da Rumbo |
| --- | --- | --- |
| Alumno de prepa | Saber qué estudiar sin adivinar ni seguir a sus amigos | Top 3 carreras explicadas con sus propios gustos, y una ruta concreta para llegar |
| Papá, mamá o tutor | Saber cuánto cuesta y si hay beca | Costo real, opciones públicas y privadas, becas con link oficial |
| Universidad | Alumnos que sí encajan con su carrera y no desertan | Solicitudes de alumnos con match alto que pidieron ser contactados |

**Por qué Rumbo y no el test gratis del Tec, la UNAM o 16Personalities:**

1. **Intereses reales, no solo declarados.** El export de TikTok muestra lo que el alumno de verdad consume, no lo que cree que debe contestar.
2. **Un portafolio, no una etiqueta.** Tres carreras, cada una con sus ramas y los trabajos posibles en cada rama, justificadas con evidencia del propio alumno.
3. **Ruta accionable.** Universidad sueño, ideal y segura; becas reales; costo según su presupuesto.
4. **Proyección a 20 años.** Escenarios de trayectoria y salario, cerrados con el audio de su yo del 2045.
5. **Neutral.** El match sale de datos oficiales; ninguna universidad paga por aparecer.

**Validación: el problema lo vivimos nosotros.** Los tres del equipo elegimos carrera sin información suficiente. Esa historia abre el pitch y se respalda con dos pruebas rápidas que se pueden hacer en el mismo hackathon.

- [ ] **Nuestra historia:** cada uno escribe en 2 líneas cómo eligió su carrera y qué le habría servido saber antes. La mejor frase va al pitch.
- [ ] **Mini encuesta en el hackathon** (mañana temprano, 10 minutos): preguntar a 10 asistentes "¿Elegiste tu carrera con buena información? Sí / Más o menos / No". Da un dato propio: "X de 10 personas en este hackathon eligieron a ciegas".
- [ ] **Probarlo con nosotros:** los tres contestamos las 20 preguntas. Si el top 3 tiene sentido con lo que hoy sabemos de nosotros, se dice en el pitch: "lo probamos con nosotros y le atinó".

## Modelo de negocio

Rumbo cobra a las universidades por **solicitud confirmada**: una tarifa fija cada vez que un alumno, después de ver su ruta, toca "Quiero que esta universidad me contacte" y su tutor lo aprueba.

Es un modelo de pago por lead (PPL), pero con el alumno en control. Para la universidad vale más que un lead normal: el alumno ya pasó por el test, tiene match alto con su carrera y él mismo pidió el contacto.

**Reglas de neutralidad (lo que blinda el modelo ante el jurado):**

1. **El match nunca depende de quién paga.** El ranking sale del perfil RIASEC, O\*NET y los filtros del alumno. Ninguna universidad puede pagar por subir.
2. **El alumno elige.** Nada se comparte hasta que él toca el botón de contacto, universidad por universidad.
3. **Solo se comparte lo mínimo.** Nombre, contacto, carrera de interés y % de match. **Nunca** sus respuestas completas ni sus datos de redes.
4. **Consentimiento del tutor** obligatorio para menores antes de cualquier contacto.

**Por qué es buen negocio:** las universidades ya gastan en captar alumnos, y un alumno que elige bien deserta menos. Rumbo les vende alumnos que encajan, no solo datos de contacto.

**Roadmap de ingresos (no entra en el demo):** licencia para prepas que quieran darle Rumbo a todos sus alumnos con un panel para el orientador.

## Experiencia de usuario y cuestionario

El alumno termina en unos 3 minutos, sin escribir nada: 20 preguntas de opción múltiple, una por pantalla, todas de un toque.

**Principios de UX**

- Una pregunta por pantalla, avance automático al tocar una opción, barra de progreso dividida en las 3 etapas ("Lo que te late", "Lo que eliges", "Tu contexto").
- Cero texto libre en el cuestionario.
- Subir TikTok es opcional y mejora el resultado; se ofrece después de la pregunta 20.
- Lenguaje de chavo de prepa, no de test psicológico.
- Mobile first: la mayoría lo va a abrir en el celular.

**Flujo**

1. Landing con botón "Descubre tu ruta".
2. Login sin contraseña (MojoAuth) y casilla de consentimiento del tutor.
3. Preguntas 1 a 15: intereses (RIASEC).
4. Preguntas 16 a 20: matemáticas, valores y contexto (dónde, presupuesto, inglés).
5. Opcional: subir export de TikTok, con un mini tutorial de 3 pasos para descargarlo.
6. Pantalla de carga con los pasos visibles.
7. Resultado en pantalla, botón "Descargar mi ruta en PDF" y botón "Quiero que me contacten" por universidad.

### Cuestionario estándar: 20 preguntas

Tres etapas, todas de un toque: 12 preguntas de "qué tanto te late", 3 de escoger una entre seis y 5 de aptitud, valores y contexto. Tiempo estimado: 3 minutos.

**Por qué este diseño**

- **Calificar actividades mide cada tipo por separado.** Con dos actividades por tipo sabemos qué tanto le gusta cada uno, no solo cuál gana. Es el mismo formato del O\*NET Interest Profiler, que pide calificar actividades.
- **Escoger una entre seis desempata.** Cuando dos tipos quedan parejos, estas preguntas obligan a decidir.
- **Actividades de la vida real, no materias.** Si te gusta o no una materia depende mucho del profe; armar una bici o vender algo no.
- **Sin sesgos.** Ninguna pregunta asume género ni nivel económico, y los profesionales de la pregunta 13 mezclan hombres y mujeres a propósito.
- **Orden alternado.** Los tipos se intercalan para que el alumno no adivine el patrón y conteste "lo correcto".
- **Anidado.** Las preguntas 1 a 6 cubren los 6 tipos una vez cada una; eso permite el modo rápido de 10 preguntas en el futuro sin rehacer nada (ver Alcance).

**Etapa 1 · Lo que te late (preguntas 1 a 12)**

Pregunta fija: "¿Qué tanto te late…?" con cuatro botones: Nada (0) · Poco (1) · Me late (2) · Me encanta (3). La letra del tipo nunca se le muestra al alumno.

1. Armar, reparar o mejorar algo con tus manos: una bici, un mueble, una compu. (R)
2. Explicarle un tema a un compañero hasta que por fin le entienda. (S)
3. Investigar por tu cuenta si algo que viste en internet es cierto. (I)
4. Organizar a tus amigos para un plan grande: un viaje, una fiesta, un torneo. (E)
5. Crear algo visual desde cero: un logo, un outfit, la decoración de un cuarto. (A)
6. Llevar el control de algo con detalle: tus gastos, un inventario, tus pendientes. (C)
7. Escuchar y apoyar a alguien que está pasando por un mal momento. (S)
8. Trabajar al aire libre o con herramientas y máquinas, aunque te ensucies. (R)
9. Vender algo o armar un negocito para ganar tu propio dinero. (E)
10. Quedarte horas con un problema difícil hasta resolverlo, solo por el gusto de entenderlo. (I)
11. Seguir un proceso paso a paso y que todo quede exacto, sin un error. (C)
12. Expresarte escribiendo, actuando, haciendo música o grabando videos. (A)

**Etapa 2 · Lo que eliges (preguntas 13 a 15)**

Escoge una de seis. La opción elegida suma 2 puntos a su tipo.

13. **Ganaste un concurso: pasas un día con un profesional. ¿Con quién te vas?**
    - Una ingeniera en una obra o en una planta de energía (R)
    - Un científico en su laboratorio (I)
    - Una directora de cine en un set de grabación (A)
    - Un psicólogo que trabaja con adolescentes (S)
    - La fundadora de una startup el día que cierra una inversión (E)
    - Un auditor revisando las cuentas de una empresa grande (C)
14. **En un proyecto en equipo, ¿qué parte agarras sin que te lo pidan?**
    - La parte práctica: armar, construir, que funcione (R)
    - Investigar y encontrar la información buena (I)
    - Que se vea increíble: el diseño y la presentación (A)
    - Que el equipo se lleve bien y nadie se quede atrás (S)
    - Liderar y presentar frente al grupo (E)
    - Llevar el calendario y revisar que todo se entregue a tiempo (C)
15. **Tienes 30 años y te va muy bien. ¿Qué es lo que más te enorgullece?**
    - Construí algo que la gente usa todos los días (R)
    - Descubrí algo que nadie había resuelto (I)
    - Creé algo que la gente recuerda (A)
    - Le cambié la vida a personas concretas (S)
    - Fundé mi propia empresa y la hice crecer (E)
    - Soy la persona en quien todos confían para que las cosas salgan perfectas (C)

**Etapa 3 · Tu contexto (preguntas 16 a 20)**

16. **¿Cómo te llevas con las matemáticas?** (aptitud)
    - Se me dan fácil y me gustan
    - Se me dan, pero no me emocionan
    - Me cuestan, pero le echo ganas
    - Me cuestan mucho
17. **¿Qué es lo que más te importa de tu futuro trabajo?** (valores)
    - Ganar bien
    - Ayudar a otros o tener impacto
    - Libertad para crear y decidir
    - Estabilidad y seguridad
18. **¿Dónde te gustaría estudiar?**
    - En mi ciudad
    - Me mudaría a otra ciudad de México
    - En el extranjero
    - Me da igual, quiero ver opciones
19. **¿Cuánto pueden pagar por semestre?**
    - Nada, busco universidad pública
    - Una privada accesible
    - Una privada de las más caras
    - Solo podría con beca
20. **¿Cuál es tu nivel de inglés?**
    - Básico
    - Intermedio
    - Avanzado

Los rangos en pesos de "accesible" y "de las más caras" los define el equipo en el catálogo.

## Metodología y lógica de matching

El match lo calcula código con datos oficiales, no la IA: Gemma 4 solo clasifica TikTok y explica el resultado. Así el resultado es rápido, repetible y defendible.

**Fundamento.** El cuestionario está inspirado en el modelo RIASEC de John Holland, uno de los más estudiados en orientación vocacional. El match usa la base pública de O\*NET (Departamento de Trabajo de EE. UU.), que da a cada ocupación un puntaje en los 6 tipos RIASEC. El cuestionario es una adaptación propia, no un instrumento validado; mide **intereses**, no aptitudes.

**Paso 1 · Perfil del cuestionario.** Por tipo: suma de sus 2 actividades de la etapa 1 (0 a 6) + 2 puntos por cada vez que se eligió en la etapa 2 (0 a 6). Resultado: 6 puntajes de 0 a 12, que se convierten a distribución (cada puntaje entre la suma de los seis).

**Perfil plano.** Si entre el tipo más alto y el más bajo hay menos de 3 puntos (por ejemplo, contestó "Me encanta" o "Nada" a todo), el resultado se presenta como **perfil explorador**: 3 carreras de tipos distintos para que explore, en vez de fingir una certeza que no hay.

**Paso 2 · Perfil de TikTok (opcional).** El alumno sube su export de TikTok (JSON). El export trae links y fechas de videos, no su descripción, así que se usan tres señales con texto: el historial de búsquedas, los hashtags favoritos y los títulos de hasta 50 videos con like (se obtienen por link en n8n). Gemma 4 clasifica ese texto en los 6 tipos RIASEC y devuelve una distribución en porcentaje, más 3 ejemplos concretos como evidencia ("ves mucho contenido de ciencia y experimentos"). Lo que no encaja en ningún tipo (memes, trends de baile sin más) se descarta.

**Paso 3 · Perfil final.** Con TikTok: 70% cuestionario + 30% TikTok, mezclando las dos distribuciones. Sin TikTok: 100% cuestionario. Código Holland = los 3 tipos más altos (por ejemplo, "IAS"); un empate lo rompe la etapa 2.

**Paso 4 · Match con carreras.** Cada carrera del catálogo está ligada a 2–4 ocupaciones de O\*NET; su perfil es el promedio de los 6 puntajes de interés de esas ocupaciones. La similitud es la **correlación** entre el perfil del alumno y el de la carrera (coseno con ambos perfiles centrados en su promedio). Va centrada porque con coseno simple casi todas las carreras salen arriba de 85% y el número no distingue nada; centrada compara qué tipos sobresalen. **% de match = 50 + 50 × correlación.** Se muestran las 3 más altas.

**Paso 5 · Ajuste por aptitud (pregunta 16).** Cada carrera tiene un nivel de matemáticas: alto, medio o bajo. En carreras de nivel alto: "Me cuestan, pero le echo ganas" resta 5 puntos y "Me cuestan mucho" resta 10. La carrera no desaparece: aparece una nota honesta ("Esta carrera tiene mucha matemática; tu plan incluye cómo reforzarla") y el ajuste se ve en el desglose. Así "gustos y aptitudes" es verdad, no solo un eslogan.

**Paso 6 · Filtros y orden (preguntas 17 a 20).**

| Pregunta | Qué hace |
| --- | --- |
| P17 · Valores | No cambia el %. Ordena las ramas de cada carrera ("ganar bien" pone primero las mejor pagadas), desempata carreras a menos de 3 puntos y da el tono del audio |
| P18 · Dónde estudiar | Universidades en su ciudad, en México o en el extranjero |
| P19 · Presupuesto | Públicas, privadas accesibles o caras; "solo con beca" pone las becas primero y solo muestra universidades con becas de 50% o más |
| P20 · Inglés | Universidades en el extranjero solo con inglés intermedio o avanzado; con básico se agrega "subir inglés" al plan de 90 días |

**Cómo se ve el % de match.** Desglose para el alumno: intereses que contestaste, intereses de tu TikTok y ajuste por matemáticas. Presupuesto y ubicación no bajan el %: cambian qué universidades aparecen.

**Paso 7 · Explicación y ruta.** Gemma 4 genera, por carrera: una línea de por qué hace match (citando una respuesta suya y un ejemplo de su TikTok), las ramas ordenadas por sus valores, los escenarios a 20 años (conservador, probable, optimista) y el guion de 15 segundos del yo del 2045. Gemma recibe salarios y universidades del catálogo y tiene prohibido inventar cifras.

Fuente a citar en la presentación: [O\*NET Resource Center](https://www.onetcenter.org/database.html).

## Resultado: pantalla y PDF

La pantalla muestra lo esencial en un vistazo; el PDF es lo que el alumno se lleva y le enseña a sus papás.

### Pantalla de resultado

- Perfil en una línea ("Eres investigador y creativo: te mueve entender cómo funcionan las cosas").
- Top 3 carreras, cada una con % de match y una línea de por qué.
- Por carrera: universidad sueño, ideal y segura, con costo y beca.
- Escenarios a 20 años en 3 tarjetas (conservador, probable, optimista).
- Reproductor del audio del yo del 2045 (arranca solo, máx. 15 s).
- Botones: "Descargar mi ruta en PDF" y "Quiero que me contacten" por universidad.

### PDF "Mi Rumbo"

| # | Sección | Contenido | Demo |
| --- | --- | --- | --- |
| 1 | Portada | Nombre, perfil en una línea, top 3 carreras | Sí |
| 2 | Por qué tú | Explicación del match con evidencia del test y de TikTok; gráfica RIASEC | Sí |
| 3 | Carrera #1 | Ramas de la carrera y trabajos por rama; 3 universidades: sueño, ideal y segura | Sí |
| 4 | Universidades | Por cada una: campus, ranking QS si aplica, costo por semestre, becas con link | Sí |
| 5 | Trabajos y salarios | Puestos posibles, salario inicial y a 10 y 20 años | Sí |
| 6 | Ruta a 20 años | Timeline: carrera, primer trabajo, crecimiento | Sí |
| 7 | Audio | QR al audio de tu yo del 2045 | Sí |
| 8 | Carreras #2 y #3 | Versión corta con 1 o 2 universidades cada una | Si sobra tiempo |
| 9 | Checklist de admisión | Examen, promedio mínimo, fechas límite | Roadmap |
| 10 | Plan de 90 días | 5 acciones concretas para empezar ya | Si sobra tiempo |

Todo el PDF se arma con una plantilla HTML y se convierte a PDF; los datos vienen del catálogo curado y de Gemma 4.

## Arquitectura y herramientas

El front en Lovable solo manda respuestas y recibe la ruta; un workflow de n8n hace todo lo demás en 6 pasos.

```
App en Lovable (login con MojoAuth)
   │  respuestas + señales de TikTok          ▲ ruta, PDF y audio
   ▼                                          │
Workflow de n8n (webhook)
   1. Clasifica TikTok (Gemma 4)
   2. Calcula el match (código: RIASEC + O*NET)   ← el corazón
   3. Busca becas (Firecrawl + catálogo)
   4. Explica la ruta (Gemma 4)
   5. Genera el audio (ElevenLabs)
   6. Arma el PDF
Cada paso guarda su resultado en caché para el modo demo.
```

El paso 2 es el corazón: el match lo calcula código sobre O\*NET, así que el resultado no depende de lo que "opine" la IA.

| Herramienta | Para qué | Reto |
| --- | --- | --- |
| Lovable | Front completo: landing, cuestionario, resultado | Best Built with Lovable |
| MojoAuth | Login sin contraseña y consentimiento del tutor | Best Auth with MojoAuth (10 ganadores) |
| n8n | Orquesta el flujo completo vía webhook | Best n8n Integration |
| Gemma 4 (por API) | Clasifica TikTok, explica el match, ramas, escenarios y guion del audio | Best Use of Gemma 4 |
| Firecrawl | Scrapea páginas oficiales de becas y universidades | Best Use of Firecrawl |
| ElevenLabs | Audio del yo del 2045 con voz genérica | Best Use of ElevenLabs |
| GitHub | Repo público con licencia MIT | Best Open-Source AI Project (MLH) |

No se usa Tavily: hace lo mismo que Firecrawl y no tiene reto propio.

## Qué es real y qué es simulado

El cálculo y la generación son reales; los datos de universidades, becas y salarios vienen de un catálogo curado a mano para 20 carreras.

| Componente | Estado en el demo | Cómo |
| --- | --- | --- |
| Login y consentimiento | Real | MojoAuth |
| Cuestionario y cálculo RIASEC | Real | Código en el front o en n8n |
| Clasificación de TikTok | Real | Gemma 4 sobre un JSON de ejemplo incluido en el proyecto |
| Match con O\*NET | Real | Código sobre el catálogo con perfiles RIASEC precalculados |
| Explicación, ramas y escenarios | Real | Gemma 4 |
| Universidades, costos, rankings, becas | Curado | JSON armado por el equipo con datos de páginas oficiales |
| Actualización de becas | Real para el perfil demo, en caché | Firecrawl scrapea 3–5 páginas de becas; el resultado se guarda |
| Salarios y trayectorias | Curado | Rangos por carrera en el catálogo |
| Audio del yo del 2045 | Real, con respaldo en caché | ElevenLabs; el audio del perfil demo ya generado |
| PDF | Real | Plantilla HTML a PDF |
| Botón de contacto a universidad | Simulado | Muestra confirmación; no envía nada |
| Instagram y Pinterest | Fuera | Roadmap |

### Catálogo curado (estructura por carrera)

```json
{
  "carrera": "Biotecnología",
  "onet_codes": ["19-1029.00", "19-4021.00"],
  "riasec": {"R": 0.45, "I": 0.95, "A": 0.25, "S": 0.30, "E": 0.20, "C": 0.40},
  "matematicas": "alto | medio | bajo",
  "ramas": [
    {"nombre": "Salud", "trabajos": ["Investigador clínico", "Desarrollo de fármacos"], "valores": ["impacto", "estabilidad"]},
    {"nombre": "Alimentos", "trabajos": ["Control de calidad", "I+D alimentario"], "valores": ["estabilidad", "dinero"]}
  ],
  "salario_mxn_mes": {"inicial": 0, "a_10_anios": 0, "a_20_anios": 0},
  "universidades": [
    {
      "nombre": "",
      "tipo": "publica | privada | internacional",
      "ciudad": "",
      "pais": "",
      "costo_semestre_mxn": 0,
      "ranking_qs": null,
      "ingles_requerido": "basico | intermedio | avanzado",
      "becas": [{"nombre": "", "cobertura": "50%", "link": ""}]
    }
  ]
}
```

Los valores en 0 o vacíos los llena el equipo con datos reales. Los perfiles RIASEC de cada carrera se calculan una vez desde O\*NET y se guardan en el catálogo; los códigos de ocupación del ejemplo son ilustrativos y hay que confirmarlos en O\*NET.

- [ ] Elegir las 20 carreras del catálogo
- [ ] Llenar 3 universidades por carrera (una pública, una privada, una internacional)
- [ ] Armar el perfil demo completo y dejar su resultado en caché

## Privacidad y datos de menores

Rumbo nunca se conecta a las cuentas del alumno: él mismo descarga su export de TikTok y lo sube, y el archivo se borra después del análisis.

- **Sin conexión directa a redes.** Las plataformas ya no permiten leer cuentas personales por API, así que usamos el export oficial que cualquier usuario puede descargar desde la app.
- **Consentimiento del tutor** para menores de 18, en el login y otra vez antes de cualquier contacto con una universidad.
- **Se borra el export** al terminar el análisis. Solo se guarda el resultado: porcentajes RIASEC y 3 ejemplos de evidencia.
- **Nada se comparte sin un toque del alumno**, universidad por universidad, y nunca los datos de redes (ver Modelo de negocio).
- **Aviso de privacidad** visible antes de subir el archivo, en lenguaje simple.
- **Voz genérica** de ElevenLabs para el yo del 2045; nunca se clona la voz del alumno.

## Guion del demo en vivo (60 segundos)

El jurado ve el flujo completo funcionando y se queda con el audio del yo del 2045.

| Tiempo | Qué se ve | Qué se dice |
| --- | --- | --- |
| 0–10 s | Landing de Rumbo | "Los tres de este equipo elegimos carrera a ciegas. No somos los únicos: 3 de cada 10 universitarios en México dejan su carrera en el primer año." |
| 10–25 s | Login, las 20 preguntas avanzando solas (perfil precargado), subida del export de TikTok | "Veinte preguntas, tres minutos, cero texto. Y si quieres, tu TikTok: lo que de verdad ves dice más que lo que contestas." |
| 25–40 s | Pantalla de carga: "Analizando tus intereses… Buscando universidades… Encontrando becas reales…" y el workflow de n8n en una segunda pestaña | "Gemma 4 lee sus intereses, el match sale de datos oficiales de O\*NET y Firecrawl trae becas reales." |
| 40–55 s | Top 3 carreras con %, universidades y becas; suena el audio del yo del 2045 | Silencio mientras suena el audio. |
| 55–60 s | Botón de PDF y frase de cierre en pantalla | "No te decimos qué estudiar. Te enseñamos quién puedes llegar a ser." |

**Requisitos técnicos del demo**

- **Modo demo:** si una API tarda más de 5 segundos, se usa el resultado en caché sin que se note.
- **Pantalla de carga** de 8 a 12 segundos aunque el resultado ya esté listo, para que se vea el proceso.
- **Perfil demo** precargado: respuestas, export de TikTok de ejemplo, resultado, PDF y audio.

**Plan de respaldo**

1. Si falla una API: el modo demo responde con caché.
2. Si falla el internet: todo el perfil demo corre local.
3. Si falla todo: video grabado del demo completo en otra pestaña.

- [ ] Grabar el video de respaldo
- [ ] Ensayar el guion 3 veces con cronómetro

## Alcance y criterios de éxito

El demo gana si el flujo corre de punta a punta en vivo, en menos de 60 segundos, sin un solo error en pantalla.

**Criterios de éxito del demo**

- [ ] El flujo completo corre en vivo de landing a PDF
- [ ] El top 3 sale del cálculo RIASEC + O\*NET, no de una respuesta fija
- [ ] Al menos una beca muestra link a su página oficial
- [ ] El audio del yo del 2045 suena sin cortes
- [ ] Se usan 6 herramientas: Lovable, MojoAuth, n8n, Gemma 4, Firecrawl, ElevenLabs
- [ ] Repo público en GitHub con licencia MIT y README

**Fuera de alcance para el hackathon**

- Instagram y Pinterest
- Checklist de admisión con fechas reales
- Panel para universidades y envío real de solicitudes
- Cuestionario validado estadísticamente
- Más de 20 carreras en el catálogo

**Roadmap después del hackathon**

1. Instagram y Pinterest con el mismo flujo de export.
2. Catálogo completo de carreras y universidades de México, actualizado con Firecrawl cada semestre.
3. Panel para universidades con solicitudes confirmadas.
4. Licencia para prepas con panel del orientador.
5. Validar el cuestionario con alumnos reales y medir cuántos siguen en su carrera al año.

### Futuro: el alumno elige 10, 20 o 50 preguntas

Después del hackathon, el alumno escoge cuánto tiempo le dedica; los tres modos usan el mismo cálculo y solo cambia qué tan preciso es el resultado.

| Modo | Para quién | Qué incluye | Tiempo | Confianza |
| --- | --- | --- | --- | --- |
| Rápido · 10 | Quiere una primera idea ya | Preguntas 1 a 6 (una por tipo), la 14 y las 18 a 20 | ~1.5 min | Baja |
| Estándar · 20 | La mayoría; es el del demo | Las 20 actuales | ~3 min | Media |
| Profundo · 50 | Indecisos, perfil explorador o quien ya va a decidir | Las 20 + 18 actividades (5 por tipo en total) + 3 de escoger una entre seis + 4 aptitudes + 2 valores + 3 de contexto | ~7 min | Alta |

**Diseño anidado.** Cada modo contiene al anterior. El alumno puede empezar en 10 y tocar "Afinar mi resultado" para seguir donde se quedó, sin repetir preguntas. El modo rápido no tiene matemáticas ni valores, así que no aplica el ajuste por aptitud.

**Lo que agrega el modo profundo**

- **4 aptitudes:** lectura y redacción, hablar en público, imaginar objetos en 3D y ciencias. Cada carrera del catálogo suma su nivel en esas cuatro.
- **2 valores:** trabajar en equipo o solo; horario fijo o libre.
- **3 de contexto:** promedio actual (filtra por promedio mínimo de admisión), si necesita trabajar mientras estudia (filtra horarios y carreras largas) y si sus papás esperan que estudie algo en específico. Si eso choca con su resultado, Rumbo le da una guía corta para platicarlo con ellos: ataca directo la presión familiar, una de las causas más comunes de elegir mal.

**Cuándo se sugiere subir de modo**

- Perfil explorador en 10 o 20: "Tus intereses están muy parejos; el modo profundo te da un resultado más claro".
- Menos de 3 puntos entre la carrera #1 y la #2.
- Antes de tocar "Quiero que me contacten": se le recomienda el modo profundo para decidir con confianza alta.

**Confianza visible.** El resultado muestra baja, media o alta según el modo y si subió TikTok, para que nadie tome una decisión grande con 10 preguntas.

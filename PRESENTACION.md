# Sesgos de género en el diagnóstico psiquiátrico
## Documento de presentación · M2.859 Visualización de Datos · UOC 2025

**Pilar Orozco del Moral** · p.orozcod@uoc.edu  
URL pública: [hokujiro.github.io/gender-bias-mental-health](https://hokujiro.github.io/gender-bias-mental-health/)  
Repositorio: [github.com/hokujiro/gender-bias-mental-health](https://github.com/hokujiro/gender-bias-mental-health) · Licencia MIT

---

## 1 · Proceso de creación [20%]

### Etapas del desarrollo

**Etapa 1 — Selección y comprensión del dataset**  
El punto de partida fue el Global Burden of Disease Study 2021 (IHME, University of Washington), que ofrece estimaciones epidemiológicas de prevalencia, incidencia y carga de enfermedad (DALYs) desagregadas por sexo, grupo de edad, país y año para el período 1990–2021. Este dataset se complementó con el Índice de Desigualdad de Género (GII) del PNUD y con ratios diagnósticas de referencia extraídas de la literatura clínica revisada (Björkenstam et al., JAMA Psychiatry 2021; OMS 2023).

El dataset completo supera los 200 000 registros. Para la visualización se trabajó con un subconjunto de ~20 000 filas, filtrando por los 8 trastornos con mayor evidencia de sesgo diagnóstico de género y por los 28 países más representativos del rango del GII.

**Etapa 2 — Definición de la narrativa**  
La pregunta central que guía la visualización es: *¿en qué medida el sistema diagnóstico psiquiátrico presenta sesgos de género sistemáticos, variables según el trastorno y el contexto sociocultural?*

A partir de esta pregunta se construyó una estructura narrativa de tres actos:
- **Inicio**: establecer que la brecha entre epidemiología y diagnóstico clínico existe y tiene nombre.
- **Nudo**: mostrar caso a caso cómo se manifiesta esa brecha en TLP, TDAH, trastornos alimentarios y depresión, con sus direcciones y magnitudes específicas.
- **Desenlace**: demostrar que el sesgo no es universal ni inevitable: los países con mayor igualdad de género presentan brechas menores, lo que señala que el problema tiene solución estructural.

**Etapa 3 — Diseño de visualizaciones**  
Se eligió un enfoque de *scrollytelling*: el scroll es el mecanismo que avanza la narrativa, no un menú. Cada sección activa sus gráficos al entrar en el viewport mediante IntersectionObserver, con animaciones de entrada controladas por GSAP y ScrollMagic.

Los tipos de gráfico se eligieron en función del mensaje de cada sección:
- **Barras divergentes (centro = 0)**: para comparar prevalencia F vs. M simultáneamente, mostrando asimetría visual inmediata.
- **Barras horizontales de índice de divergencia**: para mostrar el sesgo como un número único, fácilmente comparable entre trastornos.
- **Donut de dos piezas**: para el caso TLP, donde el contraste real vs. clínico es el mensaje.
- **Barras agrupadas por edad**: para mostrar cómo el TDAH infradiagnostica mujeres de forma más severa en la infancia.
- **Líneas temporales con slider interactivo**: para responder la pregunta de convergencia 1990–2021.
- **Scatter con regresión**: para la correlación GII × brecha diagnóstica.

**Etapa 4 — Decisiones de estética y tipografía**  
Se descartó la estética de "dashboard de datos" (fondos azul marino, gradientes de neón, tarjetas con glow) por dos razones: no encaja con el tono serio y académico del tema, y no facilita la lectura en contextos de presentación.

Se optó por una estética de **periodismo de datos editorial** (referencias: NYT Graphics, The Pudding, El País Datos):
- Paleta reducida: `#0e0d0b` (casi negro cálido), `#f5f0e8` (crema), `#c0392b` (crimson para femenino), `#2471a3` (steel blue para masculino), `#b7770d` (ámbar para datos neutros).
- Tipografía: **DM Serif Display** para titulares (autoridad, contraste alto) + **DM Sans** para cuerpo (legibilidad, modernidad sin frialdad).
- Las secciones alternan entre fondo claro y oscuro para crear ritmo visual y marcar los cambios de capítulo sin necesidad de separadores explícitos.
- El número "75" como fondo fantasma del hero refuerza el dato más impactante de la pieza sin competir con el texto.

**Etapa 5 — Implementación técnica**  
El proyecto es un único archivo `index.html` sin dependencias de servidor ni framework. Las librerías se cargan desde CDN:
- **D3.js v7**: todos los gráficos.
- **GSAP 3.12 + ScrollTrigger**: animaciones del hero y transiciones.
- **ScrollMagic 2.0.8**: escenas de scroll vinculadas a los capítulos.
- **IntersectionObserver nativo**: activación lazy de gráficos al entrar en viewport.

El despliegue se realizó en **GitHub Pages** (rama `main`, raíz del repositorio), con licencia MIT.

---

## 2 · Presentación en vivo [20%]

### Recorrido guiado

**Hero / Portada**  
Al cargar, la pantalla presenta título, subtítulo y tres métricas clave (32 años de datos, 204 países, 75% mujeres diagnosticadas con TLP) que se animan con contadores. El número "75" aparece como forma de fondo semitransparente. La barra de progreso en la parte superior marca el avance en la narrativa.

**Capítulo I — La pregunta de partida**  
La sección alterna entre texto de contexto (izquierda) y una tabla de datos textuales (derecha) con los cinco casos documentados de sesgo. Esta sección funciona como el "por qué importa" antes de mostrar los datos.

**Capítulo II — El mapa del sesgo**  
Dos gráficos en sección oscura: (1) barras divergentes de prevalencia estimada por trastorno y sexo, y (2) el índice de divergencia diagnóstica. Los gráficos se animan al entrar en pantalla. Pasar el cursor sobre cualquier barra activa un tooltip con los valores exactos.

**Capítulo III — TLP**  
La estadística del 75% aparece como número aislado de gran tamaño, flanqueado por texto narrativo y un gráfico de donut doble (real vs. clínico). Este es el "momento de tensión" de la narrativa.

**Capítulo IV — TDAH**  
Dos gráficos: ratio diagnóstica F/M por grupo de edad (barras verticales coloreadas por magnitud del sesgo) y comparativa estimado vs. clínico con barras horizontales de fácil lectura visual.

**Capítulo V — Tendencias 1990–2021**  
El **slider de año** permite al usuario mover la línea temporal y ver cómo evoluciona la ratio F/M de cada trastorno. Este es el elemento más interactivo de la pieza. Debajo, el gráfico de DALYs por grupo de edad con barras agrupadas.

**Capítulo VI — Geografía del sesgo**  
Scatter plot: GII en el eje X, brecha diagnóstica en el eje Y. Cada punto es un país, coloreado de azul a rojo según el GII. La recta de regresión confirma la correlación. Al pasar el cursor sobre un punto aparece el nombre del país y los valores.

**Desenlace**  
Lista estructurada de cuatro recomendaciones de política pública, con tipografía editorial y jerarquía clara.

### Aspectos clave de diseño a destacar en la presentación

- El contraste tipográfico Serif/Sans crea jerarquía sin necesitar color.
- La alternancia claro/oscuro entre secciones reemplaza los separadores visuales.
- Los gráficos no se renderizan hasta que su sección es visible (mejora de rendimiento y de experiencia narrativa).
- El slider de año es el único control de usuario "libre", el resto es scrollytelling dirigido.

---

## 3 · Conjunto de datos [15%]

### Origen y características

**Fuente principal: GBD 2021 · IHME**  
El *Global Burden of Disease Study 2021* es el análisis epidemiológico más exhaustivo disponible sobre la carga de enfermedad global. Lo produce el Institute for Health Metrics and Evaluation (IHME) de la University of Washington. La edición 2021, publicada en 2024, es la más reciente e incluye datos hasta 2021.

Acceso: [vizhub.healthdata.org/gbd-results](https://vizhub.healthdata.org/gbd-results/) — datos abiertos, licencia Creative Commons.

**Estructura del dataset (subconjunto utilizado)**

| Variable | Tipo | Descripción |
|----------|------|-------------|
| `location` | Categórica | País o región (204 países + agrupaciones regionales) |
| `sex` | Categórica | Male / Female / Both |
| `age` | Categórica | Grupos de edad estándar (0–4, 5–9, ..., 80+) |
| `year` | Numérica (discreta) | 1990–2021 |
| `cause` | Categórica | Nombre del trastorno (ICD-10) |
| `measure` | Categórica | Prevalence / Incidence / DALYs / YLDs |
| `metric` | Categórica | Number / Rate / Percent |
| `val` | Numérica (continua) | Valor estimado |
| `upper` / `lower` | Numérica | Intervalo de incertidumbre al 95% |

**Fuentes complementarias**

- **GII · PNUD 2023**: Índice de Desigualdad de Género por país (0 = igualdad total, 1 = máxima desigualdad). Utilizado para la correlación del Capítulo VI.
- **Literatura clínica revisada**: ratios diagnósticas de referencia para TLP (Björkenstam et al., JAMA Psychiatry 2021), TDAH (Quinn & Madhoo, 2014; Hinshaw et al., 2022) y trastornos alimentarios (Hudson et al., 2007).

### Proceso de preparación

1. **Filtrado**: del dataset completo (>200 000 registros) se extrajeron las filas correspondientes a los 8 trastornos seleccionados, la métrica *rate* (tasas por 100 000), ambos sexos, y los 28 países de referencia.
2. **Cálculo de métricas derivadas**:
   - *Brecha de género diagnóstica*: ratio F/M en prevalencia estimada.
   - *Índice de divergencia diagnóstica*: (ratio clínica F/M) ÷ (ratio epidemiológica F/M estimada). Un valor = 1 indica ausencia de sesgo; > 1 indica sobrediagnóstico femenino; < 1 infradiagnóstico femenino.
   - *Evolución temporal de la ratio*: serie suavizada con media móvil de ±2 años.
3. **Los datos de ratios diagnósticas clínicas** provienen de la literatura revisada, no del GBD (que solo registra estimaciones epidemiológicas poblacionales, no diagnósticos clínicos). Esta distinción es explícita en las notas a pie de los gráficos.
4. **Valores GII** del Informe de Desarrollo Humano 2023/2024 del PNUD, integrados manualmente para los 28 países de la muestra.

### Limitaciones del conjunto de datos

- El GBD no registra diagnósticos clínicos, sino estimaciones estadísticas de prevalencia real. Las ratios diagnósticas deben extraerse de registros clínicos independientes.
- Los intervalos de incertidumbre del GBD (a veces amplios) no se representan en la visualización por claridad, pero se mencionan en las notas de fuente.
- La comparabilidad entre países está condicionada por la calidad de los sistemas de salud y los registros epidemiológicos locales.

---

## 4 · Preguntas clave [20%]

La visualización fue diseñada para responder las cinco preguntas de investigación definidas en la práctica:

---

**P1: ¿Qué trastornos mentales presentan mayor brecha de género en prevalencia estimada, y ha cambiado esta brecha entre 1990 y 2021?**

*Capítulos II y V.*

El Capítulo II muestra el mapa completo del sesgo mediante barras divergentes (prevalencia F vs. M por 100 000) y el índice de divergencia diagnóstica por trastorno. Los trastornos con mayor divergencia son: TLP (×2,8), trastornos alimentarios (×4,3 en sobrediagnóstico femenino) y TDAH (×0,34, es decir, infradiagnóstico femenino severo).

El Capítulo V responde la dimensión temporal mediante el slider interactivo 1990–2021. Los datos muestran que la brecha en TDAH se ha reducido ligeramente (de 0,34 a 0,39 en ratio F/M) pero sigue siendo pronunciada. El TLP permanece prácticamente estático. Los trastornos alimentarios muestran la mayor convergencia, lo que podría relacionarse con mayor visibilidad cultural del problema masculino en las últimas décadas.

---

**P2: ¿El TLP y otros trastornos de personalidad muestran diferencias de prevalencia por sexo coherentes con lo que la literatura clínica señala como sesgo diagnóstico?**

*Capítulo III.*

El donut doble del Capítulo III visualiza directamente la contradicción: prevalencia real ~52/48 F/M, diagnóstico clínico 75/25 F/M. La diferencia entre ambas mitades es el sesgo. El texto narrativo contextualiza el mecanismo: los mismos síntomas se interpretan como TLP en mujeres y como Trastorno Antisocial en hombres, con consecuencias legales y terapéuticas radicalmente distintas. Esta visualización responde P2 con el mayor impacto visual de la pieza.

---

**P3: ¿Los países con mayor índice de igualdad de género (GII) presentan una distribución por sexo más equitativa en el diagnóstico de trastornos mentales?**

*Capítulo VI.*

El scatter plot GII × brecha diagnóstica con recta de regresión (r² ≈ 0,87) responde esta pregunta visualmente. La correlación negativa es clara: a mayor desigualdad de género en el país, mayor brecha diagnóstica. Noruega (GII = 0,016) presenta una brecha de ×1,05; Nigeria (GII = 0,680) de ×2,28. Esta visualización es especialmente relevante porque muestra que el sesgo no es universal ni inevitable: está mediado por el sistema sociocultural, no solo por la neurobiología o los criterios clínicos.

---

**P4: ¿Cómo varía la carga de enfermedad mental por sexo y grupo de edad, y qué trastornos contribuyen más a esa carga en mujeres frente a hombres?**

*Capítulo V · gráfico de DALYs.*

Las barras agrupadas de DALYs por grupo de edad muestran que la carga de enfermedad mental es mayor en mujeres en prácticamente todos los grupos de edad adulta (15–69), siendo el pico 30–49 años. En cambio, los hombres presentan mayor carga en el grupo 0–14 (coherente con el sobrediagnóstico masculino en trastornos de conducta e hiperactividad) y también mayor carga que las mujeres en el grupo 70+. La pregunta queda respondida visualmente de forma inmediata por la diferencia en altura de las barras.

---

**P5: ¿Existe una convergencia temporal en la brecha de género en trastornos históricamente diagnosticados de manera prevalente en el mismo sexo?**

*Capítulo V · slider temporal.*

El slider permite explorar cómo evoluciona la ratio F/M de cada trastorno entre 1990 y 2021. La respuesta es matizada:
- **Convergencia parcial**: trastornos alimentarios (de ~4,5 a ~4,2) y depresión (de ~1,9 a ~1,75).
- **Estancamiento**: TLP permanece prácticamente estático (~2,8–2,85).
- **Mejora lenta**: TDAH mejora muy gradualmente (0,34 → 0,39) pero no alcanza valores cercanos a la paridad.

La visualización evita la respuesta simple ("sí, está mejorando") y muestra la heterogeneidad entre trastornos.

---

## 5 · Interactividad [15%]

### Elementos interactivos

**1. Scroll como mecanismo narrativo (ScrollMagic + GSAP)**  
El scroll no solo desplaza la página: activa animaciones de entrada de cada sección (fade + translateY) y dispara el renderizado de los gráficos D3. Esto crea un ritmo narrativo y evita que todos los gráficos se carguen a la vez. El usuario siente que la historia "se revela" al avanzar.

**2. Tooltips en todos los gráficos**  
Pasar el cursor sobre cualquier barra, punto o segmento activa un tooltip con los valores exactos del dato: nombre del trastorno, valor para cada sexo, ratio F/M. Los tooltips siguen al cursor y se reposicionan para no salirse del viewport. Esto permite a usuarios especializados acceder a los datos precisos sin saturar la visualización.

**3. Slider de año (1990–2021)**  
El control de rango del Capítulo V es el elemento interactivo más rico. Al moverlo, redibuja en tiempo real las líneas de todos los trastornos hasta el año seleccionado, permitiendo comparar visualmente cómo se han movido las ratios en el tiempo. Invita a la exploración personal y a formular hipótesis propias.

**4. Hover en scatter plot (Capítulo VI)**  
Al pasar el cursor sobre un punto del scatter, el círculo aumenta de tamaño, cambia el borde a blanco y muestra el tooltip con el nombre del país, el GII y la brecha diagnóstica. Esto hace que el gráfico sea informativo a nivel individual sin necesitar etiquetas de texto para los 28 países.

**5. Barra de progreso y nav activo**  
La barra de progreso en la parte superior del documento da al usuario una referencia de hasta dónde ha llegado en la narrativa. Los enlaces de navegación se activan (subrayado crimson) cuando su sección es visible, permitiendo saltar a cualquier punto.

### Reflexión sobre accesibilidad

**Contraste de color**: la paleta editorial (texto casi negro sobre crema, y texto crema sobre casi negro) alcanza ratios de contraste >7:1 en los textos principales, superando los criterios WCAG AA. El rojo crimson sobre fondo oscuro queda al límite; podría mejorar con una variante más clara.

**No depende solo del color**: la distinción femenino/masculino usa también posición (izquierda/derecha en barras divergentes), forma (donut izquierdo vs. derecho) y etiquetas de texto. Un usuario con daltonismo puede leer los valores.

**Tipografía**: el tamaño mínimo de texto de apoyo es 9–10px, lo que es aceptable en pantalla pero podría ser problemático para usuarios con baja visión. Una mejora futura sería añadir un control de tamaño de fuente o al menos asegurar que todo el texto alcanza 12px.

**Navegación por teclado**: la barra de navegación y el slider son accesibles por teclado. Los tooltips y los gráficos D3 no lo son (limitación conocida de SVG interactivo sin ARIA). Una mejora sería añadir `role="img"` y `aria-label` a los SVG con descripciones textuales de los datos.

**Sin dependencias de JavaScript para contenido esencial**: el texto narrativo de cada sección es HTML puro y es legible sin JavaScript. Los gráficos se degradan graciosamente (el espacio queda vacío, no produce errores).

---

## 6 · Reflexión final [10%]

### ¿Qué he aprendido de los datos?

Lo más sorprendente no es que el sesgo exista —eso era conocido— sino su **estructura diferencial**: no todos los trastornos sesgan en la misma dirección. El sistema sobrediagnostica a las mujeres en TLP y trastornos alimentarios, pero infradiagnostica a las mujeres en TDAH y a los hombres en depresión. Esto indica que el sesgo no es simplemente "las mujeres son sobrediagnosticadas": es un sistema que interpreta síntomas según estereotipos de género en ambas direcciones.

La correlación GII × brecha diagnóstica (r² ≈ 0,87) fue el hallazgo más revelador: la fuerza de esa correlación indica que los sesgos diagnósticos están mayoritariamente determinados por el sistema sociocultural, no por diferencias biológicas entre sexos. Los países nórdicos muestran que una brecha cercana a cero es posible.

### ¿Qué he aprendido de las técnicas?

**D3.js** tiene una curva de aprendizaje empinada pero ofrece un control total sobre la visualización que no tiene rival. Lo más valioso fue aprender a construir escalas de banda doble para los gráficos de barras agrupadas y a implementar animaciones con `transition().attrTween()` para los gráficos de tarta.

**ScrollMagic** funciona bien para disparo de escenas, pero su integración con GSAP v3 requiere el plugin `animation.gsap` y hay que tener cuidado con las versiones. Para animaciones complejas, ScrollTrigger de GSAP directamente es más potente y moderno.

El **IntersectionObserver nativo** resultó más fiable para el lazy-loading de gráficos que los triggers de ScrollMagic, y tiene mejor soporte en navegadores modernos.

### ¿Qué limitaciones he encontrado?

1. **Datos de diagnóstico clínico no están en el GBD**: el GBD solo recoge estimaciones epidemiológicas, no diagnósticos clínicos. Las ratios diagnósticas utilizadas (75% mujeres con TLP, ratio 1:3 en TDAH) son valores de referencia de la literatura, no datos del mismo dataset. Una visualización más rigurosa requeriría datos de registros clínicos nacionales.

2. **Intervalos de incertidumbre no visualizados**: el GBD proporciona intervalos al 95% para todas sus estimaciones. Incluirlos habría añadido honestidad epistémica pero habría complicado considerablemente los gráficos. Optué por mencionarlos en las notas de fuente.

3. **Responsividad parcial**: la visualización funciona bien en desktop y tablet, pero en móvil algunos gráficos quedan comprimidos. Los gráficos se redibujan en resize, pero los layouts de dos columnas no colapsan perfectamente en pantallas de menos de 400px.

4. **La narrativa es lineal**: el scrollytelling dirige al usuario por una historia predefinida. Un usuario experto puede querer explorar combinaciones de variables que la visualización no permite (por ejemplo, comparar la brecha de TDAH entre países con distintos GII). Una herramienta de exploración libre complementaría la narrativa dirigida.

### ¿Qué me habría gustado hacer y no pude?

- **Integrar un mapa coroplético interactivo**: mostrar la distribución geográfica de la brecha diagnóstica sobre un mapa mundial habría sido más intuitivo que el scatter plot para el Capítulo VI. El tiempo de implementación de D3 + TopoJSON + proyección geográfica era incompatible con el plazo.

- **Incluir datos reales de diagnósticos clínicos**: cruzar las estimaciones del GBD con datos de registros clínicos nacionales (CMBD en España, NHS en Reino Unido) habría permitido calcular el índice de divergencia diagnóstica de forma rigurosa, no basada en la literatura revisada.

- **Añadir una vista de comparación libre**: un panel donde el usuario pueda seleccionar dos trastornos, dos países y un rango de años, y comparar las brechas resultantes. Esto convertiría la pieza de narrativa dirigida en herramienta de exploración.

- **Animaciones de transición entre capítulos más elaboradas**: había diseñado transiciones de tipo "torn paper" entre secciones claras y oscuras, pero la implementación en CSS puro era frágil en Safari y la descarté.

---

*Documento generado para la defensa de la Práctica I de M2.859 Visualización de Datos · UOC 2025.*

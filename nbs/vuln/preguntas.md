---
title: "Preguntas sobre vulnerabilidades"
format:
  html:
    toc: true
---

<style>
details.qa {
  border: 1px solid #dee2e6;
  border-radius: 6px;
  padding: 0;
  margin: 0.75rem 0;
  background: #fff;
  overflow: hidden;
}

details.qa[open] {
  background: #fbfbfb;
}

details.qa > summary {
  cursor: pointer;
  font-weight: 600;
  line-height: 1.4;
  list-style-position: outside;
  padding: 0.85rem 1rem 0.85rem 2.15rem;
  background: #f1f5f9;
  color: #102a43;
  border-left: 4px solid #2b6cb0;
}

details.qa > summary::marker {
  color: #2b6cb0;
}

details.qa[open] > summary {
  border-bottom: 1px solid #dbe4ee;
}

details.qa .respuesta {
  max-height: 22rem;
  overflow-y: auto;
  margin: 0;
  padding: 0.9rem 1rem 1rem 1.25rem;
  background: #fff;
  border-left: 4px solid #6c757d;
}

details.qa .respuesta::before {
  content: "Respuesta";
  display: inline-block;
  margin-bottom: 0.6rem;
  padding: 0.15rem 0.45rem;
  border-radius: 4px;
  background: #e9ecef;
  color: #495057;
  font-size: 0.78rem;
  font-weight: 700;
  letter-spacing: 0.02em;
  text-transform: uppercase;
}

details.qa .respuesta p:last-child,
details.qa .respuesta ul:last-child {
  margin-bottom: 0;
}
</style>


Esta página funciona como una guía de autoevaluación para la sección de vulnerabilidades. Cada pregunta incluye una respuesta desplegable para que puedas intentar responder primero y luego contrastar tu razonamiento.

## Lo que deberías saber

<details class="qa">
<summary>¿Cuál es la diferencia entre un bug y una vulnerabilidad?</summary>
<div class="respuesta">
<p>Un bug es una falla de software que produce un comportamiento inesperado. Puede afectar disponibilidad, resultados, experiencia de usuario o lógica del sistema, pero no necesariamente permite una acción no autorizada.</p>
<p>Una vulnerabilidad es una debilidad que puede ser aprovechada por un adversario para afectar confidencialidad, integridad o disponibilidad. La diferencia clave está en la explotabilidad y el impacto de seguridad. Un bug puede ser molesto o costoso sin ser explotable. Una vulnerabilidad conecta una falla con una ruta realista de abuso.</p>
<p>Por eso, al analizar un hallazgo, no basta con preguntar si el código tiene un error. También hay que preguntar quién puede alcanzarlo, bajo qué condiciones, qué capacidades requiere el atacante y qué efecto produce si se explota.</p>
</div>
</details>

<details class="qa">
<summary>¿Qué condiciones hacen que una falla sea explotable?</summary>
<div class="respuesta">
<p>Para que una falla sea explotable debe existir una ruta realista entre el adversario y la debilidad. Esto implica que el atacante pueda alcanzar el componente afectado, controlar o influir en los datos relevantes y producir un efecto de seguridad observable.</p>
<p>También importa el contexto. Una misma debilidad puede ser crítica en un servicio expuesto a internet y casi irrelevante en una herramienta interna sin entrada controlable por terceros. La explotabilidad depende de superficie de ataque, permisos, validaciones, configuración, exposición y medidas compensatorias.</p>
<p>Por eso, el análisis defensivo no se limita a la presencia de una falla. Debe evaluar si existe una secuencia plausible de acciones que permita convertir esa falla en daño.</p>
</div>
</details>

<details class="qa">
<summary>¿Para qué sirve un modelo de amenazas al estudiar vulnerabilidades?</summary>
<div class="respuesta">
<p>Un modelo de amenazas sirve para ordenar el análisis de riesgo. Ayuda a identificar activos, adversarios, capacidades, puntos de entrada, componentes sensibles y posibles impactos. Sin ese contexto, es fácil tratar todos los hallazgos como si tuvieran el mismo peso.</p>
<p>En vulnerabilidades, el modelo de amenazas permite preguntar qué puede hacer realmente un atacante con una debilidad. También ayuda a decidir qué controles son necesarios, qué rutas de ataque son prioritarias y qué hallazgos deben corregirse primero.</p>
<p>Su valor pedagógico es importante porque conecta código, arquitectura y riesgo. Una debilidad no existe en abstracto. Existe dentro de un sistema con usuarios, permisos, datos, dependencias y supuestos de operación.</p>
</div>
</details>

<details class="qa">
<summary>¿Cuál es la diferencia entre CWE y CVE?</summary>
<div class="respuesta">
<p>CWE clasifica tipos de debilidades. Describe patrones de error que pueden originar vulnerabilidades, como validación insuficiente, control de acceso incorrecto, exposición de información o inyección. CWE ayuda a hablar de la causa o familia del problema.</p>
<p>CVE identifica vulnerabilidades públicas específicas. Un CVE se refiere a un caso concreto en un producto, biblioteca, versión o componente determinado. Ayuda a coordinar comunicación, análisis, remediación y seguimiento entre organizaciones y herramientas.</p>
<p>Una forma práctica de distinguirlos es esta. CWE responde qué tipo de debilidad es. CVE responde qué vulnerabilidad pública específica fue reportada.</p>
</div>
</details>

<details class="qa">
<summary>¿Qué aporta CVSS y qué no debería esperarse de ese puntaje?</summary>
<div class="respuesta">
<p>CVSS aporta una estimación estandarizada de severidad. Resume características como impacto, complejidad de ataque, privilegios requeridos, interacción del usuario y alcance. Esto ayuda a ordenar hallazgos y comunicar urgencia de manera consistente.</p>
<p>CVSS no reemplaza el análisis contextual. Un puntaje alto no siempre implica máximo riesgo en todos los entornos, y un puntaje medio puede ser urgente si afecta un activo crítico o una ruta de ataque muy expuesta.</p>
<p>Por eso, CVSS debe usarse como una señal de priorización, no como decisión automática. La decisión final debe considerar exposición, criticidad del sistema, explotación conocida, disponibilidad de parche y controles compensatorios.</p>
</div>
</details>

<details class="qa">
<summary>¿Qué rol cumple la NVD en la gestión de vulnerabilidades?</summary>
<div class="respuesta">
<p>La National Vulnerability Database reúne y enriquece información sobre vulnerabilidades públicas. Para muchos CVE, entrega metadatos, referencias, puntajes, productos afectados y descripciones útiles para priorización.</p>
<p>Las herramientas de escaneo suelen consultar bases como NVD u otras fuentes de avisos para determinar si una dependencia o producto está asociado a una vulnerabilidad conocida. Esto convierte a NVD en una fuente importante para automatizar análisis.</p>
<p>Sin embargo, la información de NVD no debe leerse de forma aislada. Puede haber retrasos, cambios de puntaje, mapeos imperfectos o diferencias entre bases. Conviene contrastar con avisos del proveedor, repositorios oficiales y evidencia del entorno propio.</p>
</div>
</details>

<details class="qa">
<summary>¿Dónde entra MITRE ATT&CK si no es un catálogo de vulnerabilidades?</summary>
<div class="respuesta">
<p>MITRE ATT&CK describe tácticas y técnicas observadas en el comportamiento de adversarios. No clasifica debilidades de software ni identifica vulnerabilidades específicas. Su foco está en cómo actúa un atacante antes, durante o después de una intrusión.</p>
<p>ATT&CK complementa el análisis de vulnerabilidades porque ayuda a conectar una falla técnica con posibles acciones ofensivas. Por ejemplo, una vulnerabilidad puede facilitar ejecución de código, persistencia, robo de credenciales o movimiento lateral.</p>
<p>En un caso de estudio, mapear conductas a ATT&CK ayuda a comunicar el incidente con más precisión. No reemplaza la evidencia técnica, pero mejora la lectura defensiva y la relación con detección y respuesta.</p>
</div>
</details>

<details class="qa">
<summary>¿Cuál es la diferencia entre severidad y riesgo?</summary>
<div class="respuesta">
<p>La severidad describe la gravedad técnica potencial de una vulnerabilidad. Suele apoyarse en métricas como CVSS y considera impacto, facilidad de explotación y condiciones técnicas generales.</p>
<p>El riesgo combina severidad con contexto. Incluye probabilidad de explotación, exposición del sistema, valor del activo afectado, existencia de controles compensatorios, explotación activa y consecuencias para la organización.</p>
<p>Por eso, dos vulnerabilidades con la misma severidad pueden tener riesgos distintos. Una puede estar en un servicio público con datos sensibles. Otra puede estar en un entorno aislado, sin ruta de acceso para adversarios. La priorización necesita ambas dimensiones.</p>
</div>
</details>

<details class="qa">
<summary>¿Qué diferencia hay entre análisis estático y escaneo de dependencias?</summary>
<div class="respuesta">
<p>El análisis estático revisa código fuente o representaciones derivadas del código para encontrar patrones inseguros. Puede detectar problemas como inyección, uso inseguro de datos, flujos peligrosos o errores de validación. CodeQL es un ejemplo de esta aproximación.</p>
<p>El escaneo de dependencias revisa componentes externos usados por el proyecto y los compara contra bases de vulnerabilidades conocidas. Busca responder si alguna biblioteca, paquete o versión incluida tiene vulnerabilidades públicas asociadas. Grype es un ejemplo de esta aproximación.</p>
<p>Ambos enfoques son complementarios. El análisis estático mira el código propio. El escaneo de dependencias mira el ecosistema que el proyecto incorpora. Un programa puede tener código propio seguro y aun así depender de una biblioteca vulnerable.</p>
</div>
</details>

<details class="qa">
<summary>¿Qué es CodeQL y por qué produce resultados en SARIF?</summary>
<div class="respuesta">
<p>CodeQL es una herramienta de análisis estático que modela el código como una base de datos consultable. Permite ejecutar consultas de seguridad y calidad sobre esa representación para detectar patrones problemáticos.</p>
<p>SARIF es un formato estándar para resultados de análisis estático. Permite describir reglas, hallazgos, ubicaciones de archivo, severidad, mensajes y metadatos de herramienta de manera interoperable.</p>
<p>Usar SARIF permite integrar resultados con plataformas, revisiones de código, sistemas de seguimiento y flujos de CI/CD. El valor no está solo en detectar hallazgos, sino en poder procesarlos, compararlos y gestionarlos de forma consistente.</p>
</div>
</details>

<details class="qa">
<summary>¿Qué es Grype y qué tipo de vulnerabilidades detecta?</summary>
<div class="respuesta">
<p>Grype es una herramienta que escanea componentes y dependencias para detectar vulnerabilidades conocidas. Lee manifiestos, paquetes instalados o artefactos como imágenes de contenedor, y compara los componentes encontrados con bases de vulnerabilidades.</p>
<p>Sus hallazgos suelen incluir identificador de vulnerabilidad, paquete afectado, versión actual, severidad, descripción y versión de corrección cuando existe. Esto permite priorizar actualización o mitigación de dependencias vulnerables.</p>
<p>Grype no prueba si una vulnerabilidad es explotable en el contexto específico de la aplicación. Indica que un componente vulnerable está presente o parece estarlo. La decisión defensiva requiere validar exposición, uso real del componente y disponibilidad de remediación.</p>
</div>
</details>

<details class="qa">
<summary>¿Por qué los manifiestos de dependencias son relevantes para Grype?</summary>
<div class="respuesta">
<p>Los manifiestos de dependencias declaran componentes usados por un proyecto. Archivos como <code>package.json</code>, <code>requirements.txt</code>, <code>pom.xml</code>, <code>go.mod</code> o <code>Cargo.toml</code> permiten inferir qué bibliotecas y versiones forman parte del proyecto.</p>
<p>Grype usa esa información para construir un inventario de componentes y compararlo contra bases de vulnerabilidades. Si no encuentra manifiestos ni otra fuente de paquetes, su capacidad de detección puede ser limitada.</p>
<p>Esto no significa que no existan riesgos. Puede haber dependencias incorporadas manualmente, imágenes base, componentes del sistema operativo o binarios externos que no aparezcan en manifiestos del repositorio. Por eso el alcance del escaneo debe definirse con claridad.</p>
</div>
</details>

<details class="qa">
<summary>¿Qué significa una versión de corrección en un reporte de vulnerabilidades?</summary>
<div class="respuesta">
<p>Una versión de corrección indica una versión del componente donde la vulnerabilidad reportada fue corregida, mitigada o ya no aplica según la fuente consultada. Es una pista práctica para remediar el hallazgo mediante actualización.</p>
<p>Sin embargo, actualizar no siempre es trivial. Puede haber incompatibilidades, cambios de API, dependencias transitivas, restricciones de plataforma o pruebas necesarias antes de mover la versión en producción.</p>
<p>Si no existe versión de corrección, la organización debe evaluar mitigaciones alternativas. Por ejemplo, deshabilitar funcionalidad afectada, aplicar controles compensatorios, aislar el componente, monitorear explotación o reemplazar la dependencia.</p>
</div>
</details>

<details class="qa">
<summary>¿Qué diferencia hay entre falso positivo y falso negativo?</summary>
<div class="respuesta">
<p>Un falso positivo ocurre cuando una herramienta reporta un problema que no representa una vulnerabilidad real o accionable en ese contexto. Puede deberse a una regla demasiado amplia, falta de contexto o una dependencia presente pero no usada de forma vulnerable.</p>
<p>Un falso negativo ocurre cuando existe una vulnerabilidad real y la herramienta no la detecta. Es especialmente peligroso porque produce una falsa sensación de seguridad.</p>
<p>Ambos importan. Los falsos positivos consumen tiempo y pueden erosionar confianza en las herramientas. Los falsos negativos dejan riesgo sin visibilidad. Por eso los resultados deben revisarse, calibrarse y complementarse con otros métodos.</p>
</div>
</details>

<details class="qa">
<summary>¿Por qué un hallazgo de seguridad no termina cuando aparece en un reporte?</summary>
<div class="respuesta">
<p>Un reporte es el inicio de la gestión, no el cierre. Después de detectar un hallazgo hay que validar si aplica, entender impacto, priorizar, asignar responsable, remediar, probar y verificar que el problema desapareció.</p>
<p>También hay que decidir si corresponde comunicación, seguimiento o cambios de proceso. Si el hallazgo revela una debilidad recurrente, puede requerir capacitación, regla de revisión, prueba automatizada o cambio de arquitectura.</p>
<p>El valor real de una herramienta aparece cuando sus resultados se transforman en decisiones y mejoras. Sin ese ciclo, el análisis produce datos, pero no reduce riesgo.</p>
</div>
</details>

<details class="qa">
<summary>¿Qué enseña el caso LiteLLM sobre vulnerabilidades y cadena de suministro?</summary>
<div class="respuesta">
<p>El caso LiteLLM muestra que un incidente puede venir de la cadena de publicación y no solo del código propio. Versiones maliciosas de un paquete legítimo pueden afectar a usuarios que confían en el nombre del proyecto y en el repositorio de paquetes.</p>
<p>Esto amplía la idea de vulnerabilidad. No se trata solo de una función mal escrita. También importan credenciales de publicación, integridad del paquete, automatización de CI/CD, permisos de herramientas y confianza en dependencias.</p>
<p>La lección defensiva es que actualizar puede no ser suficiente. Si una versión maliciosa se instaló, puede haber credenciales expuestas, persistencia, actividad de red y efectos posteriores que requieren respuesta a incidentes.</p>
</div>
</details>

<details class="qa">
<summary>¿Por qué un archivo <code>.pth</code> malicioso en Python puede ser grave?</summary>
<div class="respuesta">
<p>Un archivo <code>.pth</code> puede influir en la inicialización del intérprete de Python. Si se abusa de ese mecanismo, código malicioso puede ejecutarse automáticamente cuando el entorno Python se inicia o cuando se carga la configuración del entorno.</p>
<p>Esto es grave porque reduce la necesidad de que el usuario invoque una función específica del paquete comprometido. La instalación o inicialización del entorno puede transformarse en una oportunidad de ejecución.</p>
<p>En incidentes de cadena de suministro, este tipo de mecanismo aumenta el impacto potencial. Puede permitir robo de credenciales, persistencia o preparación de etapas posteriores sin que el desarrollador lo note inmediatamente.</p>
</div>
</details>

<details class="qa">
<summary>¿Qué significa que un LLM detector de vulnerabilidades generalice fuera de distribución?</summary>
<div class="respuesta">
<p>Significa que el modelo mantiene buen desempeño cuando se evalúa en datos independientes, distintos de los usados para entrenar. En detección de vulnerabilidades, esto es crucial porque el mundo real no replica exactamente el conjunto de datos de entrenamiento.</p>
<p>Un modelo puede obtener alta exactitud dentro del mismo conjunto de datos y aun así fallar en muestras nuevas. Eso puede ocurrir si aprendió correlaciones superficiales, duplicados, estilos de código o marcas propias de la fuente original.</p>
<p>La generalización fuera de distribución es una señal más fuerte. Indica que el modelo aprendió patrones que viajan a otros contextos, aunque tampoco garantiza por sí sola que sea seguro usarlo sin revisión humana.</p>
</div>
</details>

<details class="qa">
<summary>¿Por qué los datos de entrenamiento son críticos para LLMs detectores de vulnerabilidades?</summary>
<div class="respuesta">
<p>Los datos de entrenamiento determinan qué patrones puede aprender el modelo. Si los datos tienen duplicados, etiquetas incorrectas, clases desbalanceadas o ejemplos que no representan vulnerabilidades reales, el modelo puede aprender señales equivocadas.</p>
<p>En detección de vulnerabilidades, esto es especialmente sensible porque muchas debilidades son raras, contextuales y difíciles de etiquetar. Un modelo entrenado con datos ruidosos puede parecer efectivo en pruebas internas y fallar cuando enfrenta código real.</p>
<p>Por eso, la calidad del conjunto de datos no es un detalle secundario. Es parte central de la validez del detector y de la confianza que se puede tener en sus resultados.</p>
</div>
</details>

## Preguntas para responder

<details class="qa">
<summary>Si CodeQL reporta una posible inyección SQL, ¿qué deberías revisar antes de marcarla como crítica?</summary>
<div class="respuesta">
<p>Primero revisaría si la entrada que llega a la consulta puede ser controlada por un usuario o adversario. Luego revisaría si existe sanitización, parametrización, validación o alguna biblioteca que construya la consulta de forma segura.</p>
<p>También observaría el contexto de ejecución. No es lo mismo una consulta en una ruta pública de una aplicación web que una herramienta administrativa local. Importan permisos, exposición, datos afectados y posibilidad real de explotación.</p>
<p>Finalmente, revisaría si el hallazgo corresponde a una ruta ejecutable y si CodeQL muestra un flujo de datos claro desde la fuente no confiable hasta el uso peligroso. Solo después de validar esas condiciones corresponde priorizarlo como crítico.</p>
</div>
</details>

<details class="qa">
<summary>Si Grype reporta una vulnerabilidad crítica en una dependencia que no se usa en producción, ¿qué harías?</summary>
<div class="respuesta">
<p>No la descartaría automáticamente. Primero confirmaría si realmente no llega al artefacto productivo. Hay dependencias de desarrollo que no se empaquetan ni ejecutan en producción, pero también hay casos donde una dependencia marcada como desarrollo termina incluida en una imagen o entorno final.</p>
<p>Después evaluaría si la vulnerabilidad puede ser explotada durante construcción, pruebas, CI/CD o publicación. Algunas dependencias no afectan producción, pero sí pueden afectar la cadena de suministro si se ejecutan en flujos automatizados con secretos o permisos altos.</p>
<p>Si se confirma que no hay exposición, se puede bajar la prioridad o documentar una excepción. Aun así, conviene actualizar o eliminar la dependencia cuando sea razonable, porque el inventario cambia y una dependencia no usada hoy puede entrar en uso mañana.</p>
</div>
</details>

<details class="qa">
<summary>Si un repositorio no tiene manifiestos de dependencias, ¿significa que no tiene vulnerabilidades en dependencias?</summary>
<div class="respuesta">
<p>No. Significa que la herramienta puede tener menos fuentes para construir el inventario de dependencias. El repositorio podría usar binarios incluidos manualmente, dependencias del sistema operativo, imágenes de contenedor, scripts de instalación o paquetes resueltos fuera de los manifiestos tradicionales.</p>
<p>También puede ocurrir que el proyecto tenga dependencias en archivos no soportados por la herramienta o que el artefacto final incorpore componentes durante la construcción.</p>
<p>La conclusión correcta es que el alcance del escaneo fue limitado. Para afirmar con más confianza que no hay vulnerabilidades en dependencias, habría que analizar el artefacto construido, imágenes, entorno de ejecución o SBOM asociado.</p>
</div>
</details>

<details class="qa">
<summary>Si CodeQL analiza solo el lenguaje principal del repositorio, ¿qué riesgo aparece?</summary>
<div class="respuesta">
<p>El riesgo es dejar sin analizar partes relevantes del código escritas en otros lenguajes. Muchos proyectos son mixtos. Pueden tener backend en Python, frontend en JavaScript, scripts de despliegue, infraestructura como código o componentes auxiliares.</p>
<p>Si el análisis se limita al lenguaje más frecuente, pueden quedar fuera rutas de ataque importantes. Por ejemplo, un repositorio mayoritariamente Python podría contener JavaScript expuesto al usuario o scripts de automatización con manejo de secretos.</p>
<p>La decisión puede ser razonable por simplicidad y rendimiento, pero debe documentarse como una limitación. Para proyectos críticos, conviene ejecutar análisis por lenguaje o complementar con otras herramientas.</p>
</div>
</details>

<details class="qa">
<summary>Si CodeQL y Grype entregan hallazgos distintos en el mismo repositorio, ¿cuál tiene razón?</summary>
<div class="respuesta">
<p>Pueden tener razón ambos, porque observan superficies distintas. CodeQL revisa código propio y patrones de implementación. Grype revisa componentes y vulnerabilidades conocidas en dependencias.</p>
<p>Un hallazgo de CodeQL puede existir aunque no haya dependencias vulnerables. Un hallazgo de Grype puede existir aunque el código propio no tenga patrones inseguros. También pueden relacionarse si el código usa de forma peligrosa una dependencia vulnerable.</p>
<p>La pregunta no debería ser cuál herramienta tiene razón, sino qué riesgo describe cada hallazgo. Hay que validar alcance, evidencia, severidad, exposición y remediación para cada caso.</p>
</div>
</details>

<details class="qa">
<summary>Si aparece un CVE nuevo después de haber ejecutado Grype, ¿el reporte anterior sigue siendo suficiente?</summary>
<div class="respuesta">
<p>No necesariamente. Un reporte de vulnerabilidades es válido para el momento y las bases de datos usadas en esa ejecución. Si aparece un CVE nuevo, un componente que antes parecía limpio puede quedar asociado a una vulnerabilidad.</p>
<p>Por eso el análisis de dependencias debe repetirse de forma periódica o integrarse a CI/CD y monitoreo. La seguridad de dependencias cambia aunque el código del proyecto no cambie.</p>
<p>También es importante conservar inventarios o SBOMs de versiones publicadas. Así, cuando aparece un CVE nuevo, se puede saber qué versiones del producto incluyeron el componente afectado.</p>
</div>
</details>

<details class="qa">
<summary>Si un hallazgo tiene CVSS alto, pero el componente no es alcanzable, ¿debe corregirse igual?</summary>
<div class="respuesta">
<p>Debe evaluarse con cuidado. Un CVSS alto indica severidad técnica potencial, pero el riesgo real depende de si el componente es alcanzable y explotable en el entorno concreto.</p>
<p>Si hay evidencia sólida de que no es alcanzable, puede priorizarse por debajo de otros hallazgos más expuestos. Sin embargo, la decisión debe documentarse, porque cambios futuros de configuración o uso podrían volverlo relevante.</p>
<p>Si existe una actualización segura y de bajo costo, suele ser razonable corregir de todos modos. Si la actualización es riesgosa, se puede justificar una mitigación temporal con controles compensatorios y seguimiento.</p>
</div>
</details>

<details class="qa">
<summary>Si una vulnerabilidad no tiene versión de corrección, ¿qué opciones defensivas quedan?</summary>
<div class="respuesta">
<p>La primera opción es reducir exposición. Puede deshabilitarse la funcionalidad afectada, limitar acceso, aplicar reglas de filtrado, cambiar configuración, aislar el componente o restringir permisos.</p>
<p>También se puede reemplazar la dependencia, aplicar un parche temporal, usar una rama mantenida por la comunidad o compensar con monitoreo y detección de explotación. En algunos casos, corresponde aceptar riesgo de forma formal por un tiempo limitado.</p>
<p>Lo importante es no tratar la ausencia de versión de corrección como ausencia de acción. Puede no haber actualización disponible, pero sí pueden existir mitigaciones mientras se espera una solución definitiva.</p>
</div>
</details>

<details class="qa">
<summary>Si un paquete legítimo fue comprometido y publicado con código malicioso, ¿Grype necesariamente lo detectará?</summary>
<div class="respuesta">
<p>No necesariamente. Grype se basa principalmente en vulnerabilidades conocidas y bases de datos asociadas a componentes y versiones. Si el paquete malicioso aún no tiene aviso, CVE o firma reconocida en las fuentes usadas, puede no aparecer como vulnerable.</p>
<p>Los ataques de cadena de suministro pueden requerir otras señales. Por ejemplo, cambios inesperados entre versiones, comportamiento de instalación sospechoso, ejecución automática, conexiones de red anómalas o alteraciones en el proceso de publicación.</p>
<p>Por eso, el escaneo de vulnerabilidades conocidas debe complementarse con verificación de integridad, revisión de cambios, monitoreo de comportamiento, protección de credenciales y controles de publicación.</p>
</div>
</details>

<details class="qa">
<summary>Si un incidente involucra robo de credenciales, ¿por qué actualizar la dependencia no basta?</summary>
<div class="respuesta">
<p>Actualizar la dependencia puede detener el uso de la versión maliciosa o vulnerable, pero no revierte efectos ya ocurridos. Si el atacante obtuvo credenciales, tokens o secretos, esos materiales pueden seguir siendo válidos aunque el paquete se actualice.</p>
<p>En ese caso corresponde rotar credenciales, revisar registros, buscar persistencia, analizar actividad de red, verificar accesos a servicios externos y evaluar qué datos pudieron quedar expuestos.</p>
<p>La actualización es una acción de contención o remediación técnica, pero la respuesta a incidentes debe considerar el alcance completo del compromiso.</p>
</div>
</details>

<details class="qa">
<summary>Si mapeas un incidente a MITRE ATT&CK, ¿qué valor agrega?</summary>
<div class="respuesta">
<p>Agrega una forma estructurada de describir comportamiento adversario. En vez de listar acciones sueltas, puedes vincularlas con técnicas conocidas, como ejecución por hooks de inicio, robo de credenciales o despliegue de contenedores.</p>
<p>Esto facilita comunicación entre equipos, comparación con otros incidentes y diseño de detecciones. También ayuda a pensar qué otras acciones podría intentar un atacante si ya observaste una técnica.</p>
<p>El mapeo no prueba por sí solo que algo ocurrió. Debe estar respaldado por evidencia. Su valor está en organizar la interpretación y conectar el caso con patrones defensivos más amplios.</p>
</div>
</details>

<details class="qa">
<summary>Si un LLM detecta una vulnerabilidad y explica su razonamiento, ¿deberías confiar en la explicación?</summary>
<div class="respuesta">
<p>No deberías confiar solo por la fluidez de la explicación. Los LLMs pueden producir explicaciones plausibles pero incorrectas. En seguridad, una justificación convincente debe contrastarse con el código, el flujo de datos, la configuración y el modelo de amenazas.</p>
<p>La explicación puede ser útil como hipótesis inicial. Puede orientar qué revisar, qué entrada es relevante o qué control parece faltar. Pero debe verificarse con evidencia técnica.</p>
<p>Una práctica razonable es tratar al LLM como asistente de análisis, no como autoridad. Sus hallazgos deben pasar por revisión humana, pruebas o contraste con herramientas especializadas.</p>
</div>
</details>

<details class="qa">
<summary>Si un modelo tiene alta exactitud dentro de distribución y baja fuera de distribución, ¿qué indica?</summary>
<div class="respuesta">
<p>Indica que probablemente no generaliza bien. Puede haber aprendido patrones propios del conjunto de entrenamiento, duplicados, estilo de los ejemplos o artefactos de etiquetado, en vez de patrones reales de vulnerabilidad.</p>
<p>En detección de vulnerabilidades, esto es grave porque el código real suele diferir de los datos de entrenamiento. Un modelo que falla fuera de distribución puede dar una falsa sensación de seguridad.</p>
<p>La evaluación útil debe incluir benchmarks independientes, cobertura por tipos de CWE y análisis de desempeño en clases raras. La exactitud interna no basta para afirmar que el detector será confiable.</p>
</div>
</details>

<details class="qa">
<summary>Si un conjunto de datos tiene muchos duplicados, ¿cómo puede afectar a un detector basado en aprendizaje automático?</summary>
<div class="respuesta">
<p>Los duplicados pueden inflar métricas. Si ejemplos muy similares aparecen en entrenamiento y prueba, el modelo puede memorizar patrones en vez de aprender características generales de vulnerabilidad.</p>
<p>También pueden distorsionar la distribución de clases. Algunas CWE o estilos de código pueden aparecer artificialmente sobrerrepresentados, haciendo que el modelo parezca fuerte en patrones frecuentes y débil en otros.</p>
<p>Por eso la deduplicación es parte esencial de una evaluación seria. Sin ella, la métrica puede reflejar repetición de datos más que capacidad de detección.</p>
</div>
</details>

<details class="qa">
<summary>Si un detector aprende a reconocer código "parecido a vulnerable", ¿por qué eso no basta?</summary>
<div class="respuesta">
<p>No basta porque la detección de vulnerabilidades exige distinguir una debilidad explotable de código seguro o corregido que puede parecer similar. Dos funciones pueden tener estructura parecida, pero diferir en una validación, una comprobación de permisos o una sanitización clave.</p>
<p>Si el modelo solo aprende señales generales de código sospechoso, puede fallar al comparar una vulnerabilidad con su corrección. Esto produce falsos positivos y falsos negativos difíciles de confiar.</p>
<p>Un detector útil debe capturar el detalle semántico de la debilidad. Debe entender qué condición permite abuso y por qué el cambio de corrección modifica esa condición.</p>
</div>
</details>

<details class="qa">
<summary>Si sintetizas ejemplos de vulnerabilidades para entrenar un modelo, ¿qué riesgos aparecen?</summary>
<div class="respuesta">
<p>El primer riesgo es crear ejemplos artificiales demasiado limpios, repetitivos o alejados del código real. El modelo podría aprender patrones de generación y no patrones reales de vulnerabilidad.</p>
<p>El segundo riesgo es etiquetar mal. Un ejemplo sintético puede parecer vulnerable, pero no ser explotable, o puede no corresponder exactamente a la CWE que se quiere representar.</p>
<p>La síntesis puede ser útil para clases poco representadas, pero requiere validación. Idealmente debe combinarse con revisión humana, comparación con datos reales y evaluación fuera de distribución.</p>
</div>
</details>

<details class="qa">
<summary>Si tuvieras que priorizar hallazgos de CodeQL y Grype en una misma semana, ¿qué criterios usarías?</summary>
<div class="respuesta">
<p>Usaría severidad técnica, exposición, explotabilidad, criticidad del activo, disponibilidad de corrección y evidencia de explotación activa. También consideraría si el hallazgo afecta datos sensibles, autenticación, autorización o ejecución remota.</p>
<p>Para CodeQL, revisaría si el flujo vulnerable es alcanzable por entradas no confiables y si falta un control real. Para Grype, revisaría si la dependencia afectada está en el artefacto productivo, si se usa la funcionalidad vulnerable y si existe versión de corrección.</p>
<p>La prioridad final debería equilibrar impacto y factibilidad. A veces una actualización de dependencia crítica es rápida. Otras veces un hallazgo de código propio requiere rediseño. La gestión debe ser explícita y trazable.</p>
</div>
</details>

<details class="qa">
<summary>Si una herramienta entrega muchos falsos positivos, ¿deberías dejar de usarla?</summary>
<div class="respuesta">
<p>No necesariamente. Primero conviene ajustar configuración, reglas, exclusiones y alcance. Algunas herramientas son muy útiles, pero necesitan calibración para el lenguaje, arquitectura y riesgos del proyecto.</p>
<p>También se puede usar la herramienta en etapas específicas. Por ejemplo, bloquear solo hallazgos de alta confianza y dejar otros como advertencias revisables. Esto evita fatiga sin perder visibilidad.</p>
<p>Dejar de usarla puede ser razonable si el costo de revisión supera consistentemente el valor de los hallazgos. Pero esa decisión debería basarse en evidencia y no solo en frustración inicial.</p>
</div>
</details>

<details class="qa">
<summary>Si una vulnerabilidad aparece en una dependencia transitiva, ¿quién debería corregirla?</summary>
<div class="respuesta">
<p>La corrección puede requerir varias capas. El equipo consumidor puede actualizar la dependencia directa que trae la transitiva, forzar una versión segura si el ecosistema lo permite o reemplazar la biblioteca afectada.</p>
<p>El mantenedor de la dependencia directa también puede necesitar actualizar sus propias dependencias. En proyectos de código abierto, puede ser necesario abrir un reporte de problema, enviar una solicitud de cambios o esperar una versión nueva.</p>
<p>Desde la perspectiva del producto, la responsabilidad operativa recae en quien distribuye o ejecuta el software. Aunque la falla venga de una dependencia transitiva, el equipo debe gestionar el riesgo mientras llega una corrección desde el proyecto mantenedor.</p>
</div>
</details>

<details class="qa">
<summary>Si un CVE no tiene CWE asociado, ¿pierde utilidad para el análisis?</summary>
<div class="respuesta">
<p>No pierde toda utilidad. El CVE sigue identificando una vulnerabilidad pública específica y puede incluir descripción, referencias, versiones afectadas y severidad.</p>
<p>Sin CWE, se pierde una capa de clasificación causal. Es más difícil agrupar el problema con familias de debilidades similares, extraer lecciones de desarrollo seguro o analizar tendencias por tipo de error.</p>
<p>En ese caso conviene revisar la descripción técnica y referencias para inferir la naturaleza de la debilidad, pero evitando etiquetar con demasiada seguridad si la evidencia no alcanza.</p>
</div>
</details>

<details class="qa">
<summary>Si diseñaras una política mínima de gestión de vulnerabilidades para un equipo, ¿qué exigirías?</summary>
<div class="respuesta">
<p>Exigiría escaneo periódico de código propio y dependencias, ejecución en CI/CD, registro de hallazgos, criterios de severidad y responsables claros. También definiría tiempos esperados de remediación según criticidad.</p>
<p>La política debería incluir validación contextual. No todo hallazgo se bloquea automáticamente, pero toda excepción debe documentarse con razón, evidencia, fecha de revisión y responsable.</p>
<p>También exigiría seguimiento. Después de corregir, se debe verificar que el hallazgo desapareció y que no se introdujo regresión. Para dependencias, conviene conservar inventarios o SBOMs que permitan responder ante CVEs nuevos.</p>
</div>
</details>

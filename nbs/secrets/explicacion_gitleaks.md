---
title: "Detección de secretos expuestos con Gitleaks"
---

## Exposición de secretos en código

La exposición de secretos en código ocurre cuando información sensible queda escrita dentro de un repositorio. Un secreto puede ser un token de acceso, una API key, una contraseña, una clave privada, una credencial de base de datos o cualquier valor que permita autenticarse contra un servicio o acceder a un recurso protegido.

Este problema puede aparecer en archivos fuente, archivos de configuración, scripts, variables de entorno copiadas por error, ejemplos de uso, notebooks o historial de commits. El riesgo no depende solo de que el secreto esté en la versión actual del proyecto. Si el valor fue confirmado en un commit anterior, puede seguir existiendo en el historial del repositorio.

La evidencia empírica muestra que este problema no es excepcional. Meli, McNiece y Reaves (2019) analizaron repositorios públicos de GitHub a gran escala y encontraron más de 200.000 secretos únicos, con filtraciones nuevas todos los días. Su trabajo muestra que los secretos expuestos aparecen en código, archivos criptográficos, archivos de datos y archivos de configuración, lo que confirma que la exposición puede ocurrir en distintas partes del repositorio.

Desde la perspectiva de seguridad, la exposición de secretos afecta directamente la **confidencialidad**. Una persona no autorizada que obtiene un secreto válido puede leer datos privados, consultar APIs internas, descargar artefactos, acceder a servicios externos o moverse hacia otros sistemas. Si el secreto además tiene permisos de escritura o administración, el impacto puede extenderse a integridad y disponibilidad.

## Por qué es un problema de seguridad

Un secreto expuesto puede permitir acceso no autorizado sin explotar una vulnerabilidad tradicional del software. El atacante no necesita romper un algoritmo criptográfico ni evadir un mecanismo complejo si ya posee una credencial válida. Por eso, una API key o una clave privada confirmada por error en un repositorio puede transformarse en una vía directa de compromiso.

Meli et al. (2019) estimaron que la mayoría de los secretos descubiertos en su estudio eran sensibles. También observaron que muchos secretos no desaparecen rápidamente después de ser publicados. Incluso cuando una persona elimina el valor de la versión visible del archivo, Git puede conservarlo en commits anteriores. Esto hace que la mitigación correcta no sea solo borrar la línea afectada, sino también revocar o rotar el secreto.

La detección de secretos complementa otros controles de seguridad de aplicaciones. En el marco de [OWASP Top 10](https://owasp.org/www-project-top-ten/), este tipo de revisión ayuda a reducir riesgos asociados a malas configuraciones, exposición de información sensible y fallas en la gestión de credenciales.

## Qué permite hacer Gitleaks

[Gitleaks](https://github.com/gitleaks/gitleaks) es una herramienta de análisis orientada a detectar secretos expuestos en repositorios Git, directorios de trabajo y otros conjuntos de archivos. Su propósito es identificar patrones compatibles con credenciales antes de que sean usados indebidamente o antes de que lleguen a ramas compartidas, servidores remotos o procesos de distribución.

Gitleaks analiza el contenido de los archivos y el historial Git usando reglas de detección. Estas reglas buscan cadenas que se parecen a secretos reales, como tokens de proveedores cloud, claves de APIs, credenciales embebidas, llaves privadas y valores de autenticación asociados a servicios conocidos. Esta estrategia es consistente con la observación de Meli et al. (2019): muchos secretos tienen estructuras distintivas, por ejemplo prefijos, longitudes o encabezados reconocibles, que permiten construir detectores basados en patrones.

Gitleaks puede usarse de forma local durante el desarrollo, como parte de una revisión manual o dentro de un pipeline de integración continua. En todos los casos, el objetivo es identificar secretos presentes en el repositorio para corregirlos antes de que se propaguen o para documentar una exposición que ya ocurrió.

## Problemas que detecta

Gitleaks detecta valores que tienen apariencia de secretos. Entre los casos frecuentes están tokens de acceso personal, API keys de servicios externos, credenciales de plataformas cloud, contraseñas escritas en texto plano, claves privadas SSH, secretos de webhooks, tokens de CI/CD y cadenas de conexión que incluyen usuario y contraseña.

El estudio de Meli et al. (2019) muestra ejemplos concretos de este tipo de exposición: claves de Google, AWS, Twitter, Facebook, MailGun, MailChimp, Stripe, Twilio y claves privadas RSA, EC y PGP. Estos ejemplos son relevantes porque representan credenciales que pueden afectar privacidad, integridad de datos, abuso de servicios, costos económicos o acceso a infraestructura.

Un hallazgo de Gitleaks no significa siempre que el secreto siga activo, pero sí indica que existe una cadena sensible o potencialmente sensible dentro del material analizado. Por eso el resultado debe revisarse y, cuando corresponda, el secreto debe revocarse, rotarse y eliminarse del repositorio y de su historial. Meli et al. (2019) advierten que algunos secretos pueden ser inválidos, de prueba o ya revocados, pero aun así la presencia de un patrón sensible debe tratarse como un evento de seguridad hasta ser verificado.

## Output de Gitleaks

Gitleaks genera resultados estructurados que describen cada hallazgo. En formato JSON, cada resultado incluye campos como la regla que produjo la detección, una descripción del problema, el archivo afectado, la línea donde aparece el valor, el commit asociado cuando aplica, el autor, la fecha, la huella del hallazgo y fragmentos del contenido detectado.

Esta estructura permite revisar los hallazgos de manera manual o integrarlos en herramientas de automatización. El archivo de salida puede almacenarse como evidencia del análisis, procesarse en un pipeline o usarse para priorizar la corrección de secretos expuestos.

La existencia de un output estructurado es importante porque la detección de secretos requiere trazabilidad. Para corregir el problema se necesita saber qué regla se activó, dónde aparece el valor, en qué archivo está y si pertenece al estado actual del repositorio o al historial. Esa información permite distinguir entre un secreto nuevo, un secreto heredado y un falso positivo.

## Uso básico

Un uso básico de Gitleaks sobre el directorio actual es el siguiente:

```bash
gitleaks detect -s . -f json -r results.json
```

El parámetro `detect` ejecuta el análisis de secretos. La opción `-s .` indica que la fuente a revisar es el directorio actual. La opción `-f json` define que el formato de salida será JSON. La opción `-r results.json` guarda los resultados en el archivo `results.json`.

Si Gitleaks encuentra secretos o valores compatibles con reglas de detección, el archivo `results.json` contendrá una lista de hallazgos con la ubicación y los metadatos necesarios para revisarlos. Si no se encuentran hallazgos, el resultado indica que no se detectaron secretos bajo las reglas aplicadas.

## Interpretación de resultados

El resultado de Gitleaks debe interpretarse como una señal de posible exposición. El primer paso es identificar el archivo, la línea y la regla asociada. Luego se debe determinar si el valor corresponde a una credencial real, una credencial de prueba, un ejemplo documentado o un falso positivo.

Cuando el valor corresponde a un secreto real, la acción segura es revocarlo o rotarlo. Borrar el archivo o modificar el commit más reciente no basta si el secreto ya fue publicado. Meli et al. (2019) muestran que los secretos pueden persistir en GitHub y que la detección cercana al momento del commit es importante porque un atacante puede monitorear repositorios públicos casi en tiempo real.

## Referencias

Gitleaks. (s. f.). *Gitleaks*. GitHub. https://github.com/gitleaks/gitleaks

Meli, M., McNiece, M. R., & Reaves, B. (2019). *How bad can it Git? Characterizing secret leakage in public GitHub repositories*. Network and Distributed System Security Symposium.

OWASP Foundation. (s. f.). *OWASP Top Ten*. https://owasp.org/www-project-top-ten/

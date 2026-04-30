

# Casos reales de exposición de secretos

## Uber breach (2016)

En 2016, atacantes accedieron a una cuenta privada de GitHub usada por
Uber y encontraron claves de AWS embebidas en el código. Con esas
credenciales accedieron a un datastore en AWS y descargaron datos de
usuarios y conductores. El secreto expuesto fue una clave de acceso de
AWS almacenada en un repositorio privado. El impacto fue la filtración
de información personal, incluyendo nombres, correos, teléfonos y datos
de licencias de conducir de conductores en Estados Unidos. La Federal
Trade Commission documentó que el acceso se produjo usando una clave
publicada por un ingeniero en un sitio de código compartido (Federal
Trade Commission, 2018).

## Tesla Kubernetes leak (2018)

En 2018, investigadores de RedLock detectaron que una consola de
administración de Kubernetes de Tesla estaba expuesta sin protección por
contraseña. Dentro de un pod se encontraron credenciales para el entorno
AWS de Tesla, lo que permitió acceder a recursos cloud y ejecutar
software de minería de criptomonedas. El secreto expuesto fue credencial
de acceso a AWS disponible desde la infraestructura Kubernetes. El
impacto principal fue el uso no autorizado de capacidad de cómputo en la
nube y la exposición potencial de datos internos, como telemetría
almacenada en S3. Ars Technica reportó el caso con base en los hallazgos
de RedLock (Goodin, 2018).

## Codecov breach (2021)

En 2021, un atacante modificó el Bash Uploader de Codecov para exfiltrar
información desde entornos de integración continua donde se ejecutaba el
script. La modificación enviaba URLs de repositorios Git y variables de
entorno a un servidor controlado por el atacante. Los secretos expuestos
fueron variables de entorno de CI/CD, tokens, claves y credenciales
usadas por proyectos que integraban Codecov en sus pipelines. El impacto
fue el posible compromiso de credenciales de clientes y el acceso no
autorizado a sistemas conectados a esas variables. Codecov publicó un
análisis del incidente y una actualización de seguridad que describen la
modificación maliciosa del uploader y sus efectos sobre variables de
entorno (Codecov, 2021a, 2021b).

## CircleCI breach (2023)

En 2023, CircleCI informó que un atacante comprometió el equipo de un
ingeniero mediante malware y robó una sesión SSO válida protegida por
2FA. Con esa sesión, el atacante accedió a sistemas de producción y
exfiltró datos de clientes. Los secretos expuestos incluyeron variables
de entorno, tokens, claves, OAuth tokens, API tokens y llaves SSH
almacenadas en CircleCI. El impacto fue el riesgo de acceso no
autorizado a sistemas de terceros conectados a esos secretos, por lo que
CircleCI pidió rotar todos los secretos almacenados en la plataforma. El
reporte oficial del incidente describe el alcance, la exfiltración de
claves y las medidas de respuesta (CircleCI, 2023).

## Referencias

CircleCI. (2023, January 12). *CircleCI incident report for January 4,
2023 security incident*.
https://circleci.com/blog/jan-4-2023-incident-report/

Codecov. (2021a). *Post-mortem / root cause analysis (April 2021)*.
https://about.codecov.io/apr-2021-post-mortem/

Codecov. (2021b, April 15). *Bash uploader security update*.
https://about.codecov.io/security-update/

Federal Trade Commission. (2018, April 12). *Uber agrees to expanded
settlement with FTC related to privacy, security claims*.
https://www.ftc.gov/news-events/news/press-releases/2018/04/uber-agrees-expanded-settlement-ftc-related-privacy-security-claims

Goodin, D. (2018, February 20). *Tesla cloud resources are hacked to run
cryptocurrency-mining malware*. Ars Technica.
https://arstechnica.com/information-technology/2018/02/tesla-cloud-resources-are-hacked-to-run-cryptocurrency-mining-malware/

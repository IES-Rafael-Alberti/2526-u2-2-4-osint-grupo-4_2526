# IS 2.d.02 (a) - Auditoría de Superficie de Exposición Post-Incidente (OSINT pasivo)

- Entidad objetivo: Clínica de San Rafael de Cádiz
- Equipo/Grupo: Grupo 4
- Integrantes: Hugo, Jose, Maye, Juan
- Fecha(s) de investigación: 2026-02-01
- Versión: 1.1

## 1. Resumen ejecutivo

**Objetivo.**
El propósito principal de esta auditoría ha sido identificar qué información de la organización se encontraba expuesta públicamente antes del supuesto incidente. Nos hemos centrado en detectar datos que pudieran haber ayudado a un atacante en su fase de reconocimiento, tales como identidades de empleados, vías de contacto, infraestructura tecnológica visible y metadatos olvidados en documentos públicos.

**Hallazgos clave.**
Durante la investigación, hemos encontrado varios puntos de atención que merecen ser destacados:
- **Exposición detallada del personal:** Hemos localizado un listado accesible que expone nombres y cargos de 438 empleados, incluyendo puestos clave como la Dirección Médica. Esto supone una "mina de oro" para ataques de ingeniería social.
- **Servicios internos visibles:** Se han detectado subdominios que apuntan a servicios críticos, como el portal del empleado (`portalempleado.jmpascual.com`) y el correo web, expuestos directamente a Internet.
- **Patrones de contacto claros:** La confirmación del formato de correo corporativo (`@jmpascual.com`) permite a un atacante inferir las direcciones de email de casi cualquier empleado identificado.

**Riesgo global.**
- **Alto.** La combinación de identidades con nombres y apellidos reales, junto con el acceso directo a portales de autenticación, crea un escenario ideal para un ataque dirigido con altas probabilidades de éxito.

**Recomendaciones prioritarias.**
- Como medida urgente, recomendamos revisar la necesidad de tener el listado médico completo accesible de forma pública sin autenticación previa.
- Es vital auditar los accesos remotos (como el portal del empleado) para garantizar que el doble factor de autenticación (2FA) esté activo y sea obligatorio.
- Aconsejamos establecer una rutina de limpieza de metadatos para todos los documentos PDF antes de que sean subidos a la web corporativa.

## 2. Alcance, supuestos y reglas de compromiso

**Alcance.**
Esta auditoría se ha limitado estrictamente a técnicas de OSINT pasivo sobre la entidad. Esto significa que no hemos interactuado con sus sistemas, sino que hemos analizado únicamente la huella que estos dejan en fuentes públicas.

**Fuentes permitidas.**
Para ello, nos hemos valido de motores de búsqueda, registros públicos de internet, redes sociales y el análisis de documentos que la propia organización ha hecho públicos.

**Regla crítica.**
En todo momento se ha respetado la prohibición de realizar acciones activas: no se han lanzado escaneos, no se ha intentado iniciar sesión en ningún portal y no se ha generado tráfico directo contra la infraestructura del objetivo.

**Minimización y privacidad.**
- Hemos tenido cuidado de no incluir datos personales sensibles en este informe más allá de lo necesario para demostrar el riesgo.
- En los casos donde aparecen datos de terceros, los hemos tratado con la confidencialidad requerida.

## 3. Metodología (ciclo OSINT)

A continuación, detallamos paso a paso el proceso que hemos seguido, basándonos en el ciclo de inteligencia OSINT estándar.

### 3.1 Planificación y dirección

Para guiar nuestra investigación, nos planteamos una serie de preguntas clave:
  - ¿Qué huella digital dejan los empleados y la marca en Internet?
  - ¿Es posible deducir cómo se forman los correos electrónicos corporativos?
  - ¿Existen documentos antiguos que revelen información técnica a través de sus metadatos?
  - ¿Hay infraestructura interna que, por error, esté indexada en buscadores?

- **Ventana temporal:** La toma de datos se realizó el 01/02/2026. Todas las pruebas han sido archivadas en la carpeta de evidencias para su consulta.

### 3.2 Identificación de fuentes

Seleccionamos las fuentes que nos aportarían mayor valor sin alertar al objetivo:

| Categoría   | Fuente/Herramienta                  | Qué buscamos                | Enfoque pasivo              |
|-------------|-------------------------------------|-----------------------------|-----------------------------|
| Buscadores  | Google                              | Menciones, archivos PDF     | Uso de Dorks (búsquedas avanzadas) |
| Dominios    | WHOIS/RDAP                          | Propiedad de los dominios   | Consultas a bases de datos públicas |
| RRSS        | LinkedIn/Instagram                  | Empleados y cultura corporativa | Revisión de perfiles públicos |
| Documentos  | Web corporativa                     | Memorias y cuadros médicos  | Descarga directa de archivos públicos |

### 3.3 Adquisición (recopilación)

Comenzamos ejecutando búsquedas específicas, por ejemplo:
  - Buscando todo lo relacionado con el dominio `hospitalespascual.com`.
  - Localizando archivos PDF que contuvieran referencias al dominio de correo `@jmpascual.com`.

Toda la información relevante ha sido capturada y almacenada en el directorio `evidencias/` para garantizar la trazabilidad de nuestros hallazgos.

### 3.4 Procesamiento y organización

Una vez obtenidos los datos, procedimos a organizarlos:
  - Clasificamos la información en tres grandes bloques: Personas (Identidad), Medios de contacto y Tecnología.
  - Procesamos los datos brutos para generar un listado limpio de personal médico (`doctors.json`).

### 3.5 Análisis e interpretación

Al cruzar los datos, encontramos correlaciones interesantes:
  - Al tener la lista de nombres (`doctors.json`) y conocer el formato de los correos (`@jmpascual.com`), un atacante podría generar una lista de emails válida con muy poco margen de error.
  - La existencia pública de subdominios como `portalempleado` sugiere que existe una puerta de entrada para aquellos credenciales que pudieran ser robados mediante phishing.

- **Valoración de riesgo:** Consideramos la situación de riesgo **Alto**, principalmente por la facilidad con la que se puede armar un ataque de ingeniería social muy creíble.

### 3.6 Difusión

Este informe recoge todo lo analizado y presenta recomendaciones prácticas para mitigar los riesgos detectados.

## 4. Herramientas utilizadas

| Herramienta   | Tipo                          | Uso concreto | Salida/evidencia               |
|---------------|-------------------------------|--------------|--------------------------------|
| Scripts OSINT | Recolección                   | Rastreo de dominios y emails | `evidencias/Enlaces.txt` |
| Google Dorks  | Buscador                      | Localización de PDFs olvidados | `evidencias/Memorias-San-Rafael.pdf` |
| Navegación    | Manual                        | Extracción del cuadro médico | `evidencias/doctors.json` |

## 5. Resultados (hallazgos)

### 5.1 Identidades digitales (nicks, perfiles, cuentas)

| Campo           | Contenido                                                                  |
|-----------------|----------------------------------------------------------------------------|
| ID              | A-01                                                                       |
| Categoría       | Identidad                                                                  |
| Descripción     | Hemos podido descargar un listado completo con 438 registros de empleados. Detalla nombres completos y cargos específicos (ej. Director Médico, Jefes de Servicio), lo cual expone la jerarquía interna de la clínica. |
| Evidencia       | [Cuadro Médico (JSON)](../evidencias/doctors.json)                         |
| Fecha evidencia | 2026-02-01                                                                 |
| Impacto         | Esta información facilita enormemente los ataques de "Whaling" (phishing a directivos) o "Spear Phishing", ya que el atacante puede dirigirse a la víctima por su nombre y cargo real, ganándose su confianza. |
| Riesgo          | Alto                                                                       |
| Recomendación   | Se debería evaluar si es estrictamente necesario que este listado sea indexable por buscadores. Una opción sería protegerlo tras un login o mostrar solo la información esencial para el paciente. |

### 5.2 Datos de contacto (emails, teléfonos, estructuras)

| Campo           | Contenido                                                                  |
|-----------------|----------------------------------------------------------------------------|
| ID              | A-02                                                                       |
| Categoría       | Contacto                                                                   |
| Descripción     | Hemos identificado el patrón de construcción de correos corporativos: `@jmpascual.com`. También encontramos direcciones funcionales expuestas, como `cadiz.secretaria@jmpascual.com`. |
| Evidencia       | [Enlaces Recopilados](../evidencias/Enlaces.txt)                           |
| Fecha evidencia | 2026-02-01                                                                 |
| Impacto         | Conocer el patrón de correo permite enviar malware o correos fraudulentos a toda la plantilla sin necesidad de conocer sus direcciones de antemano (fuerza bruta de usuarios). |
| Riesgo          | Medio                                                                      |
| Recomendación   | Es fundamental contar con filtros antispam robustos. Además, recomendamos sustituir las direcciones de correo publicadas en la web por formularios de contacto protegidos con Captcha. |

### 5.3 Dominios, subdominios y huella DNS (pasivo)

| Campo           | Contenido                                                                  |
|-----------------|----------------------------------------------------------------------------|
| ID              | A-03                                                                       |
| Categoría       | Dominio-DNS                                                                |
| Descripción     | Detectamos subdominios que apuntan a servicios de gestión interna: `portalempleado`, `correo` (webmail), `pruebasdiagnosticas` y `ftp`. La IP asociada es `185.186.170.111`. |
| Evidencia       | [Enlaces Recopilados](../evidencias/Enlaces.txt)                           |
| Fecha evidencia | 2026-02-01                                                                 |
| Impacto         | Exponer paneles de administración a Internet aumenta drásticamente la superficie de ataque. Si un atacante consigue credenciales, tiene una puerta directa para entrar. |
| Riesgo          | Alto                                                                       |
| Recomendación   | Lo ideal es que estos paneles estén accesibles solo vía VPN. Si deben ser públicos, es obligatorio implementar autenticación de múltiples factores (MFA). |

### 5.4 Huella documental y metadatos (documentos públicos)

| Campo           | Contenido                                                                  |
|-----------------|----------------------------------------------------------------------------|
| ID              | A-04                                                                       |
| Categoría       | Documentos-Metadatos                                                       |
| Descripción     | Encontramos documentos corporativos indexados, como las "Memorias San Rafael". Estos archivos suelen contener metadatos técnicos (usuario que creó el archivo, software utilizado) que no han sido limpiados. |
| Evidencia       | [Memorias San Rafael](../evidencias/Memorias-San-Rafael.pdf)               |
| Fecha evidencia | 2026-02-01                                                                 |
| Impacto         | Aunque parece menor, la fuga de metadatos puede revelar versiones de software vulnerables o nombres de usuario internos que ayudan a un atacante a planificar su intrusión. |
| Riesgo          | Medio                                                                      |
| Recomendación   | Implementar un proceso de "higienización" de documentos. Antes de publicar cualquier PDF, se deben borrar sus metadatos automáticamente. |

## 6. Resumen de riesgos

| ID   | Hallazgo (resumen) | Riesgo | Prioridad | Acción recomendada |
|------|--------------------|--------|-----------|--------------------|
| A-01 | Exposición masiva de empleados | Alto   | P1        | Limitar exposición y concienciar |
| A-02 | Emails y patrones expuestos | Medio  | P2        | Ocultar emails y filtrar spam |
| A-03 | Paneles (portal empleado) expuestos | Alto   | P1        | MFA obligatorio y/o VPN |
| A-04 | Documentos públicos históricos | Medio  | P3        | Limpieza de metadatos |

## 7. Conclusiones

Tras nuestro análisis, concluimos que:
- La organización presenta una **exposición crítica de su personal**. Al tener nombres, cargos y posibles emails accesibles, son un blanco fácil (y atractivo) para ciberdelincuentes.
- La infraestructura crítica, como el **portal del empleado y el correo web**, está "a tiro de piedra" desde Internet. Si no están fuertemente protegidos (MFA), suponen un riesgo inaceptable.
- En resumen, con la información recopilada en unas pocas horas, un atacante motivado tendría todo lo necesario para lanzar una campaña de **Phishing** muy efectiva.

## 8. Recomendaciones

Para mitigar estos riesgos, sugerimos el siguiente plan de acción:

**Victorias rápidas (0-30 días)**
- Retirar o proteger bajo contraseña los listados detallados del personal médico (JSON).
- Revisar urgentemente que el `portalempleado` y el acceso al correo requieran un segundo factor de autenticación.
- Solicitar a Google la desindexación de documentos antiguos que ya no deberían ser públicos.

**Medio plazo (1-3 meses)**
- Establecer una política automática que limpie los metadatos de cualquier documento antes de hacerlo público.
- Realizar formaciones de concienciación sobre ingeniería social, especialmente para el personal directivo identificado.

**Mejora continua**
- Mantener una vigilancia activa sobre qué se publica de la marca en Internet y revisar periódicamente los subdominios activos.

## 9. Anexos

### 9.1 Evidencias (índice)

A continuación enlazamos los ficheros utilizados como prueba:
- `evidencias/`:
  - `doctors.json`: El archivo que contiene el listado completo del personal.
  - `Enlaces.txt`: El resultado de nuestras herramientas de recolección de dominios.
  - `Memorias-San-Rafael.pdf`: Ejemplo de documento corporativo público analizado.

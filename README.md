Objetivo del Desafío

El objetivo de este desafío es desarrollar un pipeline declarativo en Jenkins que permita automatizar la creación de usuarios en un sistema Linux. Este pipeline debe ser capaz de tomar datos de entrada, generar contraseñas temporales y facilitar la gestión de usuarios para el área de seguridad de la empresa.

Escenario
El área de seguridad de la empresa es responsable de gestionar la creación y baja de usuarios en los sistemas. Debido a errores humanos en la creación de usuarios, se ha solicitado la automatización de este proceso mediante un job en Jenkins. Este job debe garantizar que los usuarios se creen de manera consistente y sin errores.

Requisitos del Pipeline
El operador de seguridad debe proporcionar los siguientes datos para crear un usuario:
Dato	                Descripción
Login	                Identificador único compuesto por el nombre y apellido del usuario.
Nombre y Apellido	Nombre completo del usuario.
Departamento	        Grupo al que pertenece el usuario. Los grupos disponibles son: contabilidad, finanzas y tecnología. En caso de que no exista lo vamos a crear. 

Generación de Contraseña Temporal:
•	El pipeline debe generar una contraseña temporal para el usuario.
•	Esta contraseña debe ser asignada al usuario y el sistema debe obligar al usuario a cambiarla en su primer inicio de sesión.

Entregables
•	Código Fuente del Pipeline:
El código fuente del pipeline de Jenkins está publicado en un repositorio de Github.

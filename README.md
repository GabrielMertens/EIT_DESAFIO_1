Objetivo del Desafío

El objetivo de este desafío es desarrollar un pipeline declarativo en Jenkins que permita automatizar la creación de usuarios en un sistema Linux. Este pipeline debe ser capaz de tomar datos de entrada, generar contraseñas temporales y facilitar la gestión de usuarios para el área de seguridad de la empresa.

Escenario

El área de seguridad de la empresa es responsable de gestionar la creación y baja de usuarios en los sistemas. Debido a errores humanos en la creación de usuarios, se ha solicitado la automatización de este proceso mediante un job en Jenkins. Este job debe garantizar que los usuarios se creen de manera consistente y sin errores.

Requisitos del Pipeline

El operador de seguridad debe proporcionar los siguientes datos para crear un usuario:
Dato	                

Descripción: Login      
Identificador único compuesto por el nombre y apellido del usuario.
Nombre y Apellido	Nombre completo del usuario.
Departamento: Grupo al que pertenece el usuario. Los grupos disponibles son: contabilidad, finanzas y tecnología. En caso de que no exista lo vamos a crear. 

Generación de Contraseña Temporal

•	El pipeline debe generar una contraseña temporal para el usuario.
•	Esta contraseña debe ser asignada al usuario y el sistema debe obligar al usuario a cambiarla en su primer inicio de sesión.

Entregables

•	Código Fuente del Pipeline:
El código fuente del pipeline de Jenkins está publicado en un repositorio de Github.


GUA DE USO

# Jenkins Pipeline para Crear Usuarios en Linux

Este repositorio contiene un pipeline de Jenkins que automatiza la creación de usuarios en un sistema Linux. El pipeline solicita parámetros como el nombre de usuario, nombre completo y departamento, genera una contraseña temporal y crea el usuario en el sistema.

---

## **Requisitos Previos**
Antes de utilizar este pipeline, asegúrate de tener lo siguiente:

1. **Jenkins**: Una instancia de Jenkins instalada y configurada.
2. **Agente de Jenkins**: Un agente con permisos de superusuario (`sudo`) para ejecutar comandos como `groupadd` y `useradd`.
3. **Git**: El repositorio debe estar clonado en tu servidor Jenkins o configurado para ser accedido desde Jenkins.
4. **Plugins de Jenkins**: Asegúrate de tener instalados los siguientes plugins:
   - **Pipeline**
   - **Git**
   - **Credentials Binding** (opcional, para manejar credenciales de forma segura).

# Objetivo del Desafío

El objetivo de este desafío es desarrollar un pipeline declarativo en Jenkins que permita automatizar la creación de usuarios en un sistema Linux. Este pipeline debe ser capaz de tomar datos de entrada, generar contraseñas temporales y facilitar la gestión de usuarios para el área de seguridad de la empresa.

## **Escenario**
El área de seguridad de la empresa es responsable de gestionar la creación y baja de usuarios en los sistemas. Debido a errores humanos en la creación de usuarios, se ha solicitado la automatización de este proceso mediante un job en Jenkins. Este job debe garantizar que los usuarios se creen de manera consistente y sin errores.

## **Requisitos del Pipeline**
El operador de seguridad debe proporcionar los siguientes datos para crear un usuario:
               

Descripción: Login      
Identificador único compuesto por el nombre y apellido del usuario.
Nombre y Apellido	Nombre completo del usuario.
Departamento: Grupo al que pertenece el usuario. Los grupos disponibles son: contabilidad, finanzas y tecnología. En caso de que no exista lo vamos a crear. 

## **Generación de Contraseña Temporal**
•	El pipeline debe generar una contraseña temporal para el usuario.
•	Esta contraseña debe ser asignada al usuario y el sistema debe obligar al usuario a cambiarla en su primer inicio de sesión.

## **Entregables**
•	Código Fuente del Pipeline:
El código fuente del pipeline de Jenkins está publicado en un repositorio de Github.


# GUA DE USO

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

---

## **Configuración del Pipeline en Jenkins**

### **1. Crear un Nuevo Job en Jenkins**
1. Inicia sesión en Jenkins.
2. Haz clic en **"New Item"** (Nuevo ítem).
3. Asigna un nombre al job, por ejemplo: `Crear-Usuario-Pipeline`.
4. Selecciona **"Pipeline"** y haz clic en **"OK"**.

### **2. Configurar el Pipeline desde GitHub**
1. En la configuración del job, desplázate hasta la sección **"Pipeline"**.
2. Selecciona **"Pipeline script from SCM"** (Script de pipeline desde SCM).
3. En **"SCM"**, selecciona **"Git"**.
4. En **"Repository URL"**, ingresa la URL de este repositorio publico: https://github.com/GabrielMertens/EIT_DESAFIO_1
5. En **"Branches to build"**, especifica la rama que deseas usar (por ejemplo, `main`).
6. En **"Script Path"**, ingresa la ruta al archivo `Jenkinsfile` (en este caso, simplemente `Jenkinsfile`).
7. Guarda la configuración.

---

## **Ejecutar el Pipeline**

### **1. Ejecución Manual**
1. En la página principal del job, haz clic en **"Build Now"** (Construir ahora).
2. Ingresa los siguientes parámetros:
- **LOGIN**: El nombre de usuario (por ejemplo, `juan.perez`).
- **FULL_NAME**: El nombre completo del usuario (por ejemplo, `Juan Perez`).
- **DEPARTMENT**: El departamento del usuario (elige entre `contabilidad`, `finanzas` o `tecnologia`).
3. Haz clic en **"Build"**.

### **2. Ejecución Automática (Opcional)**
Si has configurado un **webhook** en GitHub, el pipeline se ejecutará automáticamente cada vez que se realice un `push` al repositorio.

---

## **Etapas del Pipeline**

El pipeline consta de las siguientes etapas:

1. **Mostrar parámetros**:
- Muestra los parámetros ingresados por el usuario.

2. **Generar contraseña temporal**:
- Genera una contraseña temporal utilizando `openssl rand`.

3. **Crear usuario en Linux**:
- Crea el usuario en el sistema Linux y lo asigna al grupo correspondiente.

4. **Notificar al operador**:
- Muestra un resumen de la operación, incluyendo la contraseña temporal generada.

---

## **Ejemplo de Uso**

### **Parámetros de Entrada**
- **LOGIN**: `juan.perez`
- **FULL_NAME**: `Juan Perez`
- **DEPARTMENT**: `finanzas`

### **Salida Esperada**
==========================================
Parámetros ingresados:
LOGIN: juan.perez
FULL_NAME: Juan Perez
DEPARTMENT: finanzas
Contraseña temporal generada: LNxYbftkAeMbrQE0
Grupo finanzas creado.
Usuario juan.perez creado con éxito.
Resumen de la operación:
El usuario juan.perez ha sido creado con éxito.
Contraseña temporal: LNxYbftkAeMbrQE0
Por favor, envíe esta contraseña al usuario final por correo electrónico.

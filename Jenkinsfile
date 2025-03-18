pipeline {
    agent any

    parameters {
        string(name: 'LOGIN', defaultValue: '', description: 'Ingresa el login del usuario (nombre.apellido)')
        string(name: 'FULL_NAME', defaultValue: '', description: 'Ingresa el nombre y apellido del usuario')
        choice(name: 'DEPARTMENT', choices: ['contabilidad', 'finanzas', 'tecnologia'], description: 'Selecciona el departamento del usuario')
    }

    environment {
        TEMP_PASSWORD = ""
    }

    stages {
        stage('Mostrar parámetros') {
            steps {
                script {
                    echo "=========================================="
                    echo "Parámetros ingresados:"
                    echo "LOGIN: ${params.LOGIN}"
                    echo "FULL_NAME: ${params.FULL_NAME}"
                    echo "DEPARTMENT: ${params.DEPARTMENT}"
                    echo "=========================================="
                }
            }
        }

        stage('Generar contraseña temporal') {
            steps {
                script {
                    TEMP_PASSWORD = sh(script: 'openssl rand -base64 12', returnStdout: true).trim()
                    echo "Contraseña temporal generada: ${TEMP_PASSWORD}"
                }
            }
        }

        stage('Crear usuario en Linux') {
            steps {
                script {
                    sh """
                        if ! getent group ${params.DEPARTMENT} > /dev/null 2>&1; then
                            sudo groupadd ${params.DEPARTMENT} || { echo "Error al crear el grupo"; exit 1; }
                            echo "Grupo ${params.DEPARTMENT} creado."
                        else
                            # Si el grupo ya existe, muestra un mensaje
                            echo "El grupo ${params.DEPARTMENT} ya existe."
                        fi
                    """

                    sh """
                        sudo useradd -m -c "${params.FULL_NAME}" -s /bin/bash -p \$(openssl passwd -1 ${TEMP_PASSWORD}) ${params.LOGIN} || { echo "Error al crear el usuario"; exit 1; }
                        sudo usermod -aG ${params.DEPARTMENT} ${params.LOGIN}
                        echo "Usuario ${params.LOGIN} creado con éxito."
                    """
                }
            }
        }

        stage('Notificar al operador') {
            steps {
                script {
                    echo "=========================================="
                    echo "Resumen de la operación:"
                    echo "El usuario ${params.LOGIN} ha sido creado con éxito."
                    echo "Contraseña temporal: ${TEMP_PASSWORD}"
                    echo "Por favor, envíe esta contraseña al usuario final por correo electrónico."
                    echo "=========================================="
                }
            }
        }
    }
}

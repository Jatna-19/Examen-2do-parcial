# LABORATORIO DE AUTOMATIZACIÓN CON ANSIBLE Y DOCKER

## 1. Objetivo de la práctica

Implementar un entorno de administración automatizada utilizando Ansible y Docker, mediante la creación de dos contenedores con Ubuntu 24.04.

La práctica tiene como objetivo aprender a administrar servidores de manera automatizada, utilizando inventarios y playbooks, así como ejecutar tareas mediante módulos, ciclos (`loop`) y condiciones (`when`).

## 2. Herramientas utilizadas

- Docker Desktop.
- Ubuntu 24.04.
- WSL Ubuntu.
- Ansible Core 2.20.1.
- Python 3.

## 3. Estructura del proyecto

```text
ansible-lab/
│
├── docker-compose.yml
├── inventory.ini
├── playbook.yml
├── README.md
│
└── capturas/
    └── ejecucion-playbook.png
```

## 4. Configuración de los contenedores

Se crearon dos contenedores utilizando la imagen Ubuntu 24.04:

- **server1**
- **server2**

Ambos contenedores fueron configurados para permanecer activos y permitir su administración mediante Ansible.

También se instaló Python 3 en ambos servidores para permitir la ejecución de las tareas automatizadas.

## 5. Configuración del inventario

Se creó el archivo `inventory.ini` para registrar los servidores que serán administrados por Ansible.

Contenido:

```ini
[docker]
server1 ansible_connection=docker
server2 ansible_connection=docker
```

## 6. Tareas realizadas con Ansible

Mediante el archivo `playbook.yml` se realizaron las siguientes tareas:

1. Recopilar información de los servidores.
2. Mostrar el nombre de cada servidor.
3. Mostrar el sistema operativo y su versión.
4. Crear el directorio principal `/tmp/ansible-demo`.
5. Crear el archivo `info.txt` con información del servidor.
6. Crear los directorios `logs`, `backup` y `config` mediante un ciclo `loop`.
7. Utilizar una condición `when` para mostrar un mensaje cuando el sistema operativo sea Ubuntu.

## 7. Comandos para iniciar los contenedores

Para iniciar los contenedores desde la terminal de Ubuntu (WSL), ejecutar:

```bash
docker compose up -d
```

Para comprobar que los contenedores estén activos:

```bash
docker ps
```

## 8. Comandos para ejecutar el playbook

Para comprobar que la sintaxis del playbook sea correcta:

```bash
ansible-playbook -i inventory.ini playbook.yml --syntax-check
```

Para comprobar la conexión con los servidores:

```bash
ansible docker -i inventory.ini -m ping
```

Para ejecutar el playbook en ambos servidores:

```bash
ansible-playbook -i inventory.ini playbook.yml
```

## 9. Evidencia de ejecución exitosa

A continuación, se presenta la captura de pantalla correspondiente a la ejecución del playbook de Ansible.

En ella se observa que las tareas se ejecutaron correctamente en los dos servidores y que ambos finalizaron sin errores.

### Captura de pantalla de la ejecución

**Figura 1. Ejecución exitosa del playbook en los servidores Ubuntu.**

!Ejecución exitosa del playbook ![alt text](image.png)

### Resultado obtenido

| Servidor | Tareas correctas | Cambios | Errores |
|---|---:|---:|---:|
| server1 | 7 | 0 | 0 |
| server2 | 7 | 0 | 0 |

El resultado de `PLAY RECAP` confirmó que ambos servidores finalizaron correctamente, con `failed=0` y `unreachable=0`.

## 10. Conclusión

La realización de esta práctica permitió conocer y aplicar herramientas de automatización de servidores mediante Ansible y Docker.

Se logró configurar dos contenedores Ubuntu 24.04, establecer la conexión entre ellos y ejecutar correctamente diferentes tareas administrativas mediante un playbook.

También se practicó el uso de inventarios, módulos, ciclos y condiciones, comprobando la utilidad de Ansible para automatizar la administración de varios servidores.

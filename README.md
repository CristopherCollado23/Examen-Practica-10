# Laboratorio de Ansible con Docker

## Objetivo
Implementar un laboratorio de automatización utilizando Ansible y Docker, administrando dos servidores Ubuntu 24.04 desde un entorno Ubuntu en WSL 2.

## Estructura del proyecto

```text
ansible-lab/
├── docker-compose.yml
├── inventory.ini
├── playbook.yml
└── README.md
```

## Requisitos
- Docker Desktop
- Ubuntu en WSL 2
- Ansible
- Colección community.docker
- Python 3
- Docker SDK para Python

## Iniciar los servidores

Ejecutar desde la carpeta del proyecto:

```bash
docker compose up -d
```

Verificar que los contenedores estén activos:

```bash
docker ps
```

## Instalar dependencias

```bash
sudo apt update
sudo apt install -y ansible python3-docker
ansible-galaxy collection install community.docker
```

## Verificar la conexión

```bash
ansible docker -i inventory.ini -m ping
```

Los servidores deben responder correctamente con `pong`.

## Ejecutar el Playbook

```bash
ansible-playbook -i inventory.ini playbook.yml
```

## Tareas realizadas

El playbook automatiza las siguientes tareas en ambos servidores:

1. Mostrar el nombre del servidor.
2. Mostrar el sistema operativo.
3. Crear el directorio `/tmp/ansible-demo`.
4. Crear el archivo `info.txt` con información del servidor.
5. Crear los directorios `logs`, `backup` y `config` mediante un loop.
6. Mostrar un mensaje únicamente cuando el sistema operativo sea Ubuntu.

## Verificar los Resultados

docker exec server1 ls -R /tmp/ansible-demo
docker exec server2 cat /tmp/ansible-demo/info.txt
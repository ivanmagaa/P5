# Redes e Contedores en Docker e Docker Compose
## P5. DNS - Docker Compose

 ### 1. Arquivo `docker-compose.yml`
 No arquivo `docker-compose.yml`, configuramos o contedor de BIND9 para funcionar como servidor
 DNS autoritativo. Os volumes e portos configurados permiten que o contedor xestione consultas
 DNS e rexistre logs.
 ### Configuración básica:
 ```yaml
 version: '3.8'
 services:
  bind9:
    image: internetsystemsconsortium/bind9:9.18
    container_name: bind9
    restart: always
    ports:
      - "53:53/udp"
Configuración básica de BIND9 con Docker Compose
      - "53:53/tcp"
      - "127.0.0.1:953:953/tcp"
    volumes:
      - ./etc_bind:/etc/bind
      - ./cache_bind:/var/cache/bind
      - ./lib_bind:/var/lib/bind
      - ./log_bind:/var/log
 ```
 ### Explicación das opcións principais:- `image`: Define a imaxe oficial de BIND9 (versión 9.18).- `container_name`: Nome asignado ao contedor.- `restart`: Reinicia automaticamente o contedor en caso de falla.- `ports`: Especifica os portos necesarios para consultas DNS e control remoto.- `volumes`: Monta os directorios locais no contedor para gardar configuracións e logs.
 ### Como usar
 1. Crea os directorios locais necesarios:
   ```bash
   mkdir -p etc_bind cache_bind lib_bind log_bind
   ```
Configuración básica de BIND9 con Docker Compose
 2. Inicia o contedor:
   ```bash
   docker-compose up -d
   ```
 3. Verifica que o contedor está en funcionamento:
   ```bash
   docker ps
   ```

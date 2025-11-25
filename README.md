# Guía de Ejecución y Despliegue Local con Docker Compose

Este documento explica cómo ejecutar localmente un entorno completo de **WordPress + MySQL + phpMyAdmin** usando **Docker Desktop** con el archivo `docker-compose.yml`.

---

## Requisitos Previos

Antes de iniciar, asegúrate de tener instalado:

* **Docker Desktop** (Windows, macOS o Linux)
  [https://www.docker.com/products/docker-desktop/](https://www.docker.com/products/docker-desktop/)
* Archivo `docker-compose.yml` ubicado en tu carpeta del proyecto.

Para verificar instalación:

```bash
docker --version
docker compose version
```

---

## Estructura del Proyecto

El Docker Compose define los siguientes servicios:

### 1. **MySQL 8.0**

Base de datos para WordPress.

* Usuario: `wordpress`
* Password: `wordpress`
* Base: `wordpress`
* Puerto interno: `3306`

### 2. **WordPress**

Servidor web PHP+Apache.

* Expuesto en: `http://localhost:8000`
* Monta la carpeta `wp-content` para persistir archivos.
* Carga configuración adicional desde `uploads.ini`.

### 3. **phpMyAdmin**

Cliente web para administrar MySQL.

* Disponible en: `http://localhost:8080`
* Conexión automática al contenedor de MySQL.

---

## Cómo Levantar el Entorno

1. Abrir una terminal en la carpeta donde se encuentra el archivo `docker-compose.yml`.

2. Ejecutar el comando:

```bash
docker compose up -d
```

Esto descargará las imágenes (solo la primera vez) y levantará todos los servicios en segundo plano.

3. Verificar contenedores activos:

```bash
docker ps
```

4. Acceso a los servicios:

* **WordPress:** [http://localhost:8000](http://localhost:8000)
* **phpMyAdmin:** [http://localhost:8080](http://localhost:8080)

---

## Detener los Servicios

Para detener los contenedores sin eliminarlos:

```bash
docker compose stop
```

Para apagarlos y liberar recursos:

```bash
docker compose down
```

Si deseas limpiar volúmenes (incluye borrar base de datos):

```bash
docker compose down -v
```

> ADVERTENCIA *Esto eliminará por completo los datos de MySQL.*

---

## Persistencia de Datos

Este entorno persiste datos mediante:

* Volumen `db_data` → Almacena MySQL.
* Carpeta `./wp-content` → Almacena archivos de WordPress.

Esto asegura que al reiniciar contenedores no se pierdan los datos.

---

## Notas Importantes

* Puedes modificar contraseñas en la sección `environment` del `docker-compose.yml`.
* El archivo `uploads.ini` permite aumentar los límites de carga de archivos en WordPress.
* Para ver logs del servicio WordPress:

```bash
docker compose logs -f wordpress
```

---

## 💡 Tips

* Si WordPress tarda en iniciar, MySQL puede estar inicializando. Solo espera unos segundos.
* Si cambias puertos del host, revisa que no estén siendo utilizados por otro programa.

---

## ✔️ Listo

El entorno local de WordPress con Docker está completamente configurado y listo para usar.

---

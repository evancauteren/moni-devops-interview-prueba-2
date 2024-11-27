## Prueba 2 - Despliegue de una aplicación Django y React.js

Para ésta prueba del challenge, se realiza un deployment dockerizado de una aplicación Django + React.js.
La solución genera imágenes del backend y del frontend y permite desplegar los correspondientes contenedores junto a una base de datos PostgreSQL.

Se puede probar el código de la siguiente forma:

1. Clonar el repositorio localmente:
```git clone git@github.com:evancauteren/moni-devops-interview-prueba-2.git```
2. Dentro del directorio del repositorio ejecutar lo siguiente para construir las imágenes:
```docker compose build```
3. Una vez finalizado el proceso, para iniciar los contenedores ejecutar:
```docker compose up```
4. Realizar las migraciones del backend:
    - Ingresar al contenedor vía SSH:
```docker exec -i -t django_backend bash```
    - Una vez dentro, ejecutar el siguiente comando:
```python manage.py migrate```
5. Reiniciar contenedor del backend.

- Una vez que los contenedores están corriendo, podemos acceder desde un navegador al frontend:
```localhost:3000```
- Y al backend:
```localhost:8000```

#### Prerequisitos:
- Docker Desktop (en macOS y Windows)
- Python
- Node


#### Nota: 
Para poder dockerizar la aplicación se debieron tomar algunas concesiones.

**Backend:**
- Se actualizó a pygraphviz==1.7
- Se debió instalar en la instancia gcc y graphviz-dev
- Se borra psycopg2==2.7.6.1 y se deja sólo psycopg2-binary

**Frontend:**
Ya que el código tiene algunos años, para poder levantarlo con Node18 se agregó en el Dockerfile:
- ENV NODE_OPTIONS=--openssl-legacy-provider
- --force en el npm install para saltar los problemas de dependencias

**Otros:**
- Las credenciales de la BD y la secret_key del backend están en el docker-compose.yml por tratarse de un challenge no pensado para producción.
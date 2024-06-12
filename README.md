
## Dev

1. Clonar el repositorio
2. Crear un .env basado en el .env.template
3. Ejecutar el comando `git submodule update --init --recursive` para reconstruir los sub-módulos
4. Ejecutar el comando `docker compose up --build`


### Pasos para crear los Git Submodules

1. Crear un nuevo repositorio en GitHub
2. Clonar el repositorio en la máquina local
3. Añadir el submodule, donde `repository_url` es la url del repositorio y `directory_name` es el nombre de la carpeta donde quieres que se guarde el sub-módulo (no debe de existir en el proyecto)
```
git submodule add <repository_url> <directory_name>
```
4. Añadir los cambios al repositorio (git add, git commit, git push)
Ej:
```
git add .
git commit -m "Add submodule"
git push
```
5. Inicializar y actualizar Sub-módulos, cuando alguien clona el repositorio por primera vez, debe de ejecutar el siguiente comando para inicializar y actualizar los sub-módulos
```
git submodule update --init --recursive
```
6. Para actualizar las referencias de los sub-módulos
```
git submodule update --remote
```

### Pasos para commitear cambios al submódulo desde el proyecto principal

1. Entrar en el proyecto:
```
cd <submodule>
```
2. Stash a los cambios sin commitear:
```
git stash
```
3. Obtenemos la rama a la que queremos commitear (en nuestro caso main) y nos cambiamos a esa rama:
```
git pull origin main
git checkout main
```
4. Obtenemos los cambios que hemos stasheado:
```
git stash pop
```
5. Commiteamos y pusheamos nuestros cambios a nuestra rama:
```
git add .
git commit -m "<mensaje del commit>"
git push <origin> <main>
```
6. Volvemos a la rama del launcher y commiteamos los cambios del submódulo
```
cd ..
git add .
git commit -m "feat: added changes to submodule"
git push
```


## Importante
Si se trabaja en el repositorio que tiene los sub-módulos, **primero actualizar y hacer push** en el sub-módulo y **después** en el repositorio principal. 

Si se hace al revés, se perderán las referencias de los sub-módulos en el repositorio principal y tendremos que resolver conflictos.



# Prod

1. Clonar el repositorio
2. Crear un .env basado en el .env.template
3. Ejecutar el comando
```
docker compose -f docker-compose.prod.yml build
```

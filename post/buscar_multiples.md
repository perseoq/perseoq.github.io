
# Busqueda de multiples términos y copiar los archivos en un directorio específico

Es simple el código, `find` nos ayuda a buscar los elementos en el directorio actual `.`, mientras que `grep` ayuda a definir que términos estamos buscando, en este caso todos los archivos que contengan `flask` y que contengan una extensión `.pdf`, los archivos resultantes de la búsqueda serán copiados en la carpeta `Documents`

```bash
find . | grep flask | grep .pdf | xargs cp -t /home/user/Documents/
```

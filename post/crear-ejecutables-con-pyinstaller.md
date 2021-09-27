# Crear archivos ejecutables con pyinstaller

flags:

- **--noconsole** > no permite ejecutar la consola cuando se abre a la par una ventana gráfica
- **--icon** > Agrega el icono del ejecutable
- **--onefile** > crea un ejecutable en un solo archivo

Dentro del entorno de python3:

```bash
pyinstaller --noconsole --onefile --icon=file.ico main_file.py
```
El ejecutable se crea dentro de la carpeta `dist`, todos los archivos de imagen, texto, json, xml y bases de datos sqlite3 deben moverse a esta carpeta para probar que funciona correctamente.

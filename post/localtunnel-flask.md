# Instalar y configurar localtunnel para una app de Flask

Lo primero que debemos tener en cuenta es que necesitamos nodejs instalado, acá tengo otro artículo donde están las diferentes versiones para instalar tanto en ubuntu, como en debian.
- [Instalar nodejs](http://helloperseo.party/post/node-js-install.html)

Una vez instalado nodejs, instalamos localtunnel:

```bash
npm install -g localtunnel
```

Ahora creamos nuestro proyecto de Flask
```bash
virtualenv -p python3 f
source f/bin/activate
pip install flask
nano main.py
```

Supongamos que el contenido de nuestro archivo `main.py` en `/home/user/` es: 
```python
#!/home/user/f/bin/python3

from flask import Flask

app = Flask(__name__)
@app.route("/")
def hello_word():
	return "<h1>Hola mundo</h1>"

if __name__=='__main__':
	app.run(debug=True)
```

Ejecutamos nuestra aplicación Flask primero, el comando `chmod +x main.py` sirve para hacer uso de la línea `#!/home/user/f/bin/python3` contenida en nuestro archivo `main.py`.
```bash
chmod +x main.py
./main.py
```

Al ejecutarse nos mostrará algo similar a esto:
```bash
 * Serving Flask app 'main' (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: on
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
 * Restarting with stat
 * Debugger is active!
 * Debugger PIN: ***-***-**
127.0.0.1 - - [31/Dec/2021 08:47:15] "GET / HTTP/1.1" 200 -
127.0.0.1 - - [31/Dec/2021 08:47:16] "GET /favicon.ico HTTP/1.1" 404 -
127.0.0.1 - - [31/Dec/2021 08:48:15] "GET / HTTP/1.1" 200 -
127.0.0.1 - - [31/Dec/2021 08:48:16] "GET /favicon.ico HTTP/1.1" 404 -
```

Ahora sabemos que nuestro proyecto está ejecutandose en `http://127.0.0.1:5000/`, esto nos ayudará para configurar nuestro localtunnel, ya que la configuración quedaria de la siguiente forma:
```bash
lt -s test2345 -p 5000 -l 127.0.0.1
```
Donde `-s` indica nuestro subdominio personalizado, puede ser cualquier cosa que se nos ocurra, sólo recuerda que como es público el servicio algunos subdominios ya están en uso; `-p` es el puerto de nuestro proyecto local de Flask (Django, Bootle, etc); y `-l` es la dirección de nuestro servidor local.

Nos manda la respuesta: 
```bash
your url is: https://test2345.loca.lt
```
Al abrir por primera vez la `url`, nos mostrará una página donde nos pedirá que aceptemos los téminos del servicio, sólo basta con darle click al gran botón azul. Si usamos recurrentemente la `url` ya no nos mostrará la página del `TOS` y su botón azul.


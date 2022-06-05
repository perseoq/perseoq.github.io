# Configurar app de flask en Apache2 con gunicorn en Ubuntu

Prerequisitos:

```bash
(env) pip install flask gunicorn
sudo apt install apache2 -y
sudo a2enmod proxy_http
```
Supongamos que nuestro proyecto está en `/apps/panaderia` y nuestro archivo principal es `main.py` el cual mandaremos llamar desde nuestro archivo `wsgi.py` de la siguiente manera:

```python
from main import app

if __name__=='__main__':
    app.run(debug=True)
```
Lo siguiente sería hacer un servicio de nuestra app la cual la ejecutaremos con gunicorn el cual está instalado en nuestro entorno virtual (dentro de nuestra carpeta `/apps/panaderia/env`) 

```bash
sudo nano /etc/systemd/system/panaderia.service
```

En los parametros de gunicorn dado que nuestra aplicación estará en un `VPS` agregaremos el comando bind que apuntará a `0.0.0.0` y elegiremos un puerto por default gunicorn se ejecuta en el `8000`:

```bash
[Unit]
Description=Panaderia
After=network.target

[Service]
User=ubuntu
Group=ubuntu
WorkingDirectory=/apps/panaderia/env
ExecStart=/apps/panaderia/env/bin/gunicorn -b 0.0.0.0:9092 wsgi:app

[Install]
WantedBy=multi-user.target
```
Pero si tenemos varios sitios tendremos que declarar varios puertos, para este caso usaremos el `9092` de la siguiente forma:

```bash
sudo iptables -I INPUT 6 -m state --state NEW -p tcp --dport 9092 -j ACCEPT
sudo netfilter-persistent save
```
Ahora crearemos un archivo de configuración de `Apache2` llamado `panaderia.conf`:
```bash
sudo nano /etc/apache2/sites-available/panaderia.conf
```
El cual contendrá lo siguiente:

```bash
<VirtualHost *:80>
        ServerAdmin root@ubuntu
        ServerName dominio.com

        ErrorLog ${APACHE_LOG_DIR}/flaskrest-error.log
        CustomLog ${APACHE_LOG_DIR}/flaskrest-access.log combined

        <Location />
                ProxyPass http://0.0.0.0:9092/
                ProxyPassReverse http://0.0.0.0:9092/
        </Location>
</VirtualHost>
```
Lo anterior a través de `ProxyPass` y `ProxyPassReverse` apuntaremos a la url de nuestra aplicación.

Damos de alta nuestro archivo `panaderia.conf` con `a2ensite`:

```bash
sudo a2ensite panaderia
```
Y reiniciamo nuestro servidor para finalmente poder visualizar nuestro sitio con el dominio que le asignamos.

```bash
sudo systemctl restart apache2
```

## Configurar microfono en Gnome3


### Configurar archivo se ALSA

Vamos a siguiente ruta `cd /etc/modprobe.d/` y editamos con nano el archivo `sudo nano alsa-base.conf`

Agregamos la siguiente línea y guardamos:

```bash
options snd_hda_intel model=aspire-headset-mic
```
Lo siguiente es ir a la configuración de sonido en el panel de control de Gnome3 y ahí elegir tu dispositivo de entrada

### Instalar control de volumen 

```bash
sudo apt install pavucontrol
```

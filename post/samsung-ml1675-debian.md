# Crónica de una instalación frustrante (Debian 10 y Samsung ML-1675)

Ya hace unos días había actualizado mi distribución a Debian 10, había hecho todas las configuraciones pertinentes, exceptuando una, la instalación de mi impresora.

En fedora no había tenido ningun problema, puesto que con los `drivers ULD` siempre habia quedado perfecto y en Ubuntu funcionaba con un archivo `.ppd` que tenia guardado el 1860 rshev 2.0.

Ayer por la noche me dispuse a instalar la impresora pensando que iba a ser igual de sencillo que en ubuntu, pero ¡Oh mi sorpresa! no lo fue. Lo primero que hice fue dar de alta una `CUPS BRF Printer` para después ingresar el archivo `.ppd`, conecté mi impresora y mandé el archivo a impresión… no hizo nada; Revisé el cable y los leds rojo/naranja seguían parpadeando cada que ponía y quitaba las hojas; Cambié el toner y nada. Después de 6 horas de lectura, decidí instalar el driver ULD, todo iba normal, volví mandar la impresión y empezó a imprimir, al acercarme y revisar ahí estaba el terrorífico error que toda impresora SAMSUNG manda cuando su driver que es para ESA IMPRESORA resulta ser incompatible. El famoso `INTERNAL ERROR == uw_color == 4`.

Al menos sabía que mis toners aún servían, pero aún no encontraba ninguna solución a mi problema, hasta le moví al cups desde el `http://localhost:631` y NADA. De repente veo el título estando ahí y me percato que la versión es `2.2.10`, de nuevo empecé la busqueda de alguna solución para la instalación, y fue ahí donde me encontré la página https://github.com/rshev/SpliXextras donde te decía paso a paso que debías hacer:

1.- Inslatar:
```bash
sudo apt-get install printer-driver-splix
```
2.- Descargar el archivo y descomprimir el zip
```bash
https://github.com/rshev/SpliXextras/archive/master.zip
```
3.- Inslatar el archivo `ml1860.ppd`

# No se puede copiar archivos en una partición o en usb

### Solución

Instalamos el paquete necesario:

```bash
sudo apt install ntfs-3g
```

Solucionamos el problema con el comando: 

```bash
sudo ntfsfix /dev/sdX
```

# Guía para Montar y Copiar Archivos desde un Pendrive en Linux

## 1. Verifica que el pendrive esté conectado

Ejecuta el siguiente comando para listar todos los dispositivos de almacenamiento:

```bash
lsblk
```

Busca un dispositivo tipo `/dev/sdb1`, `/dev/sdc1`, etc. Ese suele ser el pendrive.

**Ejemplo de salida:**

```
sdb
└─sdb1   8G
```

## 2. Crea un punto de montaje

Si no existe, crea el directorio donde montarás el pendrive:

```bash
sudo mkdir -p /mnt/usb
```

## 3. Monta el pendrive

Si tu pendrive es `/dev/sdb1`, ejecuta:

```bash
sudo mount /dev/sdb1 /mnt/usb
```

### Solución de problemas: Error con NTFS

Si obtienes un error relacionado con NTFS (sistemas de archivos de Windows), instala el soporte necesario:

```bash
sudo apt install ntfs-3g -y
```

Luego intenta montar nuevamente.

## 4. Copia el contenido a la carpeta que desees

Para copiar todo el contenido del pendrive a `/var/www/html/`:

```bash
sudo cp -r /mnt/usb/* /var/www/html/
```

### Ver el contenido antes de copiar

Si quieres revisar qué archivos hay en el pendrive antes de copiarlos:

```bash
ls /mnt/usb
```

## 5. Desmonta el pendrive (IMPORTANTE)

Una vez terminada la copia, siempre desmonta el pendrive de forma segura:

```bash
sudo umount /mnt/usb
```

---

**Nota:** Recuerda reemplazar `/dev/sdb1` con el dispositivo correcto identificado en el paso 1, y ajusta las rutas de destino según tus necesidades.
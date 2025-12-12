# Instalar Apache en Ubuntu (comandos exactos)

## 1. Actualizar lista de paquetes

```bash
sudo apt update
```

## 2. Instalar Apache

```bash
sudo apt install -y apache2
```

## 3. Habilitar Apache para que inicie al arrancar

```bash
sudo systemctl enable apache2
```

## 4. Iniciar el servicio ahora mismo

```bash
sudo systemctl start apache2
```

## 5. Verificar que está corriendo

```bash
sudo systemctl status apache2
```

Debe mostrar **active (running)**.

## ✅ Abrir el puerto en el firewall (si tienes UFW activo)

### Permitir HTTP (puerto 80)

```bash
sudo ufw allow 80/tcp
```

### Permitir HTTPS (puerto 443) — opcional

```bash
sudo ufw allow 443/tcp
```

### Ver reglas

```bash
sudo ufw status
```
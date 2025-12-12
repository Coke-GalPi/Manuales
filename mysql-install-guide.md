# Instalar y Configurar MySQL en Ubuntu

## 1. Instalar MySQL en Ubuntu

```bash
sudo apt update
sudo apt install mysql-server -y
```

Verifica que el servicio esté funcionando:

```bash
sudo systemctl status mysql
```

Si está **active (running)**, todo ok.

## ✅ 2. Asegurar la instalación (opcional pero recomendado)

Ejecuta:

```bash
sudo mysql_secure_installation
```

Te pedirá configurar cosas como contraseña root, remover usuarios anónimos, etc.

## ✅ 3. Entrar a MySQL como root

```bash
sudo mysql
```

Entrarás al prompt:

```
mysql>
```

## ✅ 4. Crear una base de datos

Por ejemplo:

```sql
CREATE DATABASE midb;
```

## ✅ 5. Crear un usuario para esa base de datos

Ejemplo: usuario `usuario1` con clave `ClaveSegura123`

```sql
CREATE USER 'usuario1'@'%' IDENTIFIED BY 'ClaveSegura123';
```

👉 **`'%'` permite conectar desde cualquier IP.** Si solo desde localhost usa `'localhost'`.

## ✅ 6. Dar permisos al usuario sobre la base de datos

```sql
GRANT ALL PRIVILEGES ON midb.* TO 'usuario1'@'%';
```

Actualizar privilegios:

```sql
FLUSH PRIVILEGES;
```

## ✅ 7. Ver los usuarios creados

```sql
SELECT User, Host FROM mysql.user;
```

## ✅ 8. Probar login con el nuevo usuario

Salir:

```sql
exit;
```

Entrar:

```bash
mysql -u usuario1 -p
```

---

## ⚡ Resumen rápido

| Tarea | Comando |
|-------|---------|
| Instalar MySQL | `sudo apt install mysql-server -y` |
| Entrar a MySQL | `sudo mysql` |
| Crear DB | `CREATE DATABASE nombre;` |
| Crear usuario | `CREATE USER 'user'@'host' IDENTIFIED BY 'pass';` |
| Dar permisos | `GRANT ALL PRIVILEGES ON db.* TO 'user'@'host';` |
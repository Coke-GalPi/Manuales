# Configurar Apache y PHP para Vtiger CRM

## 1. Actualiza el sistema

```bash
sudo apt update && sudo apt upgrade -y
```

## ✅ 2. Instalar Apache (si aún no lo tienes)

```bash
sudo apt install apache2 -y
```

Activa Apache:

```bash
sudo systemctl enable --now apache2
```

## ✅ 3. Instalar PHP (versión recomendada por Vtiger)

- **Para Vtiger 7.5** → PHP 7.4
- **Para Vtiger 8** → PHP 8.1

### ✔ Si estás usando Vtiger 7.5, instala PHP 7.4:

Ubuntu 22.04/24.04 ya no trae PHP 7.4, por lo que debes usar el repositorio de Ondřej:

```bash
sudo apt install -y software-properties-common
sudo add-apt-repository ppa:ondrej/php -y
sudo apt update
```

Ahora instala PHP 7.4 y sus módulos:

```bash
sudo apt install -y php7.4 php7.4-cli php7.4-common php7.4-mysql php7.4-xml php7.4-curl php7.4-gd php7.4-imap php7.4-mbstring php7.4-zip php7.4-soap php7.4-intl php7.4-ldap php7.4-opcache php7.4-bcmath php7.4-json
```

### ✔ Si usas Vtiger 8.x, instala PHP 8.1 (recomendado):

```bash
sudo apt install -y php php-cli php-common php-mysql php-xml php-curl php-gd php-imap php-mbstring php-zip php-soap php-intl php-ldap php-opcache php-bcmath
```

## ✅ 4. Configurar PHP según los requisitos de Vtiger

Edita php.ini:

**PHP 7.4:**

```bash
sudo nano /etc/php/7.4/apache2/php.ini
```

**PHP 8.1:**

```bash
sudo nano /etc/php/8.1/apache2/php.ini
```

Modifica estas líneas (búscalas y cámbialas):

```ini
memory_limit = 512M
max_execution_time = 600
max_input_vars = 10000
post_max_size = 128M
upload_max_filesize = 128M
log_errors = On
display_errors = Off
```

**Guardar** → CTRL+O, Enter, CTRL+X

## ✅ 5. Habilitar módulos de Apache requeridos por Vtiger

```bash
sudo a2enmod rewrite
sudo a2enmod ssl
sudo systemctl restart apache2
```

## ✅ 6. Configurar Apache para permitir .htaccess

Edita:

```bash
sudo nano /etc/apache2/apache2.conf
```

Busca esto:

```apache
<Directory /var/www/>
    AllowOverride None
```

Cambia `None` → `All`:

```apache
<Directory /var/www/>
    AllowOverride All
```

Guardar y reiniciar:

```bash
sudo systemctl restart apache2
```

## ✅ 7. Verificar la versión de PHP

```bash
php -v
```

Debe mostrar **7.4.x** o **8.1.x**, según el Vtiger que uses.

## 🎯 8. Verificar módulos cargados

```bash
php -m
```

Debes ver:
- curl
- dom
- gd
- imap
- intl
- json
- mbstring
- mysqli
- openssl
- xml
- zip
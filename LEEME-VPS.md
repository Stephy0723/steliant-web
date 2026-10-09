# Steliant · Portafolio para VPS

Sitio estático (no necesita Node ni base de datos). Va en la RAÍZ del dominio:

    /index.html            → portafolio principal
    /demos/<proyecto>/     → cada demo

Demos incluidas (8): steliant-ecommerce, steliant-reservas, tour-steliant, steliant-firma,
steliant-legal, steliant-salud, steliant-nexo, steliant-esports.
Las rutas internas usan /demos/..., por eso el sitio debe servirse en la raíz del dominio.

Repositorio: https://github.com/Stephy0723/steliant-web

## 1. Instalar (en el VPS)

    sudo apt install -y git nginx certbot python3-certbot-nginx   # si falta alguno
    sudo git clone https://github.com/Stephy0723/steliant-web.git /var/www/steliant-portafolio

## 2. Nginx

El bloque listo está en `steliant.nginx.conf`. Solo cambia tudominio.com:

    sudo cp /var/www/steliant-portafolio/steliant.nginx.conf /etc/nginx/sites-available/steliant
    sudo nano /etc/nginx/sites-available/steliant          # poner tu dominio
    sudo ln -s /etc/nginx/sites-available/steliant /etc/nginx/sites-enabled/
    sudo nginx -t && sudo systemctl reload nginx

## 3. HTTPS

    sudo certbot --nginx -d tudominio.com -d www.tudominio.com

## Actualizar el sitio

Sube los cambios al repositorio y en el VPS ejecuta:

    cd /var/www/steliant-portafolio && sudo git pull

## Notas

- Esports, Firma, Legal, Nexo y Salud tienen rutas internas (React Router). El bloque de
  Nginx devuelve el index.html de cada demo cuando recargas una subpágina, así no da 404.
- Nginx bloquea la carpeta .git, este archivo y el .conf para que no se publiquen.

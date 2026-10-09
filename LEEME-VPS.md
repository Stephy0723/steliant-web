# Steliant · Portafolio para VPS

Sitio estático (no necesita Node ni base de datos). Se sirve en https://glitchgang.net/demos/

    /demos/                → portafolio principal
    /demos/<proyecto>/     → cada demo

Demos incluidas (8): steliant-ecommerce, steliant-reservas, tour-steliant, steliant-firma,
steliant-legal, steliant-salud, steliant-nexo, steliant-esports.
Las demos buscan sus archivos en /demos/<proyecto>/..., por eso el sitio tiene que ir
justo en /demos/ (ni en la raíz del dominio ni en otra carpeta).

Repositorio: https://github.com/Stephy0723/steliant-web

## 1. Instalar (en el VPS)

    sudo mkdir -p /var/www/steliant
    sudo git clone https://github.com/Stephy0723/steliant-web.git /var/www/steliant/demos

## 2. Nginx

Abre el archivo de glitchgang.net (por ejemplo /etc/nginx/sites-available/glitchgang) y pega
el contenido de `steliant.nginx.conf` DENTRO de su bloque server { }, antes de los demás
location. Si ya tenías un `location /demos/` de antes, bórralo.

    sudo nano /etc/nginx/sites-available/glitchgang
    sudo nginx -t && sudo systemctl reload nginx

## Actualizar el sitio

Sube los cambios al repositorio y en el VPS ejecuta:

    cd /var/www/steliant/demos && sudo git pull

## Notas

- Esports, Firma, Legal, Nexo y Salud tienen rutas internas (React Router). El bloque de
  Nginx devuelve el index.html de cada demo cuando recargas una subpágina, así no da 404.
- El botón "← STELIANT" de cada demo vuelve a /demos/ (el portafolio).
- Nginx bloquea la carpeta .git, este archivo y el .conf para que no se publiquen.

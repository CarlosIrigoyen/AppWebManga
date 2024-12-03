# Usar la imagen oficial de PHP con Apache
FROM php:8.2-apache

# Configurar límites de memoria y tamaño de carga
RUN echo 'memory_limit = 512M' >> /usr/local/etc/php/conf.d/docker-php-memlimit.ini
RUN echo 'upload_max_filesize = 40M' >> /usr/local/etc/php/conf.d/docker-php-uploads.ini

# Instalar dependencias necesarias
RUN apt-get update && apt-get -qq -y install curl --no-install-recommends \
    libpq-dev \
    git \
    unzip \
    libzip-dev \
    zlib1g-dev \
    libfreetype6-dev \
    libjpeg62-turbo-dev \
    libpng-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install -j$(nproc) zip pdo pdo_pgsql bcmath gd sockets

# Instalar Composer
RUN php -r "readfile('https://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer

# Habilitar el módulo de reescritura de Apache
RUN a2enmod rewrite

# Configurar el directorio de trabajo
WORKDIR /var/www

# Copiar los archivos del proyecto
COPY ./ /var/www

# Configurar permisos
RUN chmod -R 0777 /var/www/storage /var/www/bootstrap/cache

# Instalar dependencias de Composer en modo optimizado
RUN composer install --no-dev --optimize-autoloader

# Comando para iniciar Laravel
CMD ["php", "artisan", "serve", "--host=0.0.0.0", "--port=8000"]

# Exponer el puerto 8000
EXPOSE 8000
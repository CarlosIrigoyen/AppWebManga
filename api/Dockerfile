# Utiliza la imagen oficial de PHP con Composer
FROM php:8.3.6-cli

# Instala dependencias necesarias
RUN apt-get update && apt-get install -y \
    git \
    unzip \
    libpng-dev \
    libjpeg62-turbo-dev \
    libfreetype6-dev \
    libpq-dev \
    && docker-php-ext-configure gd --with-freetype --with-jpeg \
    && docker-php-ext-install gd \
    && docker-php-ext-install pdo_pgsql pgsql

# Establece el directorio de trabajo
WORKDIR /var/www

# Copia los archivos del proyecto al contenedor
COPY . .

# Instala Composer si no está instalado
RUN if [ ! -f /usr/local/bin/composer ]; then \
        curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer; \
    fi

# Verifica si las dependencias de Composer están instaladas, si no, las instala
RUN if [ ! -d "vendor" ]; then \
        composer install --no-interaction --prefer-dist; \
    fi

# Expone el puerto que usará la API
EXPOSE 80

# Comando para iniciar el servidor de Laravel
CMD ["php", "artisan", "serve", "--host=0.0.0.0"]

# Base image
FROM php:8.1-fpm

# Install dependencies
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        nginx \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libpng-dev \
        libzip-dev \
        unzip \
        git \
        curl \
        libonig-dev \
        libicu-dev \
        libxml2-dev \
        cron \
        supervisor && \
    docker-php-ext-install -j$(nproc) \
        bcmath \
        gd \
        intl \
        mbstring \
        opcache \
        pdo_mysql \
        soap \
        zip && \
    pecl install -o -f redis && \
    rm -rf /tmp/pear && \
    docker-php-ext-enable redis && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer

# Copy Nginx configuration
COPY nginx.conf /etc/nginx/sites-available/default

# Copy Magento source code to the container
COPY . /var/www/html/

# Set file permissions
RUN chown -R www-data:www-data /var/www/html/
RUN chmod -R 777 /var/www/html/var/
RUN chmod -R 777 /var/www/html/generated/

# Expose port
EXPOSE 80

# Start Nginx and PHP-FPM
CMD service nginx start && php-fpm

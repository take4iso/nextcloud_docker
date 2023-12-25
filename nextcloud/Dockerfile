FROM nextcloud:latest

# install PHP modules bz2, ftp
RUN apt-get update && apt-get install -y \
    libbz2-dev libssl-dev \
    && rm -rf /var/lib/apt/lists/* \
    && docker-php-ext-install bz2 \
    && docker-php-ext-install ftp

# background jobs
RUN echo "*/5 * * * * www-data php -f /var/www/html/cron.php" > /etc/cron.d/nextcloud

# SSL
COPY cert/* /etc/apache2/ssl/
COPY default-ssl.conf /etc/apache2/sites-available/
RUN a2enmod ssl \
    && a2ensite default-ssl

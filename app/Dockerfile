# Use the official Ubuntu image as a base
FROM ubuntu:22.04

# Environment variables for non-interactive installation
ENV DEBIAN_FRONTEND=noninteractive

# Install software-properties-common to manage repositories
RUN apt-get update && \
    apt-get install -y software-properties-common && \
    add-apt-repository ppa:ondrej/php && \
    apt-get update && \
    apt-get install -y apache2 \
                       php8.2 \
                       libapache2-mod-php8.2 \
                       php8.2-mysql \
                       php8.2-cli \
                       php8.2-mbstring \
                       php8.2-xml \
                       php8.2-curl \
                       php8.2-zip \
                       php8.2-intl \
                       php8.2-soap \
                       php8.2-gd \
                       php8.2-xsl \
                       php8.2-imagick \
                       php8.2-imap \
                       php8.2-bcmath \
                       php8.2-bz2 \
                       cron \
                       vim && \
    apt-get clean

# Enable the Apache rewrite module
RUN a2enmod rewrite


# Remove the default Apache index page
RUN rm /var/www/html/index.html

# Copy your application code to the Apache document root
COPY ./src /var/www/html/

# Set the correct permissions for the document root
RUN chown -R www-data:www-data /var/www/html/cwms \
    && chmod -R 777 /var/www/html/cwms


# Expose port 80 to the outside world
EXPOSE 80

# Start cron and Apache in the foreground
CMD apache2ctl -D FOREGROUND
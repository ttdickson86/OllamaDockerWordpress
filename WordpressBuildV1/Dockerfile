# Use the latest official WordPress image as the base
FROM wordpress:latest

# Install UpdraftPlus plugin by default
RUN set -ex; \
    wp plugin install updraftplus --activate --allow-root || \
    curl -o /tmp/updraftplus.zip -L https://downloads.wordpress.org/plugin/updraftplus.latest-stable.zip && \
    unzip /tmp/updraftplus.zip -d /usr/src/wordpress/wp-content/plugins/ && \
    rm /tmp/updraftplus.zip

# Expose port 80
EXPOSE 80
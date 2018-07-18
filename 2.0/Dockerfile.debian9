FROM tomashavlas/php-httpd:7.2-debian9

USER 0

ENV YII2_VERSION=2.0 \
    YII2_RELEASE=2.0.15.1

LABEL name="tomashavlas/yii2" \
      version="${YII2_VERSION}" \
      release="${YII2_RELEASE}" \
      maintaner="Tomáš Havlas <tomas@havlas.me>" \
      vendor="Tomáš Havlas" \
      io.openshift.s2i.scripts-url=image:///usr/lib/s2i

RUN apt-get update \
 && RUNTIME_DEPS=" \
        ca-certificates \
        gettext-base \
        git \
        libmagickwand-6.q16-3 \
        libnss-wrapper \
        libpng16-16 \
        libpq5 " \
 && apt-get install --yes --no-install-recommends --verbose-versions ${RUNTIME_DEPS} \
 \
 && rm --recursive /var/lib/apt/lists/*

RUN apt-get update \
 && BUILD_DEPS=" \
        libmagickwand-dev \
        libpng-dev \
        libpq-dev " \
 && HTTPD_MODULES=" \
        dir \
        rewrite " \
 \
 && PECL_EXTENSIONS=" \
        imagick " \
 && PHP_EXTENSIONS=" \
        gd \
        iconv \
        intl \
        pdo_mysql \
        pdo_pgsql \
        simplexml \
        soap \
        zip " \
 && apt-get install --yes --no-install-recommends --verbose-versions ${BUILD_DEPS} \
 && docker-httpd-module enable ${HTTPD_MODULES} \
 && docker-php-source extract \
 \
 && docker-php-ext-install ${PHP_EXTENSIONS} \
 && pecl install ${PECL_EXTENSIONS} \
 && /usr/lib/container-entrypoint/php-generate-conf_available_d \
 && docker-php-extension enable ${PECL_EXTENSIONS} ${PHP_EXTENSIONS} \
 \
 && docker-php-source delete \
 && apt-get purge --yes --auto-remove ${BUILD_DEPS} \
 && rm --recursive /var/lib/apt/lists/*

RUN apt-get update \
 && BUILD_DEPS=" \
        curl " \
 && apt-get install --yes --no-install-recommends --verbose-versions ${BUILD_DEPS} \
 \
 && curl -sS https://getcomposer.org/installer | php -- \
        --filename=composer.phar \
        --install-dir=/usr/bin \
 \
 && composer.phar clear-cache \
 && apt-get purge --yes --auto-remove ${BUILD_DEPS} \
 && rm --recursive /var/lib/apt/lists/*

RUN RUNTIME_DEPS=" \
        fxp/composer-asset-plugin:^1.4.2 " \
 && composer.phar global require --optimize-autoloader ${RUNTIME_DEPS} \
 && composer.phar global dumpautoload --optimize \
 && composer.phar clear-cache

COPY [ "./common/root", "./root", "./${YII2_VERSION}/root", "/" ]

USER 48

CMD [ "/usr/lib/s2i/usage" ]

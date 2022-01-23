# symfony-api-platform-skeleton

### Simple Template for Symfony API

You can fork it and change the git remote to your Repo
```shell
git remote set-url <your-git-remote-url>
```

installed Packages (inkl. DEV):

|PACKAGE                             |VERSION            |
|:-----------------------------------|------------------:|
|api-platform/core                   |v2.6.8             |
|doctrine/annotations                |1.13.2             |
|doctrine/cache                      |2.1.1              |
|doctrine/collections                |1.6.8              |
|doctrine/common                     |3.2.1              |
|doctrine/dbal                       |3.3.0              |
|doctrine/deprecations               |v0.5.3             |
|doctrine/doctrine-bundle            |2.5.5              |
|doctrine/doctrine-migrations-bundle |3.2.1              |
|doctrine/event-manager              |1.1.1              |
|doctrine/inflector                  |2.0.4              |
|doctrine/instantiator               |1.4.0              |
|doctrine/lexer                      |1.2.2              |
|doctrine/migrations                 |3.4.0              |
|doctrine/orm                        |2.11.0             |
|doctrine/persistence                |2.3.0              |
|doctrine/sql-formatter              |1.1.2              |
|fig/link-util                       |1.2.0              |
|friendsofphp/proxy-manager-lts      |v1.0.5             |
|laminas/laminas-code                |4.5.1              |
|nelmio/cors-bundle                  |2.2.0              |
|nikic/php-parser                    |v4.13.2            |
|phpdocumentor/reflection-common     |2.2.0              |
|phpdocumentor/reflection-docblock   |5.3.0              |
|phpdocumentor/type-resolver         |1.6.0              |
|phpstan/phpdoc-parser               |1.2.0              |
|psr/cache                           |3.0.0              |
|psr/container                       |2.0.2              |
|psr/event-dispatcher                |1.0.0              |
|psr/link                            |2.0.1              |
|psr/log                             |3.0.0              |
|roave/security-advisories           |dev-latest 25a216c |
|symfony/asset                       |v6.0.1             |
|symfony/cache                       |v6.0.2             |
|symfony/cache-contracts             |v3.0.0             |
|symfony/config                      |v6.0.2             |
|symfony/console                     |v6.0.2             |
|symfony/dependency-injection        |v6.0.2             |
|symfony/deprecation-contracts       |v3.0.0             |
|symfony/doctrine-bridge             |v6.0.2             |
|symfony/dotenv                      |v6.0.2             |
|symfony/error-handler               |v6.0.2             |
|symfony/event-dispatcher            |v6.0.2             |
|symfony/event-dispatcher-contracts  |v3.0.0             |
|symfony/expression-language         |v6.0.1             |
|symfony/filesystem                  |v6.0.0             |
|symfony/finder                      |v6.0.2             |
|symfony/flex                        |v2.1.2             |
|symfony/framework-bundle            |v6.0.2             |
|symfony/http-foundation             |v6.0.2             |
|symfony/http-kernel                 |v6.0.2             |
|symfony/maker-bundle                |v1.36.4            |
|symfony/password-hasher             |v6.0.2             |
|symfony/polyfill-intl-grapheme      |v1.24.0            |
|symfony/polyfill-intl-normalizer    |v1.24.0            |
|symfony/polyfill-mbstring           |v1.24.0            |
|symfony/polyfill-php81              |v1.24.0            |
|symfony/property-access             |v6.0.2             |
|symfony/property-info               |v6.0.2             |
|symfony/proxy-manager-bridge        |v6.0.2             |
|symfony/routing                     |v6.0.1             |
|symfony/runtime                     |v6.0.0             |
|symfony/security-bundle             |v6.0.2             |
|symfony/security-core               |v6.0.2             |
|symfony/security-csrf               |v6.0.1             |
|symfony/security-http               |v6.0.2             |
|symfony/serializer                  |v6.0.2             |
|symfony/service-contracts           |v3.0.0             |
|symfony/stopwatch                   |v6.0.0             |
|symfony/string                      |v6.0.2             |
|symfony/translation-contracts       |v3.0.0             |
|symfony/twig-bridge                 |v6.0.2             |
|symfony/twig-bundle                 |v6.0.1             |
|symfony/validator                   |v6.0.2             |
|symfony/var-dumper                  |v6.0.2             |
|symfony/var-exporter                |v6.0.0             |
|symfony/web-link                    |v6.0.1             |
|symfony/web-profiler-bundle         |v6.0.2             |
|symfony/yaml                        |v6.0.2             |
|twig/twig                           |v3.3.7             |
|webmozart/assert                    |1.10.0             |
|willdurand/negotiation              |3.0.0              |

The docker-compose config (Ready to start)
```json
services:
  composer:
    image: composer:2.2.4
    profiles:
        - tools
    volumes:
        - ./:/code:rw
    working_dir: /code
  database:
    environment:
      POSTGRES_DB: app
      POSTGRES_PASSWORD: ChangeMe
      POSTGRES_USER: symfony
    image: postgres:13-alpine
    ports:
        - target: 5432
    volumes:
        - ./docker/db/data:/var/lib/postgresql/data:rw
  nginx:
    depends_on:
        - php
    image: nginx:1.21.5
    ports:
        - published: 80
          target: 80
        - published: 443
          target: 443
    restart: always
    volumes:
        - ./:/code:rw
        - ./docker/nginx/server.conf:/etc/nginx/conf.d/default.conf:ro
  pgadmin:
    environment:
        PGADMIN_DEFAULT_EMAIL: admin@example.org
        PGADMIN_DEFAULT_PASSWORD: Secret
    image: dpage/pgadmin4:4.6
    ports:
        - published: 8080
          target: 80
    restart: always
  php:
    image: php:8.1.2-fpm-buster
    restart: always
    volumes:
        - ./:/code:rw

version: '3'
volumes:
  db-data: {}
```
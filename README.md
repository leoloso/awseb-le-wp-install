# Install WordPress on an AWS Elastic Beanstalk single instance with Let's Encrypt

Bootstrapper to launch WordPress in an AWS Elastic Beanstalk single instance with Let's Encrypt, configurable through environment variables

## Description

This project is ready to be deployed to Elastic Beanstalk under a single instance, featuring:

- WordPress pre-installed, admin area accessible under `/wp/wp-admin/`
- HTTPS through [Let's Encrypt](https://letsencrypt.org/)
- Cronjob to automatically renew the Let's Encrypt certificate
- All information is set through environment variables

## Usage

Via [Composer](https://getcomposer.org):

```bash
composer create-project leoloso/awseb-le-wp-install
```

After bootstrapping this project, add your own code, and deploy!

## Environment variables

Define the following environment variables in the Elastic Beanstalk application's configuration (under entry "Software"), or using CLI command `eb setenv`:

1. WordPress configuration (`wp-config.php`):

```bash
DB_NAME={YOUR_SITE_DB_NAME} #eg: database
DB_USER={YOUR_SITE_DB_USER} #eg: admin
DB_PASSWORD={YOUR_SITE_DB_PASSWORD} #eg: sADF!kl9diq@#Sjfk
DB_HOST={YOUR_SITE_DB_HOST} #eg: 127.0.0.1
SITE_URL_WITHOUT_HTTP={YOUR_SITE_URL_WITHOUT_HTTP} #eg: yourdomain.com
SITE_URL_WITH_HTTP={YOUR_SITE_URL_WITH_HTTP} #eg: https://yourdomain.com
SITE_NAME="{YOUR_SITE_NAME}" #eg: "My awesome website"
ADMIN_USER={ADMIN_USER} #eg: admin
ADMIN_PASSWORD={ADMIN_PASSWORD} #eg: JKo$@sfjASD00w
ADMIN_EMAIL={ADMIN_EMAIL} #eg: pedro@example.com
```

To set the SALT keys there are two alternatives:

I. Set random values through environment variable `SHUFFLE_SALT_KEYS`:

```bash
SHUFFLE_SALT_KEYS=true
```

II. Set the corresponding values directly:

```bash
# Obtain random values from https://api.wordpress.org/secret-key/1.1/salt
AUTH_KEY={YOUR_AUTH_KEY}
SECURE_AUTH_KEY={YOUR_SECURE_AUTH_KEY}
LOGGED_IN_KEY={YOUR_LOGGED_IN_KEY}
NONCE_KEY={YOUR_NONCE_KEY}
AUTH_SALT={YOUR_AUTH_SALT}
SECURE_AUTH_SALT={YOUR_SECURE_AUTH_SALT}
LOGGED_IN_SALT={YOUR_LOGGED_IN_SALT}
NONCE_SALT={YOUR_NONCE_SALT}
```

2. Let's Encrypt configuration:

```bash
LETSENCRYPT_DOMAIN={YOUR_LETSENCRYPT_DOMAIN} # Domain to register: yourdomain.com
LETSENCRYPT_EMAIL={YOUR_EMAIL} # eg: pedro@example.com
LETSENCRYPT_OPTIONS={YOUR_LETSENCRYPT_OPTIONS} # Can be used to pass "--dry-run" to avoid re-registering the certificate when launching a new server instance
```

## Credits

The Let's Encrypt configuration was mostly taken from [Radek Zajkowski](https://twitter.com/konaorange)'s article [Elastic Beanstalk and Let’s Encrypt](https://medium.com/@konaorange/elastic-beanstalk-and-lets-encrypt-74458f072f0c).

Installing WordPress through Composer and WP-CLI is based [another project of mine](https://github.com/leoloso/wp-install).

- [Leonardo Losoviz][link-author]

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

[link-author]: https://github.com/leoloso

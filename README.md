# wp-isc2-chapter-theme

This is a work in progress. We welcome any and all contributions to this project. Please provide feedback on how we can improve this theme, documentation, or code via GitHub Issues for the repo.

## Theme Installation

There are two main methods for installing the theme.

### Manual Installation

1. To install the theme, navigate to your site's `wp-content/themes/` directory. From there you can clone the repository using the following command: `git clone https://github.com/blauwers/wp-isc2-chapter-theme.git`

2. Then navigate to the `Themes` page for your Wordpress install. This pages is usally found at https://yourdomain.org/wp-admin/themes.php

3. Prior to activation, make sure the standard Wordpress theme `Twenty Seventeen` is installed. Activating the theme at this point is as easy as pressing the `Activate` button. Prior to activating the theme, you may wish to preview what the site will look like with this theme activated, this can be done by pressing the `Live Preview` button.

### Installation Via Upload

1. Download the theme as a zip archive from GitHub.

2. Then navigate to the `Themes` page for your Wordpress install. This pages is usally found at https://yourdomain.org/wp-admin/themes.php

3. Click the `Upload Theme` button and follow the instructions for uploading the zip archive.

4. Prior to activation, make sure the standard Wordpress theme `Twenty Seventeen` is installed. Activating the theme at this point is as easy as pressing the `Activate` button. Prior to activating the theme, you may wish to preview what the site will look like with this theme activated, this can be done by pressing the `Live Preview` button.

## Plugins We Use

The Austin (ISC)2 Chapter uses the following plugins to help manage our site. These plugins are part of how we make our site work well for us.

* [Akismet Anti-Spam](https://wordpress.org/plugins/akismet/)
* [Import Eventbrite Events Pro](http://xylusthemes.com/plugins/import-eventbrite-events/)
* [Keyring](https://wordpress.org/plugins/keyring/)
* [Max Mega Menu](https://wordpress.org/plugins/megamenu/)
* [The Events Calendar](https://wordpress.org/plugins/the-events-calendar/)
* [Wordfence Security](https://wordpress.org/plugins/wordfence/)
* [WP Add Mime Types](https://wordpress.org/plugins/wp-smushit/)
* [WP Smush](https://wordpress.org/plugins/wp-smushit/)

## Apache Configuration

We recommend serving your chapter website over https only. There are multiple ways to accomplish this and below is our vhost configuration to use as an example.

```
<Directory "/path/to/site/htdocs">
	Options FollowSymLinks
	AllowOverride All
	Require all granted
</Directory>

<VirtualHost *:80>
	ServerAdmin webmaster@yourdomain.org
	ServerName yourdomain.org
	ServerAlias www.yourdomain.org
	ErrorLog /path/to/log/error_log
	CustomLog /path/to/log/access_log common
	Redirect permanent / https://yourdomain.org
</VirtualHost>

<VirtualHost *:443>
  ServerAdmin webmaster@yourdomain.org
  DocumentRoot /home/yourdomain/htdocs
  ServerName yourdomain.org
  ServerAlias www.yourdomain.org
  ErrorLog /path/to/log/ssl-error_log
  CustomLog /path/to/log/ssl-access_log common

  # SSL Settings
  SSLEngine on
  SSLCertificateFile /etc/letsencrypt/live/yourdomain.org/fullchain.pem
  SSLCertificateKeyFile /etc/letsencrypt/live/yourdomain.org/privkey.pem
  SSLCACertificateFile /etc/letsencrypt/live/yourdomain.org/chain.pem

	# Enable HTTP Strict Transport Security (HSTS)
	Header always set Strict-Transport-Security "max-age=20886400; includeSubDomains;"

	# Set a same origin policy
	Header always set X-Frame-Options SAMEORIGIN

	# Rewrite any session cookies to make them more secure
	Header edit Set-Cookie ^(.*)$ $1;HttpOnly;Secure

	# Prevent browsers doing MIME Type sniffing.
	Header always set X-Content-Type-Options nosniff

</VirtualHost>
```

## Installing WordPress

See [Installing Wordpress](https://codex.wordpress.org/Installing_WordPress).

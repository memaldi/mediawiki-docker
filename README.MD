MediaWiki for Docker
====================

This docker image allows creating a MediaWiki container. You need to create a PostgreSQL container and link the MediaWiki container to it:

```
	docker run -d --link my_postgresql:db --name my_wiki -p 80:80 memaldi/mediawiki
```

Follow the installation wizard and download the LocalSettings.php file. Copy file to container:

```
	docker cp LocalSettings.php my_wiki:/var/www/html/mediawiki
```
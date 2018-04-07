# shiny_nginx

## Usage
* Place your app in the shiny-server/app directory
* In nginx/.htpasswd type in ${username}:${password_hash} for basic auth
* Run <pre>docker-compose up -d
</pre> from the directory containing docker-compose.yml
* Find your app at http://localhost/app

## Shiny Details
* Supports PDF rendering with knitr and markdown through texlive
* Installs and supports many packages related to data science

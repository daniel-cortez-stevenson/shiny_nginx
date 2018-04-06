# shiny_nginx

## Usage
* Place your app in the shiny-server/shiny/your_app directory
* In nginx/.htpasswd type in ${username}:${password_hash} for basic auth
* Run <pre>docker-compose up -d
</pre> from the directory containing docker-compose.yml
* Find your app at http://localhost/app/your_app

## Shiny Details
* Supports PDF rendering with knitr and markdown through texlive
* Installs and supports many packages related to data science

## Docker Images
* Can be pulled (default)
* or build from github files
 * add build directive to docker-compose.yml
 <pre>
    nginx:
      build: ${PWD}/nginx
      ...
    shiny:
      build: ${PWD}/shiny-server
      ...
 </pre>
  * remove <pre>image:${danielstevenson/image:tag}
  </pre>
  from both services.

### Docker URLs
https://cloud.docker.com/swarm/danielstevenson/repository/docker/danielstevenson/nginx4shinyr/general
https://cloud.docker.com/swarm/danielstevenson/repository/docker/danielstevenson/shinyr4datascience/general

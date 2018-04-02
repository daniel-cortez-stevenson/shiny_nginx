FROM r-base:3.4.3

MAINTAINER danielstevenson "daniel.stevenson@charite.de"

# Install dependencies and Download and install shiny server
# Modified from https://hub.docker.com/r/rocker/shiny/
RUN apt-get update && apt-get install -y -t unstable \
    sudo \
    gdebi-core \
    pandoc \
    pandoc-citeproc \
    libcurl4-gnutls-dev \
    libcairo2-dev/unstable \
    libxt-dev && \
    wget --no-verbose https://s3.amazonaws.com/rstudio-shiny-server-os-build/ubuntu-12.04/x86_64/VERSION -O "version.txt" && \
    VERSION=$(cat version.txt) && \
    wget --no-verbose "https://s3.amazonaws.com/rstudio-shiny-server-os-build/ubuntu-12.04/x86_64/shiny-server-$VERSION-amd64.deb" -O ss-latest.deb && \
    gdebi -n ss-latest.deb && \
    rm -f version.txt ss-latest.deb && \
    cp -R /usr/local/lib/R/site-library/shiny/examples/* /srv/shiny-server/ && \
    rm -rf /var/lib/apt/lists/*

# Install system dependencies for rpackages like curl or knitr family and related functions
RUN apt-get update -y && apt-get install -y \
    libcurl4-openssl-dev \
    libssl-dev \
    libmagick++-dev \
    libmariadb-client-lgpl-dev \
    libxml2-dev \
    librsvg2-dev \
    libwebp-dev \
    libpoppler-cpp-dev \
    libssh2-1-dev \
    libv8-3.14-dev \
    libudunits2-dev \
    libpq-dev \
    libgdal-dev \
    libtesseract-dev \
    tesseract-ocr-eng \
    libleptonica-dev

RUN R -e "install.packages(c('shiny', 'plyr', 'dplyr', 'tibble', 'tidyr', 'readr', 'RCurl', 'gtools', 'shinythemes', 'shinycssloaders', 'shinydashboard', 'shinyjs', 'd3heatmap', 'DT', 'scales', 'plotly', 'knitr', 'magick', 'devtools'), repos='https://cran.rstudio.com/', dependencies=TRUE)"
RUN R -e "devtools::install_github(c('hadley/ggplot2', 'bokeh/rbokeh', 'ramnathv/htmlwidgets', 'dreamRs/shinyWidgets', 'haozhu233/kableExtra', 'rstudio/rmarkdown'))"

# Latex support
RUN apt-get update -y && apt-get install -y \
    texlive-latex-base \
    texlive-xetex

# Shiny HTML redirect/404 error, etc.
RUN mkdir -p /etc/shiny-server/templates/ && \
    cp /opt/shiny-server/templates/error.html /etc/shiny-server/templates/


EXPOSE 3838

COPY shiny-server.conf /etc/shiny-server/shiny-server.conf

COPY shiny-server.sh /usr/bin/shiny-server.sh

CMD ["/usr/bin/shiny-server.sh"]

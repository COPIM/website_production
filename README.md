# production repository for the Copim website

Copim's website is built from Markdown files compiled into a website using [Hugo](https://gohugo.io/) static site generator. The website is available in production at [https://copim.ac.uk](https://copim.ac.uk).

This repository contains the Hugo config and the generated site files, the Markdown content files, the configuration files for serving the site through [NGINX](https://www.nginx.com/) web server, and the Docker Compose configuration file for running an instance of Hugo to rebuild the site. It also contains a Git submodule for the bespoke Hugo theme, Inate, available at [https://github.com/COPIM/inate-hugo/](https://github.com/COPIM/inate-hugo/).

To clone the site, this development environment, and its submodule run:

    git clone https://github.com/COPIM/website_production/
    git submodule init
    git submodule update

## building the site

### Markdown content

To make changes to the published website, edit any of the content in the Markdown files in ./copim_website/content/en. Each Markdown file contains frontmatter formatted at the top of the file as:

    ---
    title: "About us"
    ---

This is basic metadata about the page including but not limited to title, creation date, modification date, weighting. 

The main text of the page then appears below formatted as Markdown text. 

### Hugo config

The main Hugo configuration file is ./copim_website/config.toml. This contains basic configuration information for the site. 

Of particular note is the baseURL variable which is set as `http://localhost:1337` for local development and should be set to `http://copim.ac.uk` when deployed on the production server. 

### Hugo theme

The website's Hugo theme is a bespoke theme called Inate combining the themes [Introduction](https://github.com/victoriadrake/hugo-theme-introduction) designed by [Victoria Drake](https://victoria.dev) and [Slate](https://github.com/gesquive/slate) designed by [Gus Esquivel](https://github.com/gesquive).

The files for this theme are kept in ./copim_website/themes/inate which is initialised in this Git repository as a submodule from their dedicated Git repository at [https://github.com/COPIM/inate-hugo/](https://github.com/COPIM/inate-hugo/). If you can't see the theme in the themes folder, make sure you've initiated the Git submodule:

    git submodule init
    git submodule update

### running Hugo

Once changes have been made, you can run Hugo through the Docker Compose configuration provided. Make sure Docker is installed on whatever machine you're using and then simply run the following command from the repository's base directory:

    docker-compose run hugo

This will run Hugo on the ./copim_website directory and transform the ./copim_website/content Markdown files into website files which it places in ./copim_website/public. 

### deploying on the server

This website is deployed on Copim's dedicated Ubuntu server in the directory /home/ad7588/website_inate and is served from the Docker Compose configuration in /home/ac9573/docker-setup/nextcloud. 
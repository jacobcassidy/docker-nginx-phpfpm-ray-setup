# Docker NGINX, PHP-FPM & Ray Setup

This repository contains the files needed to quickly get up and running with a local PHP development Docker container. The container uses __NGINX & PHP-FPM__ for the server, __MySQL__ for the database, __local volumes__ for editing the files and database, and the composer __Global Ray__ package for connecting with the Ray desktop app for debugging.

Included below are one-time setup instructions for creating a __stand-alone NGINX Reverse Proxy Docker network__. This network container will allow you to run multiple containers simultaneously, all using unique local domain names on the standard 80 (HTTP) or 443 (HTTPS) ports.

This removes the need to manage port numbers, gives you clean domains to work from (no appended port number), and manages running your local domains on the HTTPS protocol.

## Other Docker Container Setup Repositories

Depending on what stack you're using and whether you use the [Ray app](https://myray.app/) for debugging, another container may be a better fit:

| Without the Global Ray package| With the Global Ray package |
| - | - |
| [NGINX, PHP-FPM & MySQL](https://github.com/jacobcassidy/docker-nginx-phpfpm-setup) | [NGINX, PHP-FPM, Ray, & MySQL](https://github.com/jacobcassidy/docker-nginx-phpfpm-ray-setup) |
| [WordPress & MySQL](https://github.com/jacobcassidy/docker-wordpress-setup) | [WordPress, Ray, & MySQL](https://github.com/jacobcassidy/docker-wordpress-ray-setup) |

## Instructions

### First Time Setup

For all features to work, you must do a one-time setup of the following:

1. Make sure the following command line tools are installed on your local machine:
    - [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
    - [mkcert](https://github.com/FiloSottile/mkcert)
2. Create a stand-alone reverse proxy network (to use multiple local domains on the standard 80 or 443 ports):
    - In the parent directory where you want to store your network files (such as `/Users/Username/Projects/Assets/Docker/`), run: `git clone git@github.com:jacobcassidy/docker-localhost-network.git`.
    - From the `docker-localhost-network` directory you just cloned, run: `docker compose up -d` to build and start the container.

### Continued/Additional Setup

1. Run `git clone git@github.com:jacobcassidy/docker-nginx-phpfpm-ray-setup.git` in the parent directory where you want your project directory nested.
2. Rename the cloned directory from "docker-nginx-phpfpm-ray-setup" to your project name.
3. Rename the `.env-example` file to `.env`.
4. Update the `.env` file with the values your project will use.
5. In the `/docker-localhost-network/certs` directory you created in the __First Time Setup__ instructions above, create the SSL certs needed for the HTTPS protocol using the command: `mkcert yourdomain.localhost`. Make sure you replace "yourdomain.localhost" with the local domain name you specified in your `.env` file.
6. Rename the created certs from `yourdomain.localhost-key.pem` to `yourdomain.localhost.key` and `yourdomain.localhost.pem` to `yourdomain.localhost.crt`
7. Open the [Docker Desktop](https://www.docker.com/products/docker-desktop/) app so the Docker engine is on.
8. Build the docker container with: `docker compose up -d` (run this command in the `your-project-name/docker` directory). This will create your server and add the `/storage/mysql` directory in your docker directory.
9. Replace this README content with your project's README content (you can view the original README [here](https://github.com/jacobcassidy/docker-nginx-phpfpm-ray-setup)).
10. Remove the cloned "docker-nginx-phpfpm-ray-setup" .git directory with: `rm -rf .git` (run this in your project directory).
11. Initialize a new git repository for your project with: `git init`.
12. If you will be using a GitHub remote repo, create and connect to it now.
13. Open your browser to the local domain specified in your `.env` file and check that everything is loading correctly.

## Issues?

If you come across any issues, please feel free to report them [here](https://github.com/jacobcassidy/docker-nginx-phpfpm-ray-setup/issues).
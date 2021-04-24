# Static Page Generator using Hugo for jacobmaestri.com

This repo contains the hugo files that are used for generating the website at [jacobmaestri.com](https://jacobmaestri.com).

## Project Structure

There are three parts to this codebase. First, this repo contains the hugo files and the content that is used to generate the static site.

There are two required submodules in this project:

* `/public/` is a submodule of the [Public Pages Repo](https://github.com/jfmaestr/jfmaestr.github.io/) and is the output when hugo generates the static files

* `/themes/` contains the [Book Theme](https://github.com/alex-shpak/hugo-book/) that this website utilizes.




## Cloning this project

[Hugo](https://gohugo.io/getting-started/quick-start/) must be installed on the development computer to serve the development web server, and eventually to generate the static files.

For the iniatial clone, run `git clone --recursive https://github.com/jfmaestr/portfolio` will clone this project, as well as the `public` and `book` theme submodules.

If you have already cloned and need to pull the submodule files, run `git submodule update --init`.

## Development

Run `hugo server -D` to start the local hugo server with draft pages enabled. This should be accessiable at the localhost address that the terminal displays after starting the server.

## Deploying changes to the public site

This repo contains `deploy.sh`. This script will build the static files using the correct theme, outputting the files to the public submodule, committing the changes, and then pushes the updates to GitHub.

When you have want to deploy your changes to the public site, simply run this script via `./deploy.sh` in your terminal and it should update the public submodule with the new static pages. 

```bash
#!/bin/sh

# If a command fails then the deploy stops
set -e

printf "\033[0;32mDeploying updates to GitHub...\033[0m\n"

# Build the project.
hugo -t book # if using a theme, replace with `hugo -t <YOURTHEME>`

# Go To Public folder
cd public

# Add changes to git.~
git add .

# Commit changes.
msg="rebuilding site $(date)"
if [ -n "$*" ]; then
	msg="$*"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master
```
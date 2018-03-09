---
title: "Setup s·nr"
author: [Paul Klemm, Peter Frommolt, Jan-Wilhelm Kornfeld]
date: 2018-03-08
titlepage: true
colorlinks: true
---

# Setup s·nr

**Always up-to date installation instructions are located in [https://github.com/snr-vis/setup-snr](https://github.com/snr-vis/setup-snr)**

## Requirements

* The only dependency for s·nr is docker. Please find the installation files for your system here: [https://www.docker.com/community-edition](https://www.docker.com/community-edition).
* Make sure to have at least `10-15 GB` of memory available for docker

## Download required files

![Download zip file of the project using GitHubs download function.](images/download_zip_arrow.png){#fig:download_zip}

* Go to [https://github.com/snr-vis/setup-snr](https://github.com/snr-vis/setup-snr) and _either_ clone the repository or download it as a zip (Fig. @fig:download_zip.).
* Go into the path of the downloaded repository and run the following docker call:

```bash
docker pull paulklemm/snr
docker run -t -d \
    -p 8080:8080 \
    -v sonar:/home/opencpu/sonar \
    --name opencpu_rstudio \
    paulklemm/snr
```

* Setting up the docker image can take a minute, depending on the system

## Quickstart: Example script to start

This script requires a Unix (e.g. `macOS` or `Linux`) system with a running docker instance. It will download this repository and initialize s·nr.

```bash
# Setup snr directory
mkdir ~/snr
cd ~/snr
git clone https://github.com/snr-vis/setup-snr
cd setup-snr
# Download all public files
make download-all-public-files
# Run the docker instance
docker pull paulklemm/snr
docker run -t -d \
    -p 8080:8080 \
    -v sonar:/home/opencpu/sonar \
    --name opencpu_rstudio \
    paulklemm/snr
```

## Generate User file

The server's API allows the create a user file by specifying path and password by calling: `http://<url_to_server>:<port>/api/makeuserfilejson?pw=mypassword&path=/home/opencpu/sonar/data`. You can use the response to create or edit the user files.

### Workflow for creating a new user

1.  Create a new folder for the user in the folder that is linked to the `docker` `R` back-end and add the data there
1.  Create a `dictionary.json` file in that folder (see [Structure of Data and OpenCPU Sessions](#structure-of-data-and-opencpu-sessions))
1.  Check `server_settings.json` file where the user configuration files are
1.  Go to this directory and save the output of `http://<url_to_server>:<port>/api/makeuserfilejson?pw=<user_password>&path=<path_to_data_on_r_back_end>` to `<username>.json`
1.  Log in to sonar with the new account

## Additional Information

Please refer to the readme of the `snr` repository ([https://github.com/snr-vis/snr](https://github.com/snr-vis/snr)) for more details.

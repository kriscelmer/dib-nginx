# dib-nginx
diskimage-builder scripts to create Ubuntu24.04 + NGINX custom OpenStack image

## Prepare and install DIB on Ubuntu 24.04 system

```bash
# Ubuntu/Debian prerequisites
sudo apt-get update
sudo apt-get -y install python3-venv qemu-utils debootstrap git

# Isolate DIB in a virtualenv
python3 -m venv ~/dib-venv
source ~/dib-venv/bin/activate
pip install --upgrade pip
pip install diskimage-builder        # pulls the latest release
```

## Clone this repo

```bash
git clone "https://github.com/kriscelmer/dib-nginx"
```

## Files to get copied into the image

Place all static files to get copied verbatim into the image in subfolders of `dib-nginx/nginx/static/`, like the `dib-nginx/nginx/static/var/www/html/index.html` to get copied into `/var/www/html/index.html`.

## Build the image

```bash
# Tell DIB where to find your element
export ELEMENTS_PATH=~/dib-nginx/elements
# Pick the Ubuntu release for the ubuntu/ubuntu-minimal element
export DIB_RELEASE=noble # Ubuntu 24.04 LTS

# Build; “vm” adds a bootloader, “ubuntu” pulls the cloud image, "nginx" refers to subfolder in ELEMENTS_PATH
disk-image-create ubuntu vm nginx install-static -o ubuntu-24.04-nginx
```

# URL Copy

A simple and universal command line tool for capturing screenshots and
uploading to the web.

It's built in bash and highly extensible and customisable. Allowing you to
easily add support for custom screencapture apps and services.

## Usage

UCP can be used by setting configuration inside `~/.ucp`, see below for more
information on available providers.

```bash
CAPTURE_PROVIDER=screencapture_select
CLIPBOARD_PROVDER=pbcopy
UPLOAD_PROVIDER=sftp

SFTP_HOST=fuller.li
SFTP_DIR=/srv/www/snapshots
BASEURL="https://snapshots.fuller.li/"
```

Once configured, you can run `ucp` to capture and upload files.

### Capture

Capture and upload a screenshot to your configured service.

```shell
$ ucp capture
https://screenshots.fuller.li/Rniol.png
```

### Upload

Upload a file to your configured service.

```shell
$ ucp upload test.tar.xz
https://screenshots.fuller.li/test.tar.xz
```

### Capture Provides

#### `screencapture`

Mac OS X Full Screen Capture

#### `screencapture_select`

#### `scrot`

Use scrot to take a full screen capture.

#### `scrot_select`

Use scrot to take a selective capture

### Clipboard Provider

#### `empty`

This provider disables copying the URL to the clipboard.

#### `pbcopy`

Mac OS X System Clipboard.

#### `xsel`

An X server command for managing the clipboard.

### Upload Provider

#### `sftp`

Uploads to SFTP. This provider requires additional configuration:

```bash
SFTP_USER=kyle # Defaults to current username
SFTP_HOST=fuller.li
SFTP_PORT=22 # Defaults to 22

## Base directory to upload file to, must end in / (unless empty)
SFTP_DIR=/srv/www/fuller.li/screenshots
```

#### `ftp`

Uploads to FTP. This provider requires additional configuration:

```bash
FTP_USER=kyle
FTP_PASSWORD=super-secret
FTP_HOST=fuller.li

## Base directory to upload file to, must end in / (unless empty)
FTP_DIR=/srv/www/fuller.li/screenshots
```

#### `bacon`

This service is shutdown :(.

#### Custom Upload Providers

A custom upload provider can be created using a bash function in your config
file. For example:

```bash
UPLOAD_PROVIDER=custom_provider

custom_provider() {
  local file=$1
  # Upload file...
  URL="https://foo.com/$file"
}
```

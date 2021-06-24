# Installation procedure for Sherlock Video Plugin

Start by installing the OS specific parts.

---

## on Linux servers

### `ffmpeg`  installation

Install the `ffmpeg` package.

On Debian based servers:

```bash
sudo apt install ffmpeg
```

On RedHat based servers:

```bash
sudo rpm install ffmpeg
```

### Converter script

Copy the script called `ffsherlock` to `/usr/bin/ffsherlock`

Make the script executable:
`sudo chmod a+x /usr/bin/ffsherlock`

### Edit Dominos list of Mime-types

In `/local/notesdata/httpd.cnf` add the lines mentioned under the heading "Set Dominos Mime-Types" in this document.

---

##  on Windows servers

### `ffmpeg`  installation

Download the installer from: https://ffmpeg.org/download.html

Unzip the downloaded file to `C:\Program Files\ffmpeg\`

You don't need to put it on the environment path.

### Converter batch file

Copy the batch file called `sherlock.bat` to `C:\Program Files\ffmpeg\bin\ffsherlock.bat`

### Edit Dominos list of Mime-types

In `C:\Program Files\IBM\Domino\Data\httpd.cnf` add the lines mentioned under the heading "Set Dominos Mime-Types" in this document.

---

## Set Dominos Mime-Types

```txt
AddType  .m4v      video/mp4
AddType  .mp4      video/mp4
AddType  .webm     video/webm
```

The path to `httpd.cnf` may be different on your installation.

Restart Dominos HTTP task, to read the `httpd.cnf` changes.

## Edit the configuration in the Video module

See: Sherlock Video Plugin.pdf

The video encoding speed can be increased by changing the number of threads the video encoder can use. Change the threads parameter in the converter parameters:

```txt
-threads 4
```

Do not use all CPU cores for the video encoder, or Domino will suffer.

## Optional: Reverse Proxy Server

If Domino is placed behind a nginx, acting as a reverse proxy server, the vhost file must have a sufficient maximum request body size.

Inside the `server {` add:

```txt
client_max_body_size 2048M;
```

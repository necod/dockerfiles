Docker Sabnzbd
==============

This is a Dockerfile to set up Sabnzbd from the jcfp PPA. Change port if
necessary to accommodate SSL. You can use this with Docker data volumes if you
desire for storing configuration and downloads.

Build
-----

::

    # docker build -t sabnzbd .

If using data-only volumes::

    # docker run -v /config --name sabnzbd_config ubuntu chown -R 22000 /config
    # docker run -v /data --name media_data ubuntu chown -R 22000 /data

Run
---

For regular filesystem storage::

    # docker run -d -v <path/to/config-file>:/config -v <path/to/downloads>:/data -p 8080:8080 sabnzbd

For data-only volume storage::

    # docker run -d --volumes-from sabnzbd_config --volumes-from media_data -p 8080:8080 --name sabnzbd_run sabnzbd

If you enable SSL, make sure to change your port numbers when running the container (9090 typically). Systemd service file is available.

Manage
------

To manage downloaded media (access the media_data volume)::

    # docker run -it --rm --volumes-from media_data ubuntu /bin/bash

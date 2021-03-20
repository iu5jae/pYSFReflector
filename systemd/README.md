# Running the pYSFReflector as a Service

Most of us will run the pYSFReflector as a service to be started automatically at system startup.
A common way to realize this is using startup-scripts. Almost all modern Linux-systems support
systemd-startup-system.

The script you find here in this directory is such a systemd-startup-script.
Simply copy it (as root) into /etc/systemd/system and use the following commands to make it running:

`sudo systemctl enable YSFReflector.service`

and for starting it initially:

`sudo systemctl start YSFReflector.service`

But before you start the reflector with this command keep sure to have following steps done:

a) Add a group named mmdvm to your system-groups with: `sudo groupadd mmdvm`

b) After this add the system-user mmdvm to your users with: `sudo useradd mmdvm -g mmdvm -s /sbin/nologin`

c) make the logdir configured in your YSFReflector.ini owned by mmdvm for example like this:
`sudo chown -R mmdvm:mmdvm /var/log/YSFReflector`

Now all is prepared for starting the reflector automatically.

To control the reflector's functions you could use following commands:

`sudo systemctl start YSFReflector.service` starts the reflector if not running

`sudo systemctl stop YSFReflector.service` stops the reflector

`sudo systemctl restart YSFReflector.service` restarts a running reflector (for example after changeing YSFReflector.ini)

`sudo systemctl status YSFReflector.service` shows actual running state of reflector


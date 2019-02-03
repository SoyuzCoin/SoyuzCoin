Sample init scripts and service configuration for soyuz3d
==========================================================

Sample scripts and configuration files for systemd, Upstart and OpenRC
can be found in the contrib/init folder.

    contrib/init/soyuz3d.service:    systemd service unit configuration
    contrib/init/soyuz3d.openrc:     OpenRC compatible SysV style init script
    contrib/init/soyuz3d.openrcconf: OpenRC conf.d file
    contrib/init/soyuz3d.conf:       Upstart service configuration file
    contrib/init/soyuz3d.init:       CentOS compatible SysV style init script

1. Service User
---------------------------------

All three startup configurations assume the existence of a "soyuz3" user
and group.  They must be created before attempting to use these scripts.

2. Configuration
---------------------------------

At a bare minimum, soyuz3d requires that the rpcpassword setting be set
when running as a daemon.  If the configuration file does not exist or this
setting is not set, soyuz3d will shutdown promptly after startup.

This password does not have to be remembered or typed as it is mostly used
as a fixed token that soyuz3d and client programs read from the configuration
file, however it is recommended that a strong and secure password be used
as this password is security critical to securing the wallet should the
wallet be enabled.

If soyuz3d is run with "-daemon" flag, and no rpcpassword is set, it will
print a randomly generated suitable password to stderr.  You can also
generate one from the shell yourself like this:

bash -c 'tr -dc a-zA-Z0-9 < /dev/urandom | head -c32 && echo'

Once you have a password in hand, set rpcpassword= in /etc/soyuz3/soyuz3.conf

For an example configuration file that describes the configuration settings,
see contrib/debian/examples/soyuz3.conf.

3. Paths
---------------------------------

All three configurations assume several paths that might need to be adjusted.

Binary:              /usr/bin/soyuz3d
Configuration file:  /etc/soyuz3/soyuz3.conf
Data directory:      /var/lib/soyuz3d
PID file:            /var/run/soyuz3d/soyuz3d.pid (OpenRC and Upstart)
                     /var/lib/soyuz3d/soyuz3d.pid (systemd)

The configuration file, PID directory (if applicable) and data directory
should all be owned by the soyuz3 user and group.  It is advised for security
reasons to make the configuration file and data directory only readable by the
soyuz3 user and group.  Access to soyuz3-cli and other soyuz3d rpc clients
can then be controlled by group membership.

4. Installing Service Configuration
-----------------------------------

4a) systemd

Installing this .service file consists on just copying it to
/usr/lib/systemd/system directory, followed by the command
"systemctl daemon-reload" in order to update running systemd configuration.

To test, run "systemctl start soyuz3d" and to enable for system startup run
"systemctl enable soyuz3d"

4b) OpenRC

Rename soyuz3d.openrc to soyuz3d and drop it in /etc/init.d.  Double
check ownership and permissions and make it executable.  Test it with
"/etc/init.d/soyuz3d start" and configure it to run on startup with
"rc-update add soyuz3d"

4c) Upstart (for Debian/Ubuntu based distributions)

Drop soyuz3d.conf in /etc/init.  Test by running "service soyuz3d start"
it will automatically start on reboot.

NOTE: This script is incompatible with CentOS 5 and Amazon Linux 2014 as they
use old versions of Upstart and do not supply the start-stop-daemon uitility.

4d) CentOS

Copy soyuz3d.init to /etc/init.d/soyuz3d. Test by running "service soyuz3d start".

Using this script, you can adjust the path and flags to the soyuz3d program by
setting the Soyuz3D and FLAGS environment variables in the file
/etc/sysconfig/soyuz3d. You can also use the DAEMONOPTS environment variable here.

5. Auto-respawn
-----------------------------------

Auto respawning is currently only configured for Upstart and systemd.
Reasonable defaults have been chosen but YMMV.

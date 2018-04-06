 - --env: set environment variables in docker command, too. Makes them available with 'docker exec', too.

## Version: 3.9.8.5  
### Date: 2018-04-05
 - finish() 'docker stop' before creating 'timetosaygoodbye' for more graceful shutdown [#37](https://github.com/mviereck/x11docker/issues/37)
 - minor *bugfix*es (XAUTHORITY in setup script, User in systemd journal service)

## Version: 3.9.8.4  
### Date: 2018-04-04
 - --workdir: *new option*
 - --systemd/--dbus-system: changed su command to remove sh from pstree
 - *bugfix* user entry in /etc/group

## Version: 3.9.8.3  
### Date: 2018-04-04
 - *bugfix* --dbus-system: regression: must not set no-new-privileges

## Version: 3.9.8.2  
### Date: 2018-04-03
 - disable entrypoint 'tini' if x11docker already runs an init system (default: tini from docker).

## Version: 3.9.8.1  
### Date: 2018-04-03
 - show container ID on stdout ([#36](https://github.com/mviereck/x11docker/issues/36))
 - --security-opt=no-new-privileges now always set except for --sudouser. It does not harm switching from root to less privileged users.
 - setup script with user switching: "exec su" instead of "su" to avoid root shell in parent tree. su is now child of init.

## Version: 3.9.8.0  
### Date: 2018-04-02
 - Removed Xtermlogfile,  using Dockerlogfile instead. Strange: solved missing output with --pw su/sudo, too.
 - Escape special characters in --env, ENV and image command. (adresses [#34](https://github.com/mviereck/x11docker/issues/34), too, now solved better)

## Version: 3.9.7.9  
### Date: 2018-03-31
 - Store parsed parts of $Imagecommand in '' to allow constructs like:  sh -c "cd /etc ; xterm"
 - *bugfix*: add --rm to docker run for environment check

## Version: 3.9.7.8  
### Date: 2018-03-31
 - Handle equal signs in container environment defined with ENV ([#34](https://github.com/mviereck/x11docker/issues/34))

## Version: 3.9.7.7  
### Date: 2018-03-31
 - Handle whitespaces in container environment defined with ENV ([#34](https://github.com/mviereck/x11docker/issues/34))

## Version: 3.9.7.6  
### Date: 2018-03-30
 - mount X socket and lockfile read-only to protect from /tmp cleanup of init systems
 - minor improvements of init system initialization
 - remove checks for --userns-remap and --selinux-enabled. [#33](https://github.com/mviereck/x11docker/issues/33)

## Version: 3.9.7.5  
### Date: 2018-03-30
 - --dbus-system: drop consolekit
 - --sysvinit,--openrc: disable getty in inittab instead of overwriting inittab with shared volume
 - --sysvinit: change rc.local in setupscript instead of overwriting it with shared volume
 - --openrc, --runit: create service in setupscript, drop some more capabilities

## Version: 3.9.7.4  
### Date: 2018-03-26
 - --sysvinit: *new option* for init system SysVinit in container. Tested with devuan.
 - --pulseaudio: *bugfix*: need to set env PULSE_SERVER
 - --runit: add softlink for X socket in x11docker.CMD.sh for compatibility with runit on debian

## Version: 3.9.7.3  
### Date: 2018-03-21
 - --pulseaudio: share XDG_RUNTIME_DIR/pulse instead of connection over tcp

## Version: 3.9.7.2  
### Date: 2018-03-20
 - [#30](https://github.com/mviereck/x11docker/issues/30) Fix writeaccess() for user/group names with spaces in it
 - --wm: fall back to autodetection if specified window manager not found
 - *bugfix* --env: regard whitespace. Still need to handle special chars like"\'$.
 - --add: *new option* to add a host command in xinitrc
 - consolekit: enable and use automatically for --dbus-system, --openrc, --runit
 - --dbus: enable automatically for --runit, --openrc
 - mywatch(): watch again, now without sh -c
 - --debug: *new option* to set -x in all scripts showing code lines while executed.
 - --sharewayland, --waylandenv: deprecated, not needed for anything anymore. --wayland does the job.
 - --help: usage() cleanup

## Version: 3.9.7.1  
### Date: 2018-03-16
 - *bugfix* alpine images: /etc/shadow entry must be /bin/sh, --dbus-system -with su fails with /bin/bash
 - *bugfix* openSUSE: finish(): replace bc with bash-only calculation, bc misses on openSUSE

## Version: 3.9.7    
### Date: 2018-03-15
 - *bugfix* openSUSE/fedora: ps check for container pid; fixed desktop logout issue, too.
 - structure change: don't sleep 1 for setup; instead wait for it in CMD.sh resp. run su or init in setup
 - SSH with --hostdisplay: set --hostipc, --hostnet and --trusted. Do not X-generate cookie, bake self.
 - *bugfix* ---weston/-weston-xwayland: do not start drm backend if started within X without DISPLAY -> crashed host X
 - *bugfix*: regard ssh session, assume tty if DISPLAY is empty
 - *bugfix*: --hostdisplay: don't set keymap
 - xinitrc: some cleanup
 - --verbose: power of moo

## Version: 3.9.6.1  
### Date: 2018-03-10
 - --lang: replace locale-gen with more general available localedef
 - --tini: check for docker-init in PATH, disable if missing ([#23](https://github.com/mviereck/x11docker/issues/23))

## Version: 3.9.6    
### Date: 2018-03-09
 - --lang: *new option* to set language locale in utf8, create it if missing.

## Version: 3.9.5    
### Date: 2018-03-06
 - --keymap: *new option* to set keyboard layout

## Version: 3.9.4.2  
### Date: 2018-03-06
 - store keyboard layout (xkb_keymap) in separate file, not in xinitrc. Set on all X servers. [#25](https://github.com/mviereck/x11docker/issues/25)

## Version: 3.9.4.1  
### Date: 2018-03-06
 - --pulseaudio: *bugfix*/typo
 - share /etc/localtime with container to have the same time

## Version: 3.9.4.0  
### Date: 2018-03-05
 - --pulseaudio --hostnet: no fallback to alsa, use localhost IP instead
 - --pulseaudio --no-internet: fallback to --alsa
 - clean up error message on docker startup failure, remove multiple error lines
 - --systemd: *bugfix*: terminate x11docker if systemd startup fails
 - stdout and stderr of image command outsourced of docker.log
 - docker log -f > docker.log to get output in detached mode
 - --sys-admin: no longer deprecated, needed for debian 9 images (but not debian 10).
 - --net and --ipc changed to --hostnet and --hostipc
 - --dbus-daemon changed to --dbus-system
 - --auto --gpu: fallback to --hostdisplay for seamless mode if xpra and weston not found ([#23](https://github.com/mviereck/x11docker/issues/23))
 - [#24](https://github.com/mviereck/x11docker/issues/24) mount /dev/dri and /dev/snd not only with --device, but also --volume to keep ownership+group
 - --hostdisplay: minor *bugfix*: Use correct display number to share /tmp/.X0-lock, only share if it exists
 - more verbose messages in waiting routines

## Version: 3.9.3.2  
### Date: 2018-03-01
 - --no-xtest: disable extension XTEST. Default for most options.
 - openSUSE docker package misses init binary, show warnings for --tini, issue [#23](https://github.com/mviereck/x11docker/issues/23)

## Version: 3.9.3.1  
### Date: 2018-03-01
 - fix XTEST warning messages

## Version: 3.9.3    
### Date: 2018-03-01
 - --tini: show warning for outdated docker versions without option --init and fall back to --no-init, issue [#23](https://github.com/mviereck/x11docker/issues/23)
 - --xtest: *new option* to enable X extension XTEST. Default for --xdummy, --xvfb, --xpra
 - --pulseaudio with --net: fallback to --alsa, disabling --pulseaudio

## Version: 3.9.2.3  
### Date: 2018-02-25
 - set container GID of video and audio to same as on host
 - cat docker daemon messages for startup error message
 - *bugfix* --kwin: kwin_wayland seems to need dbus-launch now
 - mywatch(): replaced watch with custom sleep loop, watch failed in --hostdisplay (xinitrc) setups
 - --exe: only forward stdin if not empty
 - finish(): use pkill in most cases instead of kill to avoid kill success messages
 - *bugfix* --weston/--kwin: wait for file creation of wayland socket, checking logfile is not enough
 - mywatch(): verbose output

## Version: 3.9.2.2  
### Date: 2018-02-09
 - minor *bugfix* --exe: avoid possible hostexe options with basename for $Hostexebasename
 - minor *bugfix*: typo checking /tmp/.Xn-lock
 - check free display and cache folder with find only
 - *bugfix* checking free display number: race condition if starting two x11docker instances at same time, second one failed because display number already in use
 - plasmashell added to possible window managers

## Version: 3.9.2.1  
### Date: 2018-01-29
 - correct date/year in changelog (issue [#21](https://github.com/mviereck/x11docker/issues/21))
 - finish(): minor *bugfix*: wrong warning although terminating bgpid was successfull
 - create /x11docker/environment to store and provide container environment variables

## Version: 3.9.2    
### Date: 2018-01-21
 - *bugfix*: add groups video and audio if su is not used in container. /etc/group changes by dockerrc seem to be not regarded in that case.
 - finish(): more precise check with pid and name before killing background pids

## Version: 3.9.1.9  
### Date: 2018-01-17
 - --xpra: if server crashes, use xpra option --mmap=no on restart

## Version: 3.9.1.8  
### Date: 2018-01-16
 - --xpra: stop x11docker if xpra server crashes multiple times

## Version: 3.9.1.7  
### Date: 2018-01-15
 - --gpu: share /dev/vga_arbiter and /dev/nvidia*

## Version: 3.9.1.6  
### Date: 2018-01-15
 - restart xpra server if it crashes (can happen with xpra 2.2, reason unknown)

## Version: 3.9.1.5  
### Date: 2018-01-13
 - *bugfix* xpra: reconnect to server after timeout (60s) if switching to console

## Version: 3.9.1.4  
### Date: 2018-01-12
 - --help: some usage updates
 - --xorg: create virtual framebuffer if no monitor is connected (headless server setup)
 - --xpra: note that 2.1.x series is more stable than 2.2.x series
 - create $Cacherootfolder/Xenv.latest with latest X environment variables for easier custom access
 - --verbose --systemd: hide error messages: Failed to add fd to store | Failed to set invocation ID | Failed to reset devices.list
 - --systemd: set global environment XAUTHORITY

## Version: 3.9.1.3  
### Date: 2018-01-04
 - --dbus-daemon: set xhost +SI:localuser:$USER, needed for deepin
 - *bugfix* --systemd: global XAUTHORITY setting was wrong, removed at all
 - faster startup of pulseaudio, no sleep 1
 - *bugfix*: pull terminal did not appear if running from terminal
 - create fake homedir and softlinks to sharedirs in CMD.sh, base is /fakehome now
 - extension XTEST: more restrictive defaults

## Version: 3.9.1.2  
### Date: 2017-12-28
 - --sudouser: root gets password 'x11docker', too
 - check environment variables in image and set them in x11docker.CMD.sh. Allows PATH of x11docker/trinity again.
 - *bugfix* parsing host XAUTHORITY if running from gksu
 - cut image command at '#'

## Version: 3.9.1.1  
### Date: 2017-12-28
 - *bugfix* --systemd: directly share X socket as systemd can have issues with soft links

## Version: 3.9.1    
### Date: 2017-12-25
 - run in detached mode, drop mess of nohup/setsid/script
 - --dbusdaemon: dropped consolekit, not really useful
 - --dbusdaemon: switch only for  --tini/--none. Always run daemon for --systemd --openrc --runit
 - --systemd: create /sys/fs/cgroup/systemd if missing on host
 - --sys-admin: deprecated thanks to --tmpfs=/run/lock
 - containersetup.sh collects most former 'docker exec' commands from dockerrc

## Version: 3.9.0.5  
### Date: 2017-12-21
 - add capability DAC_OVERRIDE if user switching is allowed -> needed to change /etc/sudoers if ro
 - *bugfix*: only create XDG_RUNTIME_DIR if not already existing
 - --systemd: adding --tmpfs=/run/lock allows to drop --sys-admin !

## Version: 3.9.0.4  
### Date: 2017-12-20
 - docker run --workdir=/tmp, avoids issues with WORKDIR in image (seen with lirios/unstable)
 - *bugfix* --dbus: check for dbus-launch in x11docker.CMD.sh, not in dockerrc on host
 - changes to satisfy lirios:
 - add docker run -ti
 - run docker command with script -c to provide fake tty
 - change /tmp/fakehome to /home/fakehome

## Version: 3.9.0.3  
### Date: 2017-12-17
 - switched back to /tmp/fakehome to avoid CHOWN and issues with --sharedir
 - drop --cap-add CHOWN
 - *bugfix* --sudouser, failed to start
 - --sharedir: without --home[dir], create softlinks to /tmp/fakehome
 - --home: avoid conflict with --sharedir=$HOME, mount as $HOME/$(basename $HOME)
 - only chown $Benutzerhome if --home[dir] is not used. Change non-writeable error in warning only
 - --hostdisplay: warning if host has no own cookie
 - avoid grey edge with Xwayland, Xaxis must be dividable by 8

## Version: 3.9.0.2  
### Date: 2017-12-16
 - /etc/sudoers[.d/]: replace completly to avoid possible evil image setups
 - --cap-add CHOWN as default to allow /home/$Benutzer with --sharedir

## Version: 3.9.0.1  
### Date: 2017-12-16
 - *bugfix*: --systemd: do not set $HOME globally, root may write into it
 - use /home/$Benutzer instead of /tmp/fakehome

## Version: 3.9.0    
### Date: 2017-12-15
 - /etc/shadow: disable possible root password
 - --dbusdaemon: *new option* to run dbus system daemon and consolekit in container
 - re-checked capabilities for init systems
 - --systemd: set environment globally, especially DISPLAY for deepin is needed
 - --systemd: set xhost+SI:localuser:$Benutzer as XAUTHORITY seems to be ignored
 - /tmp/.ICE-unix created in dockerrc, root owned with 1777, needed for SESSION_MANAGER
 - --rw: deprecated, root file system is always r/w now due to 'docker exec' in dockerrc

## Version: V3.8.1)  
### Date: 2017-12-10
 - *bugfix* Ubuntu: avoid Wayland backend for Weston due to MIR issue [#19](https://github.com/mviereck/x11docker/issues/19)

## Version: V3.8.1)  
### Date: 2017-12-10
 - --xorg: change Xorg to X. X is setuid wrapper for Xorg on Ubuntu 14.04

## Version: V3.8.1)  
### Date: 2017-12-10
 - +iglx removed from X options, not present in older versions of X, and maybe security issue.
 - create user in dockerrc with 'docker exec' instead of using createuser.sh
 - --xorg: removed +iglx from options, not supported on older X versions
 - --openrc: *new option* for init system OpenRC in container
 - --sharecgroup: *new option* to share /sys/fs/cgroup. default for --systemd.
 - create /var/lib/dbus in dockerrc to avoid dbus errors with init systems
 - show image name and display in weston windows
 - *bugfix* --runit: add SYS_BOOT even with --cap-default

## Version: 3.8.0    
### Date: 2017-12-04
 - --sudouser: create user with docker run options instead of createuser script
 - --sudouser: create /etc/sudoers.d/$Benutzer with docker exec in dockerrc
 - --sudouser: create /etc/sudoers.d/$Benutzer instead of adding groups wheel and sudo
 - createuser.sh: check for useradd, if missing use adduser (fits fedora and alpine/busybox as well)
 - --runit: *new option* for init system runit
 - --init: *new option* for init system tini (default now, docker run option --init)
 - --no-init: *new option* to run image command as PID 1 (has been default before x11docker 3.8)
 - --sys-admin: *new option* for --cap-add=SYS_ADMIN. Needed for systemd in debian based images.
 - --sudouser, --systemd: set needed capabilities only instead of --cap-default
 - --xpra --hostuser: create /run/user/$Hostuseruid if missing
 - $Sharefolder/stdout+sterr: chmod 666 to allow access with --user
 - container user password: x11docker (creating volume /etc/shadow)
 - init system tini as default with 'docker run --init'
 - --systemd: unprivileged systemd in container
 - --exe and --xonly: regard --home and --homedir, --user and --hostuser
 - --wayland: *new option* to auto-setup Wayland environment
 - -W is now --wayland instead of --weston, -T for --weston now
 - check pids before calling mywatch()
 - *bugfix*: --hostdisplay --gpu needs trusted cookies
 - colored logfile output
 - *bugfix* in createuser.sh: adduser failed with fedora based images, use useradd and usermod instead
 - *bugfix*: --pw=gksu: avoid wrong docker startup error message, use nohup in dockerrc
 - --verbose: green colored output for logfile titles and verbose() lines
 - set env DISPLAY XAUTHORITY and WAYLAND_DISPLAY in x1docker.CMD.sh as systemd eats them otherwise
 - --systemd: *new option* to run systemd as PID1 in container and image command as a service
 - use docker run option --tmpfs for /tmp, /var/tmp and /run instead of --volume=/tmp
 - --sudouser: instead of empty password, user name is password now
 - changed container share folder /tmp/x11docker to /x11docker to avoid issues with --tmpfs /tmp

## Version: 3.7.2    
### Date: 2017-11-11
 - allow rw with --volume=/var/tmp, needed for trinity
 - *bugfix* for su on console: exec </dev/tty
 - --nxagent: removed xhost startup workaround
 - $Hostxenv: removed custom environment
 - --nxagent: shift+F11 toggles fullscreen
 - --nxagent on Mageia: only show warning about seamless mode instead of disabling it

## Version: 3.7.1    
### Date: 2017-11-03
 - *bugfix* for gksudo and lxsudo
 - read host cookie with xauth if XAUTHORITY is empty, can happen with xdm
 - --nxagent on Mageia: no seamless mode
 - Ubuntu 16.04: *bugfix* for --xpra (must not set --webcam=no)
 - replaced while/sleep loops with watch
 - *bugfix* for weston and kwin on konsole, terminal for password prompt failed
 - alertbox(): regard $DISPLAY, use $Anyterminal otherwise to support Wayland
 - weston.ini: keyboard config setting on console
 - fedora: show alert for --ipc/--trusted due to missing extension security

## Version: 3.7.0    
### Date: 2017-10-30
 - *new option* --alsa; use -wm for --xephyr and the likes; support more terminals and message dialogs

## Version: 3.7.0    
### Date: 2017-10-30
 - auto-choose window manager in --xephyr/--xorg/--weston-xwayland/--kwin-xwayland/--xwayland except --desktop is set
 - --alsa: *new option* for ALSA sound
 - changed content of variable $Xserver to X server option names itself
 - --kwin-xwayland: set keyboard layout
 - --kwin-native: deprecated, too much trouble, but less use
 - extended terminal list for password prompt/docker pull
 - --xhost: always disabling with no_xhost(), afterwards setting --xhost
 - *bugfix* --weston/--weston-xwayland: set backend in compositor command, weston's autodetection can fail
 - *bugfix* --kwin/--kwin-xwayland: set backend in compositor command, weston's autodetection can fail
 - new function alertbox, outsourced from error(). yad, kaptain, kdialog, gxmessage, xterm: additional messagebox tools

## Version: 3.6.3.9  
### Date: 2017-10-25
 - show error messages regardless of --silent
 - change "sudo" to "sudo -E", needed for OpenSUSE
 - code cleanup, some improved messages

## Version: 3.6.3.8  
### Date: 2017-10-25
 - fedora: set --ipc and --trusted for --hostdisplay only

## Version: 3.6.3.7  
### Date: 2017-10-25
 - *bugfix* --hostdisplay on fedora: use host cookie, custom cookie is rejected

## Version: 3.6.3.6  
### Date: 2017-10-24
 - --wmlist: *new option* to retrieve list of window managers, used by x11docker-gui
 - --gpu: improved support in autochoosing mode
 - disabled note of xpra keyboard shortcuts, takes too long
 - hardcoded xpra environment variables, parsing 'xpra showconfig' takes too long
 - *bugfix* for --pw=sudo, issue with setsid

## Version: 3.6.3.5  
### Date: 2017-10-24
 - *bugfix* xpra with host user root: set environment variables
 - dbus-launch for konsole and terminator, needed in dockerrc

## Version: 3.6.3.4  
### Date: 2017-10-23
 - add /usr/sbin to PATH, needed on mageia for ip
 - *bugfix* --pw=sudo: 'setsid sudo' fails, must use 'sudo setsid'

## Version: 3.6.3.3  
### Date: 2017-10-23
 - removed experimental Code
 - *bugfix* for --wm as root in xinitrc

## Version: 3.6.3.2  
### Date: 2017-10-23
 - remove debugging 'set -x' in xinitrc

## Version: 3.6.3.1  
### Date: 2017-10-23
 - *bugfix*: don't use su $USER in xinitrc
 - split X server command with \backslash in multiple lines

## Version: 3.6.3    
### Date: 2017-10-20
 - *new option* --no-internet; adjustments for CentOS/RHEL, Arch and Manjaro

## Version: 3.6.2    
### Date: 2017-10-10
 - *new option* --xfishtank; better SELinux support; --scale and --size for --xorg

## Version: 3.6.1    
### Date: 2017-08-15
 - *new option*s --stdout and --stderr; support stdin

## Version: 3.6.0    
### Date: 2017-08-12
 - workaround: disabling SELinux for container until solution for sharing unix socket is found.
 - compare: http://www.projectatomic.io/blog/2015/06/using-volumes-with-docker-can-cause-problems-with-selinux/
 - install to /usr/bin instead of /usr/local/bin to support root
 - chmod 755 instead of +x in installation
 - check if docker is installed
 - check if docker daemon is running (with ifconfig)
 - use zenity or notify-send if xmessage is not available in error()
 - *bugfix*: cookie creation failed on X without extension security. (fedora)
 - replaced sed in xauth cookie creation, sed fails in openSUSE (!?)
 - --rw: *new option* to allow read/write access to container root file system
 - check for xpra --dpi bug in 2.1 series
 - xpra --start-via-proxy=no for xpra >= 2.1
 - --nxagent: temporary xhost +SI:localuser:$Hostuser workaround as it fails again to authenticate, not dividing between XAUTHORITY and --auth
 - --pw: *new option* to choose password prompt frontend. default: pkexec
 - reduce dependency warnings for --auto
 - *bugfix*: repeating error message if waitforlogentry() failes
 - prefer $Hostenv instead of $Newxenv for password prompt -> better support for gksu
 - show docker pull in a terminal window
 - allow --hostdisplay with --xonly. May at least be usefull to create an untrusted cookie.
 - *bugfix*es in "check window manager"
 - slit docker startup from xinitrc
 - copy host cookie into $Cachefolder for compatibility with gksu
 - use gksu/gksudo if available
 - --showenv for --xonly
 - finish(): docker stop $Containername
 - dockerrc: no ps/sleep loop if running as root
 - --no-entrypoint: *New option* to disable ENTRYPOINT in image
 - --root: deprecated. Can be achieved with --hostuser=root
 - --hostuser: *New option* to set host user different from  $(logname)
 - check if docker can run without password to make --no-password needless
 - don't start docker in xinitrc as xinit runs unprivileged
 - --ps keeps cache files, too (formerly container only)
 - --desktop: no longer deprecated, easier to understand and remember than --wm=none
 - -d: used for --desktop again, no longer for --dbus. --dbus now has short opt -b
 - improved X server check due to new variable $Desktopmode
 - minor *bugfix*: &, &&, ;, <, >, | and the like possible in image command again
 - --fullscreen. Set fullscreen screen size for windowed options (xpra),too
 - allow root to start x11docker, use $(logname) for X server and as container user

## Version: 3.5.11   
### Date: 2017-07-12
 - pull image if not available before calling 'docker run'

## Version: 3.5.10   
### Date: 2017-07-12
 - regard ENTRYPOINT in dockerrc
 - regard entrypoint of image in dockerrc

## Version: 3.5.9    
### Date: 2017-07-09
 - --user: *bugfix* parsing custom gid, gid was set to username
 - --home with --user=(unknown): only show warning (instead of error) not creating persistent home
 - do not set write permissions on --home or --homedir folder for different users than $USER or --user. (Not x11docker's job)
 - do not set --read-only if --user=0
 - minor *bugfix*: chown x11docker_CMD to host user to avoid permission issues in $Sharefolder

## Version: 3.5.8    
### Date: 2017-06-07
 - --nxagent: *bugfix* due to update? must set nxagent -ac (=xhost +) temporary to allow xinit
 - --kwin-native: always share Wayland (--sharewayland --waylandenv --dbus)
 - minor *bugfix*: allow --wm for --kwin-xwayland
 - docker run "--read-only --volume=/tmp" to restrict container filesystem as read-only (except for --sudouser)
 - --xorg supports --rotate. (Xephyr could, but crashes -> Xephyr bug. Nxagent, Xdummy, Xvfb and Xwayland refuse this.)
 - --xhost STR: *new option* to specify "xhost STR". Deprecated: --xhost+
 - --xvfb: *new option* to explicitly use Xvfb and to clearly use Xdummy on --xdummy
 - Xdummy script in $Cachefolder forked from https://xpra.org/trac/browser/xpra/trunk/src/scripts/xpra_Xdummy
 - calculate VideoRam in xorg.xdummy.conf (instead of fat hardcoded 256000 kb)

## Version: 3.5.7    
### Date: 2017-06-28
 - usage info for HTML5 web application setup
 - redirect verbose output to &3 to show it in subshells, too, and to avoid possible collision with read < <()
 - --env: set custom environment variables in dockerrc instead of in docker run
 - removed unix in $Newxenv for DISPLAY to make xpra ssh setup easier
 - Xdummy-Xwayland: new X server to provide --gpu for --xdummy based on weston, xwayland and xdotool
 - always enable extension Xtest on --xdummy to allow xpra access
 - share X socket to /tmp, create .X11-unix in dockerrc and softlink socket. This avoids writeable X11-unix in $Cachedir.
 - --setwaylandenv: env now set in dockerrc instead of docker command

## Version: 3.5.6    
### Date: 2017-06-21
 - --sudouser: reincarnated option to give sudo without password to container user.
 - docker command one-liner extended to dockerrc. dockerrc creates x11docker_CMD. Can always extract image command without additional password prompt and create some environment.
 - *bugfix* parsing option --wm
 - minor *bugfix*: export $Hostxenv in error() was empty if called in xtermrc
 - create /tmp/XDG_RUNTIME_DIR and softlink to wayland socket in container due to some KDE issues (XDG_RUNTIME_DIR must be owned by user). Fails with different --user
 - create /tmp/.X11-unix with 1777 in container to allow new X sockets (especially for startplasmacompositor). Drawback: container writeable folder in cache
 - minor *bugfix*: avoid pointless warning about XTEST if not using xpra
 - shorter sleep in finish()
 - don't search for deprecated /tmp/x11docker in checkorphaned()
 - *bugfix* typo preventing start of --kwin and --kwin-native (-width instead of --width)
 - warning with hint to use --xpra-xwayland if --scale is used with --weston-xwayland.

## Version: 3.5.5.2  
### Date: 2017-06-10
 - update usage info for --xpra and --xpra-xwayland

## Version: 3.5.5.1  
### Date: 2017-06-10
 - minor *bugfix* in --auto always choosing --xorg

## Version: 3.5.5    
### Date: 2017-06-09
 - autochoose xpra-desktop if xephyr is missing
 - improved part: check virtual screen size
 - changed dpi calculation depending on xpra mode
 - desktop mode for xpra if --wm is given
 - always set XDG_RUNTIME_DIR=/tmp as some apps may expect it

## Version: 3.5.4    
### Date: 2017-06-02
 - set rw access for /dev/dri ([#12](https://github.com/mviereck/x11docker/issues/12))
 - disable extension XTEST if using wm from host (to avoid abuse of context menu of openbox and the like)

## Version: 3.5.3    
### Date: 2017-05-29
 - --pulseaudio: get and use IP of container instead of docker0 IP range ([#11](https://github.com/mviereck/x11docker/issues/11)), disabling TCP module on exit
 - changed --volume to --sharedir to avoid confusion
 - update usage()
 - mount $Sharefolder and its content read-only
 - remove X11-unix from $Sharefolder
 - set read-only for /dev/dri on --gpu
 - --security-opt=no-new-privileges added to docker run

## Version: 3.5.2    
### Date: 2017-05-22
 - --volume: *new option* to share host folders

## Version: 3.5.1    
### Date: 2017-05-19
 - user creation with '--addgroup video' to support pre-systemd and kdeneon gpu support
 - create /tmp/.X11-unix with 1777

## Version: 3.5.0    
### Date: 2017-05-17
 - avoid Terminal window with --no-password
 - --env: regard whitespaces, use \n to divide entrys
 - set mode=preferred for Weston on tty, ignore $Screensize
 - extension XINERAMA disabled as multiple Xephyr outputs cannot handle it well
 - create container home folder /tmp/fakehome in x11docker_CMD (avoids ownership problems with wine, and is less messy in /tmp)
 - more failure checks in installer()
 - check for --userns-remap, disabling it with --userns=host if --home or --homedir are set
 - minor exploit check for DISPLAY XAUTHORITY XDG_RUNTIME_DIR WAYLAND_DISPLAY HOME
 - --output-count: *new option* to set amount if virtual screens/desktop windows for Weston, Kwin, Xephyr
 - --westonini: *new option* to specify a custom weston.ini for --weston and --weston-xwayland
 - *bugfix*: -s KILL for weston on finish avoids zombies
 - --cachedir: *new option*: specify custom cache folder
 - --homedir: *new option*: specify host folder to share as home
 - automatically choose trusted or untrusted cookies
 - --trusted: *new option*: enforce trusted cookies for --hostdisplay and --kwin-native
 - --cache deprecated
 - --cap-default: Allow docker default capabilities
 - --orphaned cleans /tmp/x11docker
 - show docker log in xtermrc if pulling image
 - 'docker run --cap-drop=ALL' as default
 - --user: *new option* to set user to use (name or uid, non-existing uids possible. default: host user)
 - reduce /etc/passwd and /etc/group to container user and groups user and videp only (except root, keeps whole files).
 - creating container user similar to host user with docker run option --user and custom /etc/passwd instead of script createuser.
 - dismissed --hostuser --sudouser, effect of --hostuser is default now, --sudouser not possible due to --cap-drop=ALL
 - --gpu: only share --device=/dev/dri instead of listing all files in it

## Version: 3.2.1    
### Date: 2017-05-05
 - minor *bugfix*: --scale with --xpra-xwayland under X without Wayland failed

## Version: 3.2.0    
### Date: 2017-05-04
 - --scale: *new option* for xpra and weston
 - --rotate: *new option* for weston
 - --dpi: *new option* for screen density
 - minor *bugfix*: checking screensize in Gnome-Wayland failed looking for primary display, window was not roughly maximized
 - *bugfix*: missing error() in xinitrc
 - allow MIT-SHM for --exe

## Version: 3.1.16   
### Date: 2017-05-03
 - *bugfix* --xpra-wayland in check for WAYLAND_DISPLAY

## Version: 3.1.15   
### Date: 2017-05-02
 - minor *bugfix* in choosing terminal, replace $Waylandterminal with $Terminal in re-check
 - minor *bugfix* xtermrc and xinitrc: check if $Dockerpidfile is not empty
 - faster startup for --xpra-xwayland, --weston-xwayland, --kwin and --kwin-xwayland
 - code cleanup

## Version: 3.1.14   
### Date: 2017-05-01
 - checkorphaned() uses container names instead of numbers
 - *bugfix* --exe: reliable kill $Hostexe, even with --weston* and --kwin*
 - *bugfix*: remove : and / from image name in $Containername

## Version: 3.1.13   
### Date: 2017-04-30
 - Improved multimonitor support (still missing: multihead)
 - *bugfix*: redirection of stderr wihout cat, avoids broken pipe on ctrl-c in ubuntu and opensuse
 - *bugfix*: removed custom socket in xpra (failed in opensuse)
 - removed $Cidfile at all, cleanup hint in finish() with $Containername
 - avoid root ownership for $Dockerlogfile and $Dockerpidfile

## Version: 3.1.12   
### Date: 2017-04-29
 - clean up confusion with x11docker.log
 - minor *bugfix*: include warning() in xinitrc
 - *bugfix* in xinitrc for --no-xhost
 - don't share $Xclientcookie as $Sharefolder is already shared
 - don't use $Cacherootfolder for parsererror
 - hint to use --sudo on some systems
 - use id -g instead of $Benutzer for group name
 - add lsb-release -ds to verbose output

## Version: 3.1.11   
### Date: 2017-04-29
 - disabled $Cidfile as not important and due to [#10](https://github.com/mviereck/x11docker/issues/10)

## Version: 3.1.10   
### Date: 2017-04-28
 - minor *bugfix*: check for xenial instead of 16.04/xvfb
 - regression fix: set XPRA_XSHM=0 on Shareipc=no
 - disable --desktop-scaling in xpra, not supported before xpra v1.x

## Version: 3.1.9    
### Date: 2017-04-27
 - don't create Cacherootfolder in variable definitions
 - check for Xvfb on Ubuntu 16.04

## Version: 3.1.8    
### Date: 2017-04-25
 - Add advice for --xorg how to setup xserver-xorg-legacy

## Version: 3.1.7    
### Date: 2017-04-25
 - --xpra and --xdummy now use Xvfb if installed. Compare #9, Xdummy cannot be used on Ubuntu 16.04 due to xorg.conf location
 - set $Windowmanager in auto choosing X server if switching to desktop windows

## Version: 3.1.6    
### Date: 2017-04-21
 - *bugfix* 2 --nxagent: don't close nxagent on every call of nxclient

## Version: 3.1.5    
### Date: 2017-04-20
 - *bugfix* --nxagent: don't close nxagent on every call of nxclient

## Version: 3.1.4    
### Date: 2017-04-19
 - --nxagent supports untrusted cookies
 - *bugfix*: don't set dpi if xdpyinfo fails

## Version: 3.1.3    
### Date: 2017-04-18
 - --nxagent cookie workaround as it ignores XAUTHORITY on option -auth
 - --nxagent workaround to terminate on pressing window close button -> fake nxclient
 - *bugfix* typo in finish() looking for docker pid

## Version: 3.1.2    
### Date: 2017-04-18
 - --nxagent sets right keyboard layout, thanks to Ulrich!

## Version: 3.1.1    
### Date: 2017-04-18
 - --nxagent now supports --size, --fullscreen and --clipboard, thanks to Ulrich Sibiller from Arctica!
 - check dpi from host and set this to new X server
 - xpra xmessage to be patient
 - disabled keyboard adjusting for --nxagent

## Version: 3.1.0    
### Date: 2017-04-16
 - --nxagent: new X server option

## Version: 3.0.0    
### Date: 2017-04-15
 - Wayland support.
 - code cleanup
 - second stderr &3 to show warnings and errors also from within xinitrc and xtermrc
 - error messages on docker startup failure in xtermrc
 - --xhost changed to --xhost+, affects new X server only
 - --kwin und --kwin-wayland: new X server / wayland options
 - xdummy.conf or --xpra: custom modeline setting fittung to actual resolution
 - --xdummy regards --size
 - x11docker_CMD checks if ps is available
 - --wm changed, autochoosing no longer default
 - --desktop dismissed
 - old --env now is called --showenv
 - --env: *new option*: set custom envionment variables
 - --dbus: *new option*, run image command with dbus-launch
 - chmod 1777 /tmp/X11-unix to allow creation of X sockets in container
 - --verbose output much more reliebalenow, tail improved
 - use prefix unix for DISPLAY to disable MIT_SHM instead using other environment variables
 - --virtualgl dismissed
 - --dockerenv dismissed
 - --xpra-image --xorg-image --xdummy-image dismissed
 - --tcp --tcpxsocket --xsocket dismissed
 - --weston, --wayland: *new option*s for pure Wayland applications
 - --xpra-xwayland: new X server option
 - create dektop starter with basename instead of $0
 - createuser: start with --user=0 to allow useradd and su
 - --setwaylandenv: *new option* setting environment variables for toolkits like QT and GTK to use wayland
 - dismissed --glamor, now always enabled.
 - dismissed --sharegpu: same is done with --gpu
 - --nothing: Provide no X or Wayland server
 - --sharewayland: Share host wayland socket and set WAYLAND_DISPLAY
 - reverse order of killing of bgpids in finish(),last one first, to catch possible further output with tail -F
 - Newdisplaynumber for xorg starts with 8, Newxvt not added 7
 - xinitrc: XPRA_OPENGL_DOUBLE_BUFFERED=1 to avoid xpra bug 1469
 - check and set $XDG_RUNTIME_DIR for weston and Xwayland
 - --weston-xwayland and --xwayland: new X server options

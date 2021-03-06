# linux

**beta software! proceed with caution**

npm installs [hypercore linux](https://github.com/maxogden/hypercore) (based on [tiny core linux](http://tinycorelinux.net/)) and runs it as a daemon using the new Mac OS Yosemite hypervisor (via [xhyve](https://github.com/mist64/xhyve)).

This module is a low level component that is part of [HyperOS](http://hyperos.io/). We are working on integrating the other HyperOS components to support advanced functionality like running containers, sharing filesystems etc.

Mac OS Yosemite only for now, Windows support coming later through Hyper-V integration (see [this issue](https://github.com/maxogden/linux/issues/4) if you wanna help)

**WARNING**
-----------
 - xhyve is a very new project, expect bugs! You must be running OS X 10.10.3 Yosemite or later and 2010 or later Mac for this to work.
 - if you happen to be running any version of VirtualBox prior to 4.3.30 or 5.0 then xhyve will crash your system either if VirtualBox is running or had been run previously after the last reboot (see xhyve's issues [#5](mist64/xhyve#5) and [#9](mist64/xhyve#9) for the full context). So, if you are unable to update VirtualBox to version 4.3.30 or 5, or later, and were using it in your current session please do restart your Mac before attempting to run xhyve.
 - (these warnings were borrowed from [coreos-xhyve](https://github.com/coreos/coreos-xhyve))
 
[![js-standard-style](https://cdn.rawgit.com/feross/standard/master/badge.svg)](https://github.com/feross/standard)
[![Build Status](https://travis-ci.org/maxogden/linux.svg?branch=master)](https://travis-ci.org/maxogden/linux)

### installation

```
npm install linux -g
```

### usage

Quickstart:

1. Run `linux init` in a folder where you want to store your linux runtime config
2. Run `sudo linux boot` to start the local linux server daemon
3. Run `linux ssh` to log in to the server daemon over ssh
4. Run `linux halt` to stop the server daemon when you're done

```
$ linux
Usage:     linux <command> [args...]

Commands:
  init     creates a new ./linux folder in this directory to hold config
  boot     boots up linux from config in ./linux
  status   checks if linux is running or not
  ssh      sshes into linux and attaches the session to your terminal
  run      runs a single command over ssh
  halt     runs sudo halt in linux, initiating a graceful shutdown
  kill     immediately ungracefully kills the linux process with SIGKILL
  pid      get the pid of the linux process
  ps       print all linux processes running on this machine
```

### example

```
# initialize a linux folder to hold state
$ linux init
Created new config folder at /Users/max/test/linux

# starts a linux daemon
$ sudo linux boot
Linux has booted { ip: '192.168.64.127',
  hostname: 'simon-mittens-snuggles-toby',
  pid: 20665 }

# ssh login
$ linux ssh
Warning: Permanently added '192.168.64.127' (ECDSA) to the list of known hosts.
 __    __    __
/  \__/  \__/  \__   Welcome to HyperOS Linux! (Based on TinyCore Linux)
\__/  \__/  \__/  \        hyperos.io              tinycorelinux.net
   \__/  \__/  \__/
tc@simon-mittens-snuggles-toby:~$ pwd
/home/tc
tc@simon-mittens-snuggles-toby:~$ exit
Connection to 192.168.64.127 closed.

# run a single command over ssh
$ linux run uname -a
Linux simon-mittens-snuggles-toby 3.16.6-tinycore64 #777 SMP Thu Oct 16 10:21:00 UTC 2014 x86_64 GNU/Linux

$ linux status
Linux is running { pid: 20665 }

# gracefully shutdown
$ linux halt

$ linux status
Linux is not running
```

# special thanks

- thanks to [nlf](https://github.com/nlf) (Nathan LaFreniere) for help, if you like docker you should definitely check out his projects [dhyve](https://github.com/nlf/dhyve) and [dhyve-os](https://github.com/nlf/dhyve-os/)
- thanks to [tiny core linux](http://tinycorelinux.net/) for being awesome
- thanks to [boot2docker](https://github.com/boot2docker/boot2docker) for some stuff I borrowed from their [rootfs folder](https://github.com/boot2docker/boot2docker/tree/master/rootfs/rootfs)

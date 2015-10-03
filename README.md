A collection of notes I've made as part of setting up an Azure and AWS VMs to host games servers. I've tried with both OpenSuse 13.2 and Amazon Linux.

# Misc Housekeeping

## For OpenSuse

Before getting started I grabbed the `man` package `sudo zypper install man`. Because I want me some manuals and apropos and what not.

## For Both Dists

Update manual database: `sudo mandb`. Now I can apropos manuals, which while not strictly needed is certainly helpful for noodling around.

I also grab all my security updates and all the other housekeeping stuff which is a good idea to do, which I use a combination of `yast` (command line interface) and `zypper` to do.

### Getting Tmux

I also grab [tmux](https://tmux.github.io/) `sudo zypper install tmux` (OpenSuse)/`sudo yum install tmux`, as it helps with coordinating different running servers.

# Setting up a Steam User

Depending on the VM I may have a game user by default, but I want to set up an explicit steam on for SteamCMD.

## For OpenSuse

In yast add a new user "steam", set a password (whatevr - I'm about to disable it anyway), and disable user login.

## For Amazon Linux

Add a new user via `sudo adduser steam`.

## For Both Dists

After doing that I use `sudo passwd -l steam` to lock that accounts password. This means that you can't log into this account with a password. The only realistic way you can get to this account at this point is `sudo su -l steam` (the -i does:*Provide an environment similar to what the user would expect had the user logged in directly.*, which means we don't leak any user state to that account).

# Installing Required Libs

## For OpenSuse

64 bit Open Suse required me to install the following: `libstdc++6-32bit`, which brought in all the required deps for SteamCMD.

## For Amazon Linux

Amazon linux required me to bring in `libstdc++44.i686` (`sudo yum install libstdc++44.i686`), which was all the deps needed for SteamCmd.

# Getting SteamCMD

[This](https://developer.valvesoftware.com/wiki/SteamCMD) page has up to date details with how to grab SteamCMD.

To summarize (all as the steam user):

- Grab SteamCMD: `mkdir ~/steamcmd`, `cd ~/steamcmd`, `wget https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz`
- Extract: `tar -xvzf steamcmd_linux.tar.gz`
- Run that sucker: `./steamcmd.sh`

# Install Games

The procedure is similar for various games. Some games will require that you're logging in as a user that owns the game, others will allow anonymous access.

Some examples follow.

## Terraria

You need to be logged in with an account that owns Terraria

- Set the directory to install to: `force_install_dir ./terraria/`
- Install with `app_update 105600`

Once that's done, then you're good to go, there's a `TerrariaServer` file in the installation directory to start up the server

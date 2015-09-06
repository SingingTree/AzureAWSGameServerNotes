A collection of notes I've made as part of setting up an Azure VM to host games servers. The OS for this VM is OpenSuse 13.2.

# Misc Housekeeping

Before getting started I grabbed the `man` package `sudo zypper install man` and updated my manual database: `sudo mandb`. Now I can apropos manuals, which while not strictly needed is certainly helpful for noodling around.

I also grab all my security updates and all the other housekeeping stuff which is a good idea to do, which I use a combination of `yast` (command line interface) and `zypper` to do.

# Getting Tmux

I also grab [tmux](https://tmux.github.io/) `sudo zypper install tmux`, as it helps with coordinating different running servers.

# Setting up a Steam User

My Azure VM had a games user by default, but I want to set up an explicit steam on for SteamCMD. In yast I add a new user "steam", set a password (I'm about to disable it anyway), and disable user login. After doing that I use `sudo passwd -l steam` to lock that accounts password. This means that you can't log into this account with a password. The only realistic way you can get to this account at this point is `sudo su -l steam` (the -i does:*Provide an environment similar to what the user would expect had the user logged in directly.*, which means we don't leak any user state to that account).

# Getting SteamCMD

[This](https://developer.valvesoftware.com/wiki/SteamCMD) page has up to date details with how to grab SteamCMD.

To summarize (all as the steam user):

- Grab SteamCMD: `mkdir ~/steamcmd`, `cd ~/steamcmd`,

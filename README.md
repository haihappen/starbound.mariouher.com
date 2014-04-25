# starbound.mariouher.com

## Setup

Add user.

```sh
adduser ubuntu
adduser ubuntu sudo
```

Copy SSH key (run on local machine).

```sh
ssh-copy-id -i ~/.ssh/uherdotmarioatgmaildotcom ubuntu@starbound.mariouher.com
```

Allow user to sudo.

```sh
echo "ubuntu ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
```

Disable login for root.

```sh
echo "
PermitRootLogin no
AllowUsers ubuntu
" >> /etc/ssh/sshd_config
service ssh reload
```

Upgrade to latest updates.

```sh
sudo aptitude update
sudo aptitude safe-upgrade
sudo aptitude full-upgrade
```

Install Steam. (http://starbounder.org/Guide:LinuxServerSetup)

```sh
sudo apt-get install lib32gcc1
sudo apt-get install libvorbisfile3
mkdir steam; cd steam
wget http://media.steampowered.com/installer/steamcmd_linux.tar.gz
tar -zxvf steamcmd_linux.tar.gz
rm steamcmd_linux.tar.gz
./steamcmd.sh
```

Install (and update) Starbound.

```
login <username> <password>
force_install_dir /home/ubuntu/starbound
app_update 211820
set_steam_guard_code <steam_guard_code>
quit
```

Copy `starbound.conf` into `/etc/init/starbound.conf`.

## Usage

```sh
ssh ubuntu@starbound.mariouher.com -i ~/.ssh/uherdotmarioatgmaildotcom

sudo [start|stop|restart] starbound
```

Logs are stored in `/var/log/upstart/starbound.conf`.

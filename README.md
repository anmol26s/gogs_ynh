# Gogs package for YunoHost

Gogs is a self-hosted Git service written in Go. Alternative to Github.
- [Gogs website](http://gogs.io)

## Requirements
A functional instance of [YunoHost](https://yunohost.org)

## Installation
From the command-line:

`sudo yunohost app install -l Gogs https://github.com/YunoHost-Apps/gogs_ynh`

## Upgrade
From the command-line:

`sudo yunohost app upgrade -u https://github.com/YunoHost-Apps/gogs_ynh gogs`

## Notes on SSH usage
If you want to use Gogs with ssh and be able to pull/push with you ssh key, your ssh daemon must be properly configured to use private/public keys. Here is a sample configuration of `/etc/ssh/sshd_config` that works with Gogs:

```bash
PubkeyAuthentication yes
AuthorizedKeysFile %h/.ssh/authorized_keys
ChallengeResponseAuthentication no
PasswordAuthentication no
UsePAM no
```

You also need to add your public key to your Gogs profile.

If you use ssh on another port than 22, you need to add theses lines to your ssh config in `~/.ssh/config`:

```bash
Host domain.tld
    port 2222 # change this with the port you use
```

## Info on upgrading from the old package version (gogs <0.9.xx)
Previous versions of this package used to build Gogs from sources instead of using the pre-compiled binary. It also left data in many places which was not good. The upgrade tries to take care of moving everything to the right place **BUT it's strongly advised to do a backup of your repositories and of the Gogs directory before the update**. Your avatars and issue attachments files may be lost in the process.

Also, in some cases, Gogs will not restart properly during the update. If so, you can rerun the update safely or try to start Gogs with `sudo systemctl restart gogs.service`.

Sources and issues of the old package can be found [here](https://github.com/YunoHost-Apps/gogs_ynh_old/)

## Info
Gogs v0.11

- [YunoHost forum thread](https://forum.yunohost.org/t/gogs-package-an-awesome-github-alternative/1127)

Architecture: this package is compatible with amd64, i386 and arm. The package will try to detect it with the command uname -m and fail if it can't detect the architecture. If that happens please open an issue describing your hardware and the result of the command `uname -m`.

## License
Gogs is published under the MIT License:
https://github.com/gogits/gogs/blob/master/LICENSE

This package is published under the MIT License.


## Developper info
Please do your pull requests to the `dev` branch.

Test or upgrade to dev version:
```bash
sudo su - admin
git clone -b dev https://github.com/YunoHost-Apps/gogs_ynh
# to install
sudo yunohost app install -l Gogs /home/admin/gogs_ynh
# to upgrade
sudo yunohost app upgrade -f /home/admin/gogs_ynh gogs

```

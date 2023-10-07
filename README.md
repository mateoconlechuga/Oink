<img src="Oink!.png" alt="Oink!" width="500"/>

## A lightweight DDNS client for [Porkbun](https://porkbun.com)


**Oink!** is an unofficial DDNS client for porkbun.com built in Go. **Oink!** only depends on Go's standard library.

---
### How to install
You can install **Oink!** using an [official package](https://github.com/RLado/Oink/releases) or by using *make*.

#### On distributions supporting .deb files (Debian, Ubuntu, ...)
```bash
dpkg -i <oink_pkg>.deb
```

#### On Arch-based distros
*Note: Also available in the [AUR](https://aur.archlinux.org/packages/oink)*
```bash
pacman -U <oink_pkg>.pkg.tar.zst 
```

#### Or you can build from source and install using *make*
> Requires *make* and *go*
```bash
make
sudo make install
```

You may **uninstall** using `sudo make uninstall` to remove **all** configuration files and binaries

---
### How to setup
The setup process is simple:

- If installed correctly you should find **Oink!**'s configuration file in */etc/oink_ddns/config.json*. Open the file with your text editor of choice.
- In the configuration file you should find the following contents that must be filled in:
> ⚠️ *In case you do not already have an API key, you will need to request one at: https://porkbun.com/account/api*
```json
{
    "global": {
        "secretapikey": "<your secret api key here>",
        "apikey": "<your api key here>",
        "interval": 900,
        "ttl": 600
    },
    "domains": [
        {
            "domain": "<your domain here>",
            "subdomain": "<your subdomain here>"
        }
    ]
}
```

If you want to update more than one domain or subdomain, you can add new domains like so:
```json
{
    "global": {
        "secretapikey": "<your secret api key here>",
        "apikey": "<your api key here>",
        "interval": 900,
        "ttl": 600
    },
    "domains": [
        {
            "secretapikey": "<override secret api key here>",
            "apikey": "<override api key here>",
            "domain": "<your domain here>",
            "subdomain": "<your subdomain here>",
            "ttl": 800
        },
        {
            "domain": "<your domain 2 here>",
            "subdomain": "<your subdomain 2 here>"
        }
    ]
}
```
> *Entries must at least contain the `domain` and `subdomain` fields.*

- Enable and start the service using `systemd`
> ⚠️ *Make sure to **enable** API ACCESS in your porkbun domain's control panel*
```bash
systemctl enable oink_ddns
systemctl start oink_ddns
```
- You are done! Your domain DNS record should update automatically


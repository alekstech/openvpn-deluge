# OpenVPN and Deluge in Docker

This is a two-container project.
- The `openvpn` container, which runs [OpenVPN](openvpn.net), a VPN client.
- The `deluge` container runs [Deluge](deluge-torrent.org), a torrent client. It uses the `openvpn` container for its network. 

## Usage

### 1. Set up bind mounts

Both containers require hard drive access for data storage. Make sure that these four folders exist in your file system.
- d:/Github/openvpn-deluge/openvpn/bind-mounts/net
- d:/Github/openvpn-deluge/openvpn/bind-mounts/vpn
- d:/media/
- d:/Github/openvpn-deluge/deluge/bind-mounts/deluge

You can change them to any other location by editing `docker-compose.yml`.

On Windows, you will want to make sure that the drive where your folders are located is available to Docker - see Docker > Settings > Resources > File sharing.

### 2. Add VPN settings

The `openvpn` container expects to find a configuration file in the folder called `client.openvpn` in the `vpn` folder:

```
d:/Github/openvpn-deluge/openvpn/bind-mounts/vpn/client.openvpn
```

If your VPN uses username and password authentication, one of the lines in `client.openvpn` will be
```
auth-user-pass
```

You can save your username and password in the same folder, in a file with username on line one and password on line two:

```
myvpnusername
myvpnpassword
```


If your file is called `vpn.auth`, you can edit the line in `client.openvpn` to be:
```
auth-user-pass /vpn/vpn.auth
```

### 3. Start the containers

Run `docker-compose up`.

### 4. Run Deluge

Visit [localhost:8112](localhost:8112) in your browser. You can change the port by editing `docker.compose.yml`.

To check that Deluge connects via the VPN, you may want to use [ipMagnet](http://ipmagnet.services.cbcdn.com/) or a similar service.

You will find downloaded files in d:/media/.

## Sources
Based on:
- https://github.com/dperson/openvpn-client
- https://github.com/kurankat/docker-deluge

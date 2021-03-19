# ZeroTier Starter Pack

**ZeroTier Starter Pack** is a Docker Compose project running a [ZeroTier](https://zerotier.com) client,
along with a [zerotier-dns](https://github.com/mje-nz/zerotier-dns) server assigning hostnames for the devices
connected to the network, and a [CoreDNS](https://github.com/coredns/coredns) server, 
forwarding queries to external resolvers.

In short, this will allow you to access your devices like so:
- `home-pc.zt.example.com`

## Requirements
* Docker
* Docker Compose

## Setting up
### Prerequisites
* Have a [ZeroTier network](https://my.zerotier.com/) set up.
* Have a [ZeroTier API key](https://my.zerotier.com/account).
* Have a domain name to be used as a DNS search domain (e.g. `example.com`)

### Configuration Files
Make a copy of the `zerotier-dns.example.yml` configuration and edit it:
```bash
cp zerotier-dns.example.yml zerotier-dns.yml
vim zerotier-dns.yml
```
Make sure you specify the `domain`, `api-key`, and `network`, at a minimum.
For full reference, please read the [zerotier-dns documentation](https://github.com/mje-nz/zerotier-dns/tree/815a3c35ea316d212e413f73c3fb130493283b3c).

Make a copy of the `Corefile.example` configuration file and edit it:
```bash
cp Corefile.example Corefile
vim Corefile
```
Make sure you replace the `zt.example.com` with your desired domain name. 
For full reference, please read the [CoreDNS forward plugin documentation](https://coredns.io/plugins/forward/).

### Run
Start the project:
```bash
docker-compose up
```

### ZeroTier Configuration
Join a network:
```bash
docker exec ztsp-zerotier-one zerotier-cli join <YOUR_NETWORK_ID>
```

Approve the node in the [ZeroTier Central](https://my.zerotier.com). 
Then make note of the node's IP and enter it in the **Server Address** field.
Use the same domain name you configured in the files, and enter it in the **Search Domain** field.

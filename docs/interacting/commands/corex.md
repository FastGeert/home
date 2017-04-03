# CoreX Management Commands

Available commands:

- [corex.create](#create)
- [corex.list](#list)
- [corex.terminate](#terminate)
- [corex.client](#client)


<a id="create"></a>
## corex.create

Creates a new container with the given root plist, mount points and ZeroTier ID, and connects it to the given bridges.


Arguments:

```javascript
{
    "plist": "http://url/to/plist",
    "mount": {
        "/host/directory": "/container/directory"
    },
    "network": {
        "zerotier": "zerotier network id", //options
        "bridge": [], //list of bridges names to connect to
    }
    //TODO:
    "port": {
        host_port: container_port,
    }
}
```

Arguments:

```javascript
{
  'root': {root_url},
  'mount': {mount},
  'network': {
      'zerotier': {zerotier},
      'bridge': {bridge},
  },
  'port': {port},
  'hostname': {hostname},
}
```

Values:

- **root_url**: the root filesystem plist

- **mount**: a dict with `{host_source: container_target}` mount points, where `host_source` directory must exists, `host_source` can be a URL to a plist to mount

- **zerotier**: An optional ZeroTier network ID to join

- **bridge**: list of tuples as `('bridge_name': 'network_setup')` where `network_setup` can be one of the following:
  - `''` or `'none'`: no IP is gonna be set on the link
  - `'dhcp'`: Run `udhcpc` on the container link, of course this will only work if the `bridge` is created with `dnsmasq` networking
  - `'CIDR'`: Assign static IP to the link

  Example: `bridge=[('br0', '127.0.0.100/24'), ('br1', 'dhcp')]`

- **port**: A dict of `host_port: container_port` pairs

  Example: `port={8080: 80, 7000:7000}`

- **hostname**: Specific hostname you want to give to the container, if None it will automatically be set to core-x, x being the ID of the container



### corex.list
Takes no arguments.
List all available `live` Cores on a host.

### corex.terminate
Arguemnts:
```javascript
{
    "container": container_id,
}
```
Destroys a Core and stops the Core processes. It takes a mandatory core ID.

### corex.dispatch
Arguments:
```javascript
{
     "container": core_id,
     "command": {
         //the full command payload
     }
}
```



<a id="list"></a>
### container.list

<a id="terminate"></a>
### container.terminate

<a id="client"></a>
### container.client

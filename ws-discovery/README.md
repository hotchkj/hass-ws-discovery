# WS-Discovery Home Assistant Add-on

![Supports amd64 Architecture][amd64-shield]
![Supports aarch64 Architecture][aarch64-shield]
![Supports armhf Architecture][armhf-shield]
![Supports armv7 Architecture][armv7-shield]
![Supports i386 Architecture][i386-shield]

## About

This add-on provides WS-Discovery (Web Services Dynamic Discovery) support for Home Assistant. It makes Linux/Samba servers visible in the Windows Network Browser, allowing Windows computers to discover your Home Assistant server and any Samba shares on your network.

This add-on uses [wsdd](https://github.com/christgau/wsdd) by Steffen Christgau - a Python implementation of a WS-Discovery server that implements the LLMNR and WS-Discovery protocols. The wsdd implementation is sourced directly from the official repository at https://github.com/christgau/wsdd.

## Installation

1. Click the Home Assistant My button below to open the add-on on your Home Assistant instance:

   [![Open your Home Assistant instance and show the add-on store.](https://my.home-assistant.io/badges/supervisor_store.svg)](https://my.home-assistant.io/redirect/supervisor_store/)

2. Search for "WS-Discovery" and install the add-on
3. Configure the add-on (see Configuration section below)
4. Start the add-on
5. Check the logs to see if everything is working correctly

## Configuration

Add-on configuration example:

```yaml
workgroup: WORKGROUP
hostname: ""
domain: ""
interface: ""
verbose: false
ipv4only: false
ipv6only: false
```

### Basic Options

#### `workgroup`
The Windows workgroup name. Default is `WORKGROUP`.

#### `hostname`
The hostname to advertise. If left empty, the system hostname will be used.

#### `domain`
Report being a member of an Active Directory domain. If set, this disables the workgroup option. Leave empty if not using AD.

#### `interface`
Specify the network interface or IP address to use for WS-Discovery traffic. For example: `eth0` or `192.168.1.10`. Leave empty to use all available interfaces.

#### `verbose`
Enable verbose logging for debugging. Default is `false`.

### Advanced Options

#### `hoplimit`
Hop limit for multicast packets. Default is `1` (link-local only). Range: 1-255.

#### `uuid`
Specify a custom UUID for the target device. Leave empty to auto-generate.

#### `no_autostart`
Do not start networking after launch. Default is `false`.

#### `no_http`
Disable HTTP service (useful for debugging). Default is `false`.

#### `ipv4only`
Use only IPv4. Default is `false`.

#### `ipv6only`
Use IPv6 only. Default is `false`.

#### `shortlog`
Log only level and message (shorter log format). Default is `false`.

#### `preserve_case`
Preserve case of the provided/detected hostname. Default is `false`.

#### `chroot`
Directory to chroot into. Leave empty for no chroot.

#### `user`
Drop privileges to specified user:group. Leave empty to run as default user.

#### `discovery`
Enable discovery operation mode. Default is `false`.

#### `listen`
Listen on path or localhost port in discovery mode. Leave empty for default.

#### `no_host`
Disable server mode operation (host will be undiscoverable). Default is `false`.

#### `metadata_timeout`
Set timeout for HTTP-based metadata exchange. Leave empty for default.

#### `source_port`
Send multicast traffic/receive replies on this port. Leave empty for default.

## Support

Got questions?

You could open an issue on GitHub:

- [Open an issue](https://github.com/hotchkj/Home-Assistant-WSD/issues)

## License

MIT License - see [LICENSE](../LICENSE) file for details.

The underlying [wsdd](https://github.com/christgau/wsdd) implementation is licensed under the MIT License.

[amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg
[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[armhf-shield]: https://img.shields.io/badge/armhf-yes-green.svg
[armv7-shield]: https://img.shields.io/badge/armv7-yes-green.svg
[i386-shield]: https://img.shields.io/badge/i386-yes-green.svg

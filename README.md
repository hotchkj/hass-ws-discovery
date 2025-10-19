# WS-Discovery Home Assistant Add-on Repository

![Supports amd64 Architecture][amd64-shield]
![Supports aarch64 Architecture][aarch64-shield]
![Supports armhf Architecture][armhf-shield]
![Supports armv7 Architecture][armv7-shield]
![Supports i386 Architecture][i386-shield]

## About

This repository contains a Home Assistant add-on that provides WS-Discovery (Web Services Dynamic Discovery) support. It makes Linux/Samba servers visible in the Windows Network Browser, allowing Windows computers to discover your Home Assistant server and any Samba shares on your network.

This add-on uses [wsdd](https://github.com/christgau/wsdd) by Steffen Christgau - a Python implementation of a WS-Discovery server that implements the LLMNR and WS-Discovery protocols. The wsdd implementation is sourced directly from the official repository at https://github.com/christgau/wsdd.

## Installation

### Add the Repository

1. Navigate to the Supervisor Add-on Store in Home Assistant
2. Click on the three dots in the top right corner and select "Repositories"
3. Add this repository URL: `https://github.com/hotchkj/hass-ws-discovery`
4. Find "WS-Discovery" in the add-on store and click it
5. Click "Install"
6. Configure the add-on (see Configuration section below)
7. Start the add-on
8. Check the logs to see if everything is working correctly

Alternatively, click the button below to add this repository automatically:

[![Open your Home Assistant instance and show the add add-on repository dialog with this repository URL pre-filled.](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fhotchkj%2Fhass-ws-discovery)

## Configuration

Add-on configuration example:

```yaml
workgroup: WORKGROUP
hostname: ""
domain: ""
interface: ""
verbose: false
```

For detailed configuration options, see the [add-on README](ws-discovery/README.md). The add-on supports all wsdd command line options including:

- **Basic options**: workgroup, hostname, domain, interface, verbose
- **Advanced options**: hoplimit, uuid, ipv4only, ipv6only, preserve_case, and more

### Common Options

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

## Support

Got questions?

You could open an issue on GitHub:

- [Open an issue](https://github.com/hotchkj/hass-ws-discovery/issues)

## License

MIT License - see [LICENSE](LICENSE) file for details.

The underlying [wsdd](https://github.com/christgau/wsdd) implementation is licensed under the MIT License.

[amd64-shield]: https://img.shields.io/badge/amd64-yes-green.svg
[aarch64-shield]: https://img.shields.io/badge/aarch64-yes-green.svg
[armhf-shield]: https://img.shields.io/badge/armhf-yes-green.svg
[armv7-shield]: https://img.shields.io/badge/armv7-yes-green.svg
[i386-shield]: https://img.shields.io/badge/i386-yes-green.svg

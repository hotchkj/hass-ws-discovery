# Home Assistant Add-on: WS-Discovery

## How to use

This add-on provides WS-Discovery (Web Services Dynamic Discovery) support, making your Home Assistant server discoverable by Windows computers on your network. It implements the LLMNR and WS-Discovery protocols to make your Home Assistant instance appear in the Windows Network Browser.

### Getting Started

1. Configure the add-on (see Configuration section below)
2. Start the add-on
3. Check the logs to verify it's running correctly
4. Your Home Assistant should now appear in Windows Network Browser

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

### Basic Configuration Options

#### `workgroup` (string, required)

The Windows workgroup name that this device should join. This must match the workgroup used by Windows computers on your network for them to discover this device.

**Default**: `WORKGROUP`

**Example**: `HOME` or `OFFICE`

#### `hostname` (string, optional)

The hostname to advertise to Windows computers. If left empty, the system hostname will be used.

**Default**: Empty (uses system hostname)

**Example**: `homeassistant` or `ha-server`

#### `domain` (string, optional)

Report being a member of an Active Directory domain. When set, this disables the workgroup option. Only use this if you're integrating with an Active Directory environment.

**Default**: Empty (not domain joined)

**Example**: `company.local`

#### `interface` (string, optional)

Specify the network interface or IP address to use for WS-Discovery traffic. Useful in multi-homed systems or when you want to limit discovery to specific networks.

**Default**: Empty (all available interfaces)

**Examples**: 
- `eth0` - Use specific network interface
- `192.168.1.100` - Use specific IP address
- `wlan0` - Use WiFi interface

#### `verbose` (boolean)

Enable verbose logging for debugging purposes. When enabled, the add-on will log detailed information about discovery requests and responses.

**Default**: `false`

### Advanced Configuration Options

#### `hoplimit` (integer)

Hop limit for multicast packets. Controls how far multicast packets can travel through routers.

**Default**: `1` (link-local only)
**Range**: 1-255

#### `uuid` (string, optional)

Specify a custom UUID for the target device. Leave empty to auto-generate a unique identifier.

**Default**: Empty (auto-generated)

#### `no_autostart` (boolean)

Do not start networking immediately after launch. Useful for debugging or custom initialization.

**Default**: `false`

#### `no_http` (boolean)

Disable HTTP service. Useful for debugging WS-Discovery protocol without HTTP metadata exchange.

**Default**: `false`

#### `ipv4only` (boolean)

Use only IPv4 protocol for discovery. Disable IPv6 support completely.

**Default**: `false`

#### `ipv6only` (boolean)

Use only IPv6 protocol for discovery. Disable IPv4 support completely.

**Default**: `false`

#### `shortlog` (boolean)

Use shorter log format showing only level and message. Reduces log verbosity.

**Default**: `false`

#### `preserve_case` (boolean)

Preserve the exact case of the provided or detected hostname instead of converting to lowercase.

**Default**: `false`

#### `chroot` (string, optional)

Directory to chroot into for enhanced security. Leave empty for no chroot operation.

**Default**: Empty (no chroot)

#### `user` (string, optional)

Drop privileges to the specified user:group after startup. Format: `username` or `username:groupname`.

**Default**: Empty (run as default user)

#### `discovery` (boolean)

Enable discovery operation mode for debugging. Allows the daemon to perform discovery operations.

**Default**: `false`

#### `listen` (string, optional)

Listen on specific path or localhost port in discovery mode. Used with discovery option.

**Default**: Empty (use defaults)

#### `no_host` (boolean)

Disable server mode operation. The host will be undiscoverable but can still perform discovery of other devices.

**Default**: `false`

#### `metadata_timeout` (string, optional)

Set timeout for HTTP-based metadata exchange operations.

**Default**: Empty (use default timeout)

#### `source_port` (string, optional)

Send multicast traffic and receive replies on this specific port number.

**Default**: Empty (use default port)

## Quick Setup

For most users, the default configuration works out of the box:

1. Ensure your `workgroup` matches your Windows network (usually `WORKGROUP`)
2. Start the add-on
3. Your Home Assistant should now appear in Windows Network Browser

### Network Requirements

This add-on requires `host_network: true` to function properly because it needs to:

- Listen on multicast addresses (239.255.255.250 for IPv4, ff02::c for IPv6)
- Respond with correct network interface information
- Bind to system ports (UDP 3702 for WS-Discovery)
- Access network interface details for proper advertisement

### Common Use Cases

#### Home Network Setup

```yaml
workgroup: WORKGROUP
hostname: homeassistant
verbose: false
```

#### Office/Enterprise Network

```yaml
workgroup: OFFICE
hostname: ha-server
interface: eth0
verbose: false
```

#### Active Directory Integration

```yaml
domain: company.local
hostname: homeassistant
interface: 192.168.10.100
```

## Troubleshooting

### Add-on Won't Start

- Check the logs for specific error messages
- Ensure no other service is using WS-Discovery ports
- Verify `host_network: true` is enabled

### Windows Can't Discover Home Assistant

1. **Verify workgroup**: Ensure the `workgroup` setting matches your Windows computers
2. **Check firewall**: Disable firewall temporarily to test if it's blocking multicast traffic
3. **Network connectivity**: Ensure Home Assistant and Windows computers are on the same subnet
4. **Enable verbose logging**: Set `verbose: true` to see discovery requests and responses
5. **Check Windows services**: Ensure "Function Discovery Resource Publication" service is running on Windows

### Discovery Works But Can't Access Services

- This add-on only provides discovery; actual services (like Samba) need to be configured separately
- Ensure file sharing services are properly configured and accessible
- Check that required ports for your services (e.g., 445 for SMB) are open

### Debugging Steps

1. Enable verbose logging:
   ```yaml
   verbose: true
   ```

2. Check the add-on logs for error messages or discovery activity

3. Test from Windows command prompt:
   ```cmd
   ping homeassistant.local
   nslookup homeassistant
   ```

4. Use network tools to verify multicast traffic:
   ```bash
   tcpdump -i any host 239.255.255.250
   ```

## Support

If you encounter issues:

- Check the [GitHub Issues](https://github.com/hotchkj/hass-ws-discovery/issues) for known problems
- Review the [wsdd documentation](https://github.com/christgau/wsdd) for protocol-specific details
- Enable verbose logging and include log output when reporting issues

## License

MIT License - see [LICENSE](../LICENSE) file for details.

The underlying [wsdd](https://github.com/christgau/wsdd) implementation is licensed under the MIT License.
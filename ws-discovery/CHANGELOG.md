# Changelog

All notable changes to this add-on will be documented in this file.

## [0.1.3] - 2025-10-19

### Fixed
- Remove PNG files from Git LFS tracking so add-on icon displays correctly in Home Assistant
- Home Assistant Supervisor cannot fetch LFS files, causing icons to appear broken

### Changed
- Update .gitattributes to mark binary files but exclude PNG from LFS

## [0.1.0] - 2025-10-19

### Added
- Initial release of WS-Discovery add-on
- Custom Docker image built from wsdd v0.9 release
- Support for multiple architectures (amd64, aarch64, armhf, armv7, i386)
- Comprehensive support for all wsdd command line options:
  - Basic options: interface, hoplimit, uuid, verbose
  - Network options: domain, hostname, workgroup
  - Advanced options: no-autostart, no-http, ipv4only, ipv6only
  - Logging options: shortlog
  - System options: preserve-case, chroot, user
  - Discovery options: discovery, listen, no-host
  - Timing options: metadata-timeout, source-port
- Host network mode for proper WS-Discovery functionality
- Configuration via YAML format (config.yaml)

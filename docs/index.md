---
hide:
    - navigation
---

<style>
.md-content .md-typeset h1 { display: none; }
</style>

<p align="center">
    <a href="https://paloaltonetworks.com"><img src="https://github.com/cdot65/pan-os-upgrade/blob/main/docs/images/logo.svg?raw=true" alt="PaloAltoNetworks"></a>
</p>
<p align="center">
    <em><code>pan-os-upgrade</code>, Automating PAN-OS and Panorama Upgrade Workflows</em>
</p>
<p align="center">
<a href="https://github.com/cdot65/pan-os-upgrade/graphs/contributors" target="_blank">
    <img src="https://img.shields.io/github/contributors/cdot65/pan-os-upgrade.svg?style=for-the-badge" alt="Contributors">
</a>
<a href="https://github.com/cdot65/pan-os-upgrade/network/members" target="_blank">
    <img src="https://img.shields.io/github/forks/cdot65/pan-os-upgrade.svg?style=for-the-badge" alt="Forks">
</a>
<a href="https://github.com/cdot65/pan-os-upgrade/stargazers" target="_blank">
    <img src="https://img.shields.io/github/stars/cdot65/pan-os-upgrade.svg?style=for-the-badge" alt="Stars">
</a>
<a href="https://github.com/cdot65/pan-os-upgrade/issues" target="_blank">
    <img src="https://img.shields.io/github/issues/cdot65/pan-os-upgrade.svg?style=for-the-badge" alt="Issues">
</a>
<a href="https://github.com/cdot65/pan-os-upgrade/blob/main/LICENSE" target="_blank">
    <img src="https://img.shields.io/github/license/cdot65/pan-os-upgrade.svg?style=for-the-badge" alt="License">
</a>
</p>

---

**Documentation**: <a href="https://cdot65.github.io/pan-os-upgrade/" target="_blank">https://cdot65.github.io/pan-os-upgrade/</a>

**Source Code**: <a href="https://github.com/cdot65/pan-os-upgrade" target="_blank">https://github.com/cdot65/pan-os-upgrade</a>

---

`pan-os-upgrade` is designed to provide network administrators and security professionals with an efficient tool to execute configuration backups, network state snapshots, system readiness checks, and operating system upgrades of Palo Alto Networks firewalls and Panorama appliances.

## Key Features

- **Three Unique Upgrade Workflows Supported**:
  - `firewall`: targets and upgrades an individual firewall
  - `panorama`: targets and upgrades an individual Panorama appliance
  - `batch`: targets a Panorama appliance and upgrades firewalls in batch
- **Automation of Routine Tasks**: Reduces manual errors and saves time by automating upgrades, configurations, and system checks.
- **Support for Direct and Proxy Connections**: Connect directly to firewalls or through a Panorama appliance, with support for targeting specific devices using filters.
- **Pre/Post Diff**: Network snapshots are taken before and after the upgrade process, providing a PDF report of changes within the network environment after the upgrade completes.
- **Active/Passive High Availability (HA) Workflow**: Fully supports upgrading devices in active/passive HA configurations, ensuring both members are properly upgraded and synchronized.
- **Multi-threading for Efficiency**: Utilizes multi-threading to parallelize upgrades, especially beneficial when upgrading multiple devices through Panorama, enhancing performance and reducing overall upgrade time.
- **Customizable and Extensible**: Execution of the script can be tailored to fit diverse network environments and requirements, offering flexibility for various deployment scenarios.
- **Comprehensive PAN-OS Interactions**: Facilitates extensive interactions with Palo Alto Networks appliances for operations like readiness checks, state snapshots, and report generation.

---

### Logic Workflow

You can view the logical workflow of the `pan-os-upgrade` subcommands by viewing these diagrams:

- [pan-os-upgrade firewall](https://link.excalidraw.com/readonly/JYX3bXR6dS8Eoejmpcfx?darkMode=true)
- [pan-os-upgrade panorama](https://link.excalidraw.com/readonly/lFTV51plR0DBR5FdkC5Y?darkMode=true)
- [pan-os-upgrade batch](https://link.excalidraw.com/readonly/hNOeOAWRlk4t9uKBfPVE?darkMode=true)

---

## Execution

There are two primary methods to execute the `pan-os-upgrade` tool:

- Python virtual environment
- Docker container image

### Python Virtual Environment Workflow

This approach involves setting up a Python virtual environment and running `pan-os-upgrade` within this isolated environment, ensuring compatibility and preventing any conflicts with system-wide Python installations.

#### Python Virtual Environment Features

- Easy and isolated Python environment setup.
- Full control over the Python version and dependencies.
- Ideal for users familiar with Python and virtual environments.

#### Python Getting Started

Install `pan-os-upgrade` via pip in a Python virtual environment and configure it using command-line arguments or an interactive shell. Detailed instructions can be found in the [User Guide](user-guide/python/getting-started.md).

### Docker Container Workflow

Running `pan-os-upgrade` in a Docker container encapsulates the tool and its dependencies in an isolated environment, simplifying setup and ensuring consistency across different systems.

#### Docker Key Features

- Simplified setup process with Docker.
- Consistent runtime environment regardless of the host system.
- Suitable for users who prefer Docker or require containerized environments.

#### Docker Getting Started

Pull the `pan-os-upgrade` Docker image, run the container with mounted directories for outputs, and interact with the tool in an isolated environment. More information is available in the [User Guide](user-guide/docker/getting-started.md).

---

Visit the [User Guide](user-guide/introduction.md) for detailed insights into setting up and running `pan-os-upgrade` using either Python or Docker workflows.

---

## Example Execution

<div class="termy">

```console
❯ pan-os-upgrade batch
Panorama hostname or IP: panorama1.cdot.io
Panorama username: officehours
Panorama password:
Firewall target version (ex: 10.1.2): 10.1.3-h3
Dry Run? [Y/n]: n
=================================================================================================
Welcome to the PAN-OS upgrade tool

This script software is provided on an 'as-is' basis with no warranties, and no support provided.

The selected `batch` subcommand will upgrade one or more firewalls.

Settings: No settings.yaml file was found, default values will be used.
You can create a settings.yaml file with 'pan-os-upgrade settings' command.

Inventory: No inventory.yaml file was found, firewalls will need be selected through the menu.
You can create an inventory.yaml file with 'pan-os-upgrade inventory' command.
=================================================================================================
🚀 panorama1.cdot.io: Connection to the appliance successful.
✅ panorama1.cdot.io: Connection to Panorama established. Firewall connections will be proxied!
🔧 panorama1.cdot.io: Retrieving a list of all firewalls connected to Panorama...
🔧 panorama1.cdot.io: Retrieving detailed information of each firewall...
╒═════╤════════════╤════════════════╤═════════╤═══════════╤═══════════╤═══════════╤═══════════╕
│   # │ Hostname   │ IP Address     │ Model   │ PAN-OS    │ Content   │ HA Mode   │ Preempt   │
╞═════╪════════════╪════════════════╪═════════╪═══════════╪═══════════╪═══════════╪═══════════╡
│   1 │ katy-fw1   │ 192.168.255.41 │ PA-VM   │ 10.1.3-h3 │ 8799-8509 │ passive   │ no        │
├─────┼────────────┼────────────────┼─────────┼───────────┼───────────┼───────────┼───────────┤
│   2 │ katy-fw2   │ 192.168.255.42 │ PA-VM   │ 10.1.3-h3 │ 8799-8509 │ active    │ no        │
├─────┼────────────┼────────────────┼─────────┼───────────┼───────────┼───────────┼───────────┤
│   3 │ lab-fw1    │ 192.168.255.11 │ PA-VM   │ 10.1.3    │ 8729-8157 │ disabled  │ N/A       │
├─────┼────────────┼────────────────┼─────────┼───────────┼───────────┼───────────┼───────────┤
│   4 │ lab-fw2    │ 192.168.255.12 │ PA-VM   │ 10.1.3    │ 8729-8157 │ disabled  │ N/A       │
├─────┼────────────┼────────────────┼─────────┼───────────┼───────────┼───────────┼───────────┤
│   5 │ lab-fw3    │ 192.168.255.13 │ PA-VM   │ 10.1.3    │ 8729-8157 │ disabled  │ N/A       │
├─────┼────────────┼────────────────┼─────────┼───────────┼───────────┼───────────┼───────────┤
│   6 │ lab-fw4    │ 192.168.255.14 │ PA-VM   │ 10.1.3    │ 8729-8157 │ disabled  │ N/A       │
├─────┼────────────┼────────────────┼─────────┼───────────┼───────────┼───────────┼───────────┤
│   7 │ lab-fw5    │ 192.168.255.15 │ PA-VM   │ 10.1.3    │ 8729-8157 │ disabled  │ N/A       │
├─────┼────────────┼────────────────┼─────────┼───────────┼───────────┼───────────┼───────────┤
│   8 │ lab-fw6    │ 192.168.255.16 │ PA-VM   │ 10.1.4-h4 │ 8729-8157 │ active    │ yes       │
├─────┼────────────┼────────────────┼─────────┼───────────┼───────────┼───────────┼───────────┤
│   9 │ lab-fw7    │ 192.168.255.17 │ PA-VM   │ 10.1.4-h4 │ 8729-8157 │ passive   │ yes       │
╘═════╧════════════╧════════════════╧═════════╧═══════════╧═══════════╧═══════════╧═══════════╛
You can select devices by entering their numbers, ranges, or separated by commas.
Examples: '1', '2-4', '1,3,5-7'.
Type 'done' on a new line when finished.

Enter your selection(s): 3-4
  - lab-fw1 selected.
  - lab-fw2 selected.
Enter your selection(s): done
🔧 panorama1.cdot.io: Selected 2 firewalls from inventory.yaml for upgrade.
📝 panorama1.cdot.io: Upgrading 2 devices to version 10.1.3-h3...
📝 panorama1.cdot.io: Please confirm the selected firewalls:
  - lab-fw1 (192.168.255.11)
  - lab-fw2 (192.168.255.12)
🟧 panorama1.cdot.io: Dry run mode is disabled, upgrade workflow will be executed.
📝 panorama1.cdot.io: Do you want to proceed with the upgrade? [y/N]: y
🚀 Proceeding with the upgrade...
🚀 Proceeding with the upgrade...
🔧 panorama1.cdot.io: Using 10 threads.
📝 lab-fw1: 007054000654321 192.168.255.41
📝 lab-fw2: 007054000654322 192.168.255.42
📝 lab-fw1: HA mode: active
📝 lab-fw2: HA mode: passive
📝 lab-fw1: Local state: active, Local version: 10.1.3, Peer version: 10.1.3
📝 lab-fw1: Version comparison: equal
🔍 lab-fw1: Detected active target device in HA pair running the same version as its peer. Added target device to revisit list.
📝 lab-fw2: Local state: passive, Local version: 10.1.3, Peer version: 10.1.3
📝 lab-fw2: Version comparison: equal
📝 lab-fw2: Target device is passive
📝 lab-fw2: Current version: 10.1.3
📝 lab-fw2: Target version: 10.1.3-h3
✅ lab-fw2: Upgrade required from 10.1.3 to 10.1.3-h3
🔧 lab-fw2: Refreshing list of available software versions
✅ lab-fw2: version 10.1.3-h3 is available for download
✅ lab-fw2: Base image for 10.1.3-h3 is already downloaded
🚀 lab-fw2: Performing test to see if 10.1.3-h3 is already downloaded.
✅ lab-fw2: version 10.1.3-h3 already on target device.
✅ lab-fw2: 10.1.3-h3 has been downloaded and sync'd to HA peer.
🚀 lab-fw2: Performing snapshot of network state information.
🚀 lab-fw2: Attempting to capture network state snapshot (Attempt 1 of 3).
✅ lab-fw2: Network snapshot created successfully on attempt 1.
💾 lab-fw2: Network state snapshot collected and saved to assurance/snapshots/lab-fw2/pre/2024-02-25_04-14-15.json
🚀 lab-fw2: Performing readiness checks of target firewall.
🚀 lab-fw2: Performing readiness checks to determine if firewall is ready for upgrade.
✅ lab-fw2: Passed Readiness Check: Check if active support is available
🟨 lab-fw2: Skipped Readiness Check: Check if a given ARP entry is available in the ARP table
✅ lab-fw2: Passed Readiness Check: Check if there are pending changes on device
🟨 lab-fw2: Skipped Readiness Check: Check if the certificates' keys meet minimum size requirements
🟨 lab-fw2: Skipped Readiness Check: Running Latest Content Version
✅ lab-fw2: Passed Readiness Check: Check if any Dynamic Update job is scheduled to run within the specified time window
✅ lab-fw2: Passed Readiness Check: No Expired Licenses
🟨 lab-fw2: Skipped Readiness Check: Check if a there is enough space on the `/opt/panrepo` volume for downloading an PanOS image.
✅ lab-fw2: Passed Readiness Check: Checks HA pair status from the perspective of the current device
🟨 lab-fw2: Skipped Readiness Check: Check if a given IPsec tunnel is in active state
🟨 lab-fw2: Skipped Readiness Check: Check for any job with status different than FIN
🟨 lab-fw2: Skipped Readiness Check: Check if NTP is synchronized
✅ lab-fw2: Passed Readiness Check: Check if the clock is synchronized between dataplane and management plane
✅ lab-fw2: Passed Readiness Check: Check connectivity with the Panorama appliance
🟨 lab-fw2: Skipped Readiness Check: Check if a critical session is present in the sessions table
✅ lab-fw2: Readiness Checks completed
🚀 lab-fw2: Checking if HA peer is in sync.
✅ lab-fw2: HA peer sync test has been completed.
🚀 lab-fw2: Performing backup of configuration to local filesystem.
📝 lab-fw2: Not a dry run, continue with upgrade.
🚀 lab-fw2: Performing upgrade to version 10.1.3-h3.
📝 lab-fw2: The install will take several minutes, check for status details within the GUI.
🚀 lab-fw2: Attempting upgrade to version 10.1.3-h3 (Attempt 1 of 3).
Device 007054000654322 installing version: 10.1.3-h3
✅ lab-fw2: Upgrade completed successfully
🚀 lab-fw2: Rebooting the target device.
🟧 lab-fw2: Retry attempt 1 due to error: 007054000654322 not connected
🟧 lab-fw2: Retry attempt 2 due to error: 007054000654322 not connected
🟧 lab-fw2: Retry attempt 3 due to error: 007054000654322 not connected
🟧 lab-fw2: Retry attempt 4 due to error: 007054000654322 not connected
🟧 lab-fw2: Retry attempt 5 due to error: 007054000654322 not connected
🟧 lab-fw2: Retry attempt 6 due to error: 007054000654322 not connected
🟧 lab-fw2: Retry attempt 7 due to error: 007054000654322 not connected
🟧 lab-fw2: Retry attempt 8 due to error: 007054000654322 not connected
📝 lab-fw2: Current device version: 10.1.3-h3
✅ lab-fw2: Device rebooted to the target version successfully.
🚀 lab-fw2: Performing backup of configuration to local filesystem.
🔧 lab-fw2: Waiting for the device to become ready for the post upgrade snapshot.
🚀 lab-fw2: Performing snapshot of network state information.
🚀 lab-fw2: Attempting to capture network state snapshot (Attempt 1 of 3).
❌ lab-fw2: Error running snapshots: ElementTree.fromstring ParseError: junk after document element: line 1, column 3703
🚀 lab-fw2: Attempting to capture network state snapshot (Attempt 1 of 3).
✅ lab-fw2: Network snapshot created successfully on attempt 1.
💾 lab-fw2: Network state snapshot collected and saved to assurance/snapshots/lab-fw2/post/2024-02-25_04-32-05.json
💾 lab-fw2: Snapshot comparison PDF report saved to assurance/snapshots/lab-fw2/diff/2024-02-25_04-32-08_report.pdf
🚀 panorama1.cdot.io: Revisiting firewalls that were active in an HA pair and had the same version as their peers.
📝 lab-fw1: 007054000654321 192.168.255.41
📝 lab-fw1: HA mode: active
📝 lab-fw1: Local state: active, Local version: 10.1.3, Peer version: 10.1.3-h3
Waiting for HA synchronization to complete on lab-fw1. Attempt 1/3
HA synchronization complete on lab-fw1. Proceeding with upgrade.
📝 lab-fw1: Version comparison: older
📝 lab-fw1: Target device is on an older version
📝 lab-fw1: Suspending HA state of active
🟧 lab-fw1: Error received when suspending active target device HA state: argument of type 'NoneType' is not iterable
📝 lab-fw1: Current version: 10.1.3
📝 lab-fw1: Target version: 10.1.3-h3
✅ lab-fw1: Upgrade required from 10.1.3 to 10.1.3-h3
🔧 lab-fw1: Refreshing list of available software versions
✅ lab-fw1: version 10.1.3-h3 is available for download
✅ lab-fw1: Base image for 10.1.3-h3 is already downloaded
🚀 lab-fw1: Performing test to see if 10.1.3-h3 is already downloaded.
✅ lab-fw1: version 10.1.3-h3 already on target device.
✅ lab-fw1: 10.1.3-h3 has been downloaded and sync'd to HA peer.
🚀 lab-fw1: Performing snapshot of network state information.
🚀 lab-fw1: Attempting to capture network state snapshot (Attempt 1 of 3).
✅ lab-fw1: Network snapshot created successfully on attempt 1.
💾 lab-fw1: Network state snapshot collected and saved to assurance/snapshots/lab-fw1/pre/2024-02-25_04-33-26.json
🚀 lab-fw1: Performing readiness checks of target firewall.
🚀 lab-fw1: Performing readiness checks to determine if firewall is ready for upgrade.
✅ lab-fw1: Passed Readiness Check: Check if active support is available
🟨 lab-fw1: Skipped Readiness Check: Check if a given ARP entry is available in the ARP table
✅ lab-fw1: Passed Readiness Check: Check if there are pending changes on device
🟨 lab-fw1: Skipped Readiness Check: Check if the certificates' keys meet minimum size requirements
🟨 lab-fw1: Skipped Readiness Check: Running Latest Content Version
✅ lab-fw1: Passed Readiness Check: Check if any Dynamic Update job is scheduled to run within the specified time window
✅ lab-fw1: Passed Readiness Check: No Expired Licenses
🟨 lab-fw1: Skipped Readiness Check: Check if a there is enough space on the `/opt/panrepo` volume for downloading an PanOS image.
🟨 lab-fw1: Skipped Readiness Check: Checks HA pair status from the perspective of the current device
🟨 lab-fw1: Skipped Readiness Check: Check if a given IPsec tunnel is in active state
🟨 lab-fw1: Skipped Readiness Check: Check for any job with status different than FIN
🟨 lab-fw1: Skipped Readiness Check: Check if NTP is synchronized
✅ lab-fw1: Passed Readiness Check: Check if the clock is synchronized between dataplane and management plane
✅ lab-fw1: Passed Readiness Check: Check connectivity with the Panorama appliance
🟨 lab-fw1: Skipped Readiness Check: Check if a critical session is present in the sessions table
✅ lab-fw1: Readiness Checks completed
🚀 lab-fw1: Checking if HA peer is in sync.
✅ lab-fw1: HA peer sync test has been completed.
🚀 lab-fw1: Performing backup of configuration to local filesystem.
📝 lab-fw1: Not a dry run, continue with upgrade.
🚀 lab-fw1: Performing upgrade to version 10.1.3-h3.
📝 lab-fw1: The install will take several minutes, check for status details within the GUI.
🚀 lab-fw1: Attempting upgrade to version 10.1.3-h3 (Attempt 1 of 3).
Device 007054000654321 installing version: 10.1.3-h3
✅ lab-fw1: Upgrade completed successfully
🚀 lab-fw1: Rebooting the target device.
🟧 lab-fw1: Retry attempt 1 due to error: 007054000654321 not connected
🟧 lab-fw1: Retry attempt 2 due to error: 007054000654321 not connected
🟧 lab-fw1: Retry attempt 3 due to error: 007054000654321 not connected
🟧 lab-fw1: Retry attempt 4 due to error: 007054000654321 not connected
🟧 lab-fw1: Retry attempt 5 due to error: 007054000654321 not connected
🟧 lab-fw1: Retry attempt 6 due to error: 007054000654321 not connected
🟧 lab-fw1: Retry attempt 7 due to error: 007054000654321 not connected
📝 lab-fw1: Current device version: 10.1.3-h3
✅ lab-fw1: Device rebooted to the target version successfully.
🚀 lab-fw1: Performing backup of configuration to local filesystem.
🔧 lab-fw1: Waiting for the device to become ready for the post upgrade snapshot.
🚀 lab-fw1: Performing snapshot of network state information.
🚀 lab-fw1: Attempting to capture network state snapshot (Attempt 1 of 3).
✅ lab-fw1: Network snapshot created successfully on attempt 1.
💾 lab-fw1: Network state snapshot collected and saved to assurance/snapshots/lab-fw1/post/2024-02-25_04-50-28.json
💾 lab-fw1: Snapshot comparison PDF report saved to assurance/snapshots/lab-fw1/diff/2024-02-25_04-50-29_report.pdf
✅ panorama1.cdot.io: Completed revisiting firewalls

```

</div>

Here's an example of the PDF diff report that's generated:

<img src="https://github.com/cdot65/pan-os-upgrade/blob/main/docs/images/report.png?raw=true" alt="PDF">

For more examples and usage scenarios, refer to the [Documentation](https://cdot65.github.io/pan-os-upgrade/).

---

### Release Notes

Updates with each release are tracked at [Release Notes](about/release-notes.md).

### Contributing

Contributions are welcome and greatly appreciated. Visit the [Contributing](about/contributing.md) page for guidelines on how to contribute.

### License

This project is licensed under the Apache 2.0 License - see the [License](about/license.md) page for details.

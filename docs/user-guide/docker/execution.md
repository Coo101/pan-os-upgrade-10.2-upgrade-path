# Docker Execution for pan-os-upgrade

Run `pan-os-upgrade` in Docker for a consistent setup across systems. This guide details the steps for Docker configuration and execution, including Panorama proxy connections.

## Pulling the Docker Image

Pull the `pan-os-upgrade` image from GitHub Packages:

<div class="termy">

```console
docker pull ghcr.io/cdot65/pan-os-upgrade:latest
```

</div>

## Docker Setup

Before executing the tool, ensure your Docker environment is correctly set up.

### Prepare Directories

Create `assurance` and `logs` directories in your working directory to store outputs and logs:

<div class="termy">

```console
mkdir assurance logs
```

</div>

If you plan on customizing the settings of the script, create an empty `settings.yaml` in your working directory. This file will be filled out correctly when you run the `settings` argument when running the container image (see the `Advanced Settings` section):

<div class="termy">

```console
touch settings.yaml
```

</div>

### Run Docker Container

Before we get the execution, let's take a moment to review the flags that we need to pass at runtime.

#### Docker CLI flags

| flag   | description                                                             | required? |
| ------ | ----------------------------------------------------------------------- | --------- |
| -v     | mount files / folders from your local computer into the container       | yes       |
| -it    | let Docker know that you need an interactive session with the container | yes       |
| --rm   | remove the container after it completes its execution, good for hygiene | no        |
| --name | assign a name to the container instance                                 | no        |

##### Volume Mounts

We will need to create at least two volume mounts with Docker, this workflow allows us to have our local files available within the Docker container. When a Docker container completes its execution, the default behavior is to stop the container and this will prevent us from viewing the logs, snapshots, configuration backups, and readiness checks.

##### Interactive Teletype

Since we are using a CLI tool that requires interaction from us during its execution, we also need to flag the container to work in an interactive teletype session.

##### Optional Flags

If you'd like, you can assign a name to your container. This can help you create a friendly name for the container instance that will help you revisit it, should that prove necessary.

If you decide to assign your container a name that be common across multiple executions, you will want to also pass the `--rm` flag to remove the container after its execution completes. This is a good practice to reduce the amount of duplicate containers, but will prevent you from revisiting a specific container instance later on; this shouldn't be an issue since all logs, snapshots, checks, and backups are available in your host's current directory, thanks to the volume mounts.

#### Example Execution on macOS and Linux

In this example we will upgrade a firewall directly by using the `firewall` argument when executing the container. The `$(pwd)` on macOS and Linux is a shortcut for `full path to your current working directory`; feel free to simply run `pwd` from your terminal to get an understanding of the response.

<div class="termy">

```console
docker run -it ghcr.io/cdot65/pan-os-upgrade firewall
Firewall hostname or IP: lab-fw1.cdot.io
Firewall username: officehours
Firewall password:
Target version: 10.1.4
Dry Run? [Y/n]: n
=================================================================================================
Welcome to the PAN-OS upgrade tool

This script software is provided on an 'as-is' basis with no warranties, and no support provided.

The selected `firewall` subcommand will upgrade a single Firewall appliance.

Settings: Custom configuration loaded file detected and loaded at:
/app/settings.yaml
=================================================================================================
🚀 lab-fw1.cdot.io: Connection to the appliance successful.
📝 lab-fw1: 007054000654320 192.168.255.11
📝 lab-fw1: HA mode: disabled
📝 lab-fw1: Current version: 10.1.3-h3
📝 lab-fw1: Target version: 10.1.4
✅ lab-fw1: Upgrade required from 10.1.3-h3 to 10.1.4
🔧 lab-fw1: Refreshing list of available software versions
✅ lab-fw1: version 10.1.4 is available for download
✅ lab-fw1: Base image for 10.1.4 is already downloaded
🚀 lab-fw1: Performing test to see if 10.1.4 is already downloaded.
✅ lab-fw1: version 10.1.4 already on target device.
✅ lab-fw1: version 10.1.4 has been downloaded.
🚀 lab-fw1: Performing snapshot of network state information.
🚀 lab-fw1: Attempting to capture network state snapshot (Attempt 1 of 3).
✅ lab-fw1: Network snapshot created successfully on attempt 1.
💾 lab-fw1: Network state snapshot collected and saved to assurance/snapshots/lab-fw1/pre/2024-02-25_11-38-57.json
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
🟨 lab-fw1: Skipped Readiness Check: Check if the clock is synchronized between dataplane and management plane
✅ lab-fw1: Passed Readiness Check: Check connectivity with the Panorama appliance
🟨 lab-fw1: Skipped Readiness Check: Check if a critical session is present in the sessions table
✅ lab-fw1: Readiness Checks completed
🚀 lab-fw1: Performing backup of configuration to local filesystem.
📝 lab-fw1: Not a dry run, continue with upgrade.
🚀 lab-fw1: Performing upgrade to version 10.1.4.
📝 lab-fw1: The install will take several minutes, check for status details within the GUI.
🚀 lab-fw1: Attempting upgrade to version 10.1.4 (Attempt 1 of 3).
Device 007054000654320 installing version: 10.1.4
✅ lab-fw1: Upgrade completed successfully
🚀 lab-fw1: Rebooting the target device.
🟧 lab-fw1: Retry attempt 1 due to error: URLError: reason: [SSL: UNEXPECTED_EOF_WHILE_READING] EOF occurred in violation of protocol (_ssl.c:1000)
🟧 lab-fw1: Retry attempt 2 due to error: URLError: reason: [SSL: UNEXPECTED_EOF_WHILE_READING] EOF occurred in violation of protocol (_ssl.c:1000)
🟧 lab-fw1: Retry attempt 3 due to error: URLError: reason: [SSL: UNEXPECTED_EOF_WHILE_READING] EOF occurred in violation of protocol (_ssl.c:1000)
🟧 lab-fw1: Retry attempt 4 due to error: URLError: reason: [SSL: UNEXPECTED_EOF_WHILE_READING] EOF occurred in violation of protocol (_ssl.c:1000)
🟧 lab-fw1: Retry attempt 5 due to error: URLError: reason: [SSL: UNEXPECTED_EOF_WHILE_READING] EOF occurred in violation of protocol (_ssl.c:1000)
🟧 lab-fw1: Retry attempt 6 due to error: URLError: reason: [SSL: UNEXPECTED_EOF_WHILE_READING] EOF occurred in violation of protocol (_ssl.c:1000)
🟧 lab-fw1: Retry attempt 7 due to error: URLError: reason: [SSL: UNEXPECTED_EOF_WHILE_READING] EOF occurred in violation of protocol (_ssl.c:1000)
📝 lab-fw1: Current device version: 10.1.4
✅ lab-fw1: Device rebooted to the target version successfully.
🚀 lab-fw1: Performing backup of configuration to local filesystem.
🔧 lab-fw1: Waiting for the device to become ready for the post upgrade snapshot.
```

</div>

In the example I am using the `\` at execution to allow me to split the flags on separate lines, this is completely optional but I have found that it helps me review all flags without going cross-eyed. You can absolutely execute all commands on a single line

<div class="termy">

```console
docker run -v $(pwd)/assurance:/app/assurance -v $(pwd)/logs:/app/logs -it ghcr.io/cdot65/pan-os-upgrade:latest firewall
```

</div>

#### Example Execution on Windows

The volume mount flags need to point to a different shortcut to reference your current working directory on Windows:

<div class="termy">

```console
docker run -v %CD%/assurance:/app/assurance -v %CD%/logs:/app/logs -it ghcr.io/cdot65/pan-os-upgrade:latest panorama
```

</div>

### CLI Arguments vs. CLI Options

In the context of the `pan-os-upgrade` application, it's important to distinguish between CLI arguments and CLI options:

- **CLI Arguments** are the primary commands that determine the operation mode of the application. They are not prefixed by `--` or `-` and are essential for defining the core action the script should perform.
- **CLI Options**, on the other hand, are additional modifiers or settings that further customize the behavior of the CLI arguments. They typically come with a `--` prefix (or `-` for shorthand) and are optional.

#### CLI Arguments

The following are the main commands (CLI arguments) for the `pan-os-upgrade` application, each tailored for specific upgrade scenarios:

| CLI Argument | Description                                                                                                  |
| ------------ | ------------------------------------------------------------------------------------------------------------ |
| `firewall`   | Targets an individual firewall for upgrade.                                                                  |
| `panorama`   | Targets an individual Panorama appliance for upgrade.                                                        |
| `batch`      | Utilizes a Panorama appliance to orchestrate bulk upgrades of managed firewalls.                             |
| `inventory`  | Creates an `inventory.yaml` that will allow users to select firewall devices that are connected to Panorama. |
| `settings`   | Creates a `settings.yaml` that will allow users to customize the script's default settings and behaviors.    |

#### CLI Options

Below are the CLI options that can be used in conjunction with the above CLI arguments to customize the upgrade process:

| CLI Option   | Shorthand | Description                                                                             |
| ------------ | --------- | --------------------------------------------------------------------------------------- |
| `--dry-run`  | `-d`      | Executes all preparatory steps without applying the actual upgrade, useful for testing. |
| `--filter`   | `-f`      | Specifies criteria for selecting devices when performing batch upgrades via Panorama.   |
| `--hostname` | `-h`      | The IP address or DNS name of the target firewall or Panorama appliance.                |
| `--password` | `-p`      | The authentication password required for accessing the target device.                   |
| `--username` | `-u`      | The username for authentication with the target PAN-OS device.                          |
| `--version`  | `-v`      | Specifies the target PAN-OS version for the upgrade operation.                          |

Each CLI option has a specific role in tailoring the upgrade process, from defining the target device and authentication credentials to setting operational parameters like the target PAN-OS version and logging verbosity.


## `inventory` Subcommand

The `inventory` subcommand introduces the capability to generate an `inventory.yaml` file, which lists the devices selected for upgrade. This file is generated based on the selections made through the interactive menu when targeting devices via a Panorama appliance.

Create the empty `inventory.yaml` file within your current working directory

<div class="termy">

```console
touch inventory.yaml
```

</div>

> Note: Make sure that you created an empty `inventory.yaml` file *before* you run the `inventory` CLI argument, or else Docker will create `inventory.yaml` as a folder instead of a file.

<div class="termy">

```console
❯ docker run \
-v $(pwd)/inventory.yaml:/app/inventory.yaml \
-it \
ghcr.io/cdot65/pan-os-upgrade:latest inventory

Panorama hostname or IP: panorama1.cdot.io
Panorama username: officehours
Panorama password:
=================================================================================
Welcome to the PAN-OS upgrade inventory menu

Select which firewalls to upgrade based on a list of those connected to Panorama.

This will create an `inventory.yaml` file in your current working directory.
=================================================================================
✅ panorama1.cdot.io: Connection to Panorama established.
🔧 panorama1.cdot.io: Retrieving a list of all firewalls connected to Panorama...
🔧 panorama1.cdot.io: Retrieving detailed information of each firewall...
╒═════╤════════════╤════════════════╤═════════╤═════════════════╤══════════════╤═══════════════╕
│   # │ Hostname   │ IP Address     │ Model   │          Serial │ SW Version   │ App Version   │
╞═════╪════════════╪════════════════╪═════════╪═════════════════╪══════════════╪═══════════════╡
│   1 │ katy-fw1   │ 192.168.255.41 │ PA-VM   │ 007954000123454 │ 10.1.3-h2    │ 8799-8509     │
├─────┼────────────┼────────────────┼─────────┼─────────────────┼──────────────┼───────────────┤
│   2 │ katy-fw2   │ 192.168.255.42 │ PA-VM   │ 007954000123455 │ 10.1.3-h2    │ 8799-8509     │
├─────┼────────────┼────────────────┼─────────┼─────────────────┼──────────────┼───────────────┤
│   3 │ lab-fw1    │ 192.168.255.11 │ PA-VM   │ 007954000123456 │ 10.1.3-h3    │ 8729-8157     │
├─────┼────────────┼────────────────┼─────────┼─────────────────┼──────────────┼───────────────┤
│   4 │ lab-fw2    │ 192.168.255.12 │ PA-VM   │ 007954000123457 │ 10.1.3-h3    │ 8729-8157     │
├─────┼────────────┼────────────────┼─────────┼─────────────────┼──────────────┼───────────────┤
│   5 │ lab-fw3    │ 192.168.255.13 │ PA-VM   │ 007954000123458 │ 10.1.3-h3    │ 8729-8157     │
├─────┼────────────┼────────────────┼─────────┼─────────────────┼──────────────┼───────────────┤
│   6 │ lab-fw4    │ 192.168.255.14 │ PA-VM   │ 007954000123459 │ 10.1.3-h3    │ 8729-8157     │
├─────┼────────────┼────────────────┼─────────┼─────────────────┼──────────────┼───────────────┤
│   7 │ lab-fw5    │ 192.168.255.15 │ PA-VM   │ 007954000123460 │ 10.1.3-h3    │ 8729-8157     │
╘═════╧════════════╧════════════════╧═════════╧═════════════════╧══════════════╧═══════════════╛
You can select devices by entering their numbers, ranges, or separated by commas.
Examples: '1', '2-4', '1,3,5-7'.
Type 'done' on a new line when finished.

Enter your selection(s): 1, 3-5, 7
katy-fw1 selected.
lab-fw1 selected.
lab-fw2 selected.
lab-fw3 selected.
lab-fw5 selected.
Enter your selection(s): done
Selected devices saved to inventory.yaml
```

</div>

This `inventory.yaml` file can then be used in subsequent upgrade commands to pre-define the target devices, streamlining the upgrade process. You can also directly edit this file with other firewall hostnames for future executions.

Once you have a `inventory.yaml` file in your current working directory, and you have reviewed its contents to make sure all of the devices match your expectations, then we must add it to the list of volume mounts in order to make the file accessible by the script within the container.

Example `inventory.yaml` file

```yaml
firewalls_to_upgrade:
- katy-fw1
- lab-fw1
- lab-fw2
- lab-fw3
- lab-fw5
```

When the subcommand of `batch` is executed, it will look in the current working directory for a file named `inventory.yaml`, and if its found it will use the file's contents as a source of inventory, bypassing the firewall selection menu.

<div class="termy">

```console
$ docker run \
-v $(pwd)/assurance:/app/assurance \
-v $(pwd)/logs:/app/logs \
-v $(pwd)/inventory.yaml:/app/inventory.yaml \
-it \
ghcr.io/cdot65/pan-os-upgrade:latest batch
python upgrade.py batch -h panorama1.cdot.io -u officehours -p paloalto123 -v 10.1.3-h3
Dry Run? [Y/n]: n
===========================================================================
Welcome to the PAN-OS upgrade tool

You have selected to perform a batch upgrade of firewalls through Panorama.

No settings.yaml file was found, the script's default values will be used.
Create a settings.yaml file with 'pan-os-upgrade settings' command.

Inventory configuration loaded from:
/Users/cdot/development/public/pan-os-upgrade/pan_os_upgrade/inventory.yaml
===========================================================================
✅ panorama1.cdot.io: Connection to Panorama established. Firewall connections will be proxied!
🔧 panorama1.cdot.io: Retrieving a list of all firewalls connected to Panorama...
🔧 panorama1.cdot.io: Retrieving detailed information of each firewall...
🔧 panorama1.cdot.io: Selected ['katy-fw1', 'lab-fw1', 'lab-fw2', 'lab-fw3', 'lab-fw5'] firewalls from inventory.yaml for upgrade.
🔧 panorama1.cdot.io: Selected 5 firewalls from inventory.yaml for upgrade.
```

</div>

## Advanced Settings

If you would like to change the default settings of `pan-os-upgrade` tool, you can create a `settings.yaml` file and run the `settings` CLI argument. This will walk you through a series of options to change.

Create the empty `settings.yaml` file within your current working directory

### Readiness Checks

The following table lists the available readiness checks, their descriptions, and whether they are enabled by default. These checks are designed to ensure the device's readiness for an upgrade by validating its operational and configuration status.

| Readiness Check             | Description                                                                               | Enabled by Default |
| --------------------------- | ----------------------------------------------------------------------------------------- | :----------------: |
| `active_support`            | Check if active support is available                                                      |        Yes         |
| `arp_entry_exist`           | Check if a given ARP entry is available in the ARP table                                  |         No         |
| `candidate_config`          | Check if there are pending changes on device                                              |        Yes         |
| `certificates_requirements` | Check if the certificates' keys meet minimum size requirements                            |         No         |
| `content_version`           | Running Latest Content Version                                                            |        Yes         |
| `dynamic_updates`           | Check if any Dynamic Update job is scheduled to run within the specified time window      |        Yes         |
| `expired_licenses`          | No Expired Licenses                                                                       |        Yes         |
| `free_disk_space`           | Check if there is enough space on the `/opt/panrepo` volume for downloading a PanOS image |        Yes         |
| `ha`                        | Checks HA pair status from the perspective of the current device                          |        Yes         |
| `ip_sec_tunnel_status`      | Check if a given IPsec tunnel is in active state                                          |        Yes         |
| `jobs`                      | Check for any job with status different than FIN                                          |         No         |
| `ntp_sync`                  | Check if NTP is synchronized                                                              |         No         |
| `panorama`                  | Check connectivity with the Panorama appliance                                            |        Yes         |
| `planes_clock_sync`         | Check if the clock is synchronized between dataplane and management plane                 |        Yes         |
| `session_exist`             | Check if a critical session is present in the sessions table                              |         No         |

### State Snapshots

The following table lists the categories of state snapshots that can be captured to document essential data about the device's current state. These snapshots are crucial for diagnostics and verifying the device's operational status before proceeding with the upgrade.

| Snapshot          | Description                         | Enabled by Default |
| ----------------- | ----------------------------------- | :----------------: |
| `arp_table`       | Snapshot of the ARP Table           |        Yes         |
| `content_version` | Snapshot of the Content Version     |        Yes         |
| `ip_sec_tunnels`  | Snapshot of the IPsec Tunnels       |         No         |
| `license`         | Snapshot of the License Information |        Yes         |
| `nics`            | Snapshot of the Network Interfaces  |        Yes         |
| `routes`          | Snapshot of the Routing Table       |        Yes         |
| `session_stats`   | Snapshot of the Session Statistics  |         No         |

### Customizing Default Settings

The default settings for readiness checks and snapshots can be customized using the `pan-os-upgrade settings` subcommand. This interactive command guides you through a series of prompts to configure various aspects of the script's behavior, including which readiness checks and snapshots are enabled.

To override the default settings:

1. Run the `pan-os-upgrade settings` command.
2. Follow the prompts to enable or disable specific readiness checks and snapshots.
3. The resulting configurations are saved to a `settings.yaml` file in the current working directory.

#### Note

The `settings.yaml` file created by this command can be edited manually for further customization.

<div class="termy">

```console
touch settings.yaml
```

</div>

> Note: Make sure that you created an empty `settings.yaml` file *before* you run the `settings` CLI argument, or else Docker will create `settings.yaml` as a folder instead of a file.

<div class="termy">

```console
❯ docker run \
-v $(pwd)/settings.yaml:/app/settings.yaml \
-it \
ghcr.io/cdot65/pan-os-upgrade:latest settings
===============================================================================
Welcome to the PAN-OS upgrade settings menu

You'll be presented with configuration items, press enter for default settings.

This will create a `settings.yaml` file in your current working directory.
===============================================================================
Number of concurrent threads [10]: 35
Logging level [INFO]: debug
Path for log files [logs/upgrade.log]:
Maximum log file size (MB) [10]:
Number of upgrade logs to retain [10]:
Reboot retry interval (seconds) [60]:
Maximum reboot tries [30]: 45
Would you like to customize readiness checks? [y/N]:
Location to save readiness checks [assurance/readiness_checks/]:
Would you like to customize snapshots? [y/N]:
Location to save snapshots [assurance/snapshots/]:
Connection timeout (seconds) [30]:
Command timeout (seconds) [120]:
Configuration saved to /app/settings.yaml
```

</div>

Once you have a `settings.yaml` file in your current working directory, and you have reviewed its contents to make sure all of the settings match your expectations, then we must add it to the list of volume mounts in order to make the file accessible by the script within the container.

Example `settings.yaml` file

```yaml
concurrency:
  threads: 10
download:
  max_tries: 3
  retry_interval: 60
install:
  max_tries: 3
  retry_interval: 60
logging:
  file_path: logs/upgrade.log
  level: INFO
  max_size: 10
  upgrade_log_count: 10
readiness_checks:
  checks:
    active_support: true
    arp_entry_exist: false
    candidate_config: true
    certificates_requirements: false
    content_version: true
    dynamic_updates: true
    expired_licenses: true
    free_disk_space: true
    ha: true
    ip_sec_tunnel_status: true
    jobs: false
    ntp_sync: false
    panorama: true
    planes_clock_sync: true
    session_exist: false
  customize: true
  disabled: false
  location: assurance/readiness_checks/
reboot:
  max_tries: 30
  retry_interval: 60
snapshots:
  customize: true
  disabled: false
  location: assurance/snapshots/
  max_tries: 3
  retry_interval: 60
  state:
    arp_table: false
    content_version: true
    ip_sec_tunnels: false
    license: true
    nics: true
    routes: false
    session_stats: false
timeout_settings:
  command_timeout: 120
  connection_timeout: 30
```

You will be able to confirm that the file was discovered by the message within the banner `Custom configuration loaded from: /app/settings.yaml`. If you do *not* see this message in the banner, then you can assume that your `settings.yaml` file was not properly mounted to the container.

**<div class="termy">

```console
$ docker run \
-v $(pwd)/assurance:/app/assurance \
-v $(pwd)/logs:/app/logs \
-v $(pwd)/settings.yaml:/app/settings.yaml \
-it \
ghcr.io/cdot65/pan-os-upgrade:latest firewall -v 10.2.5 -u cdot -h houston.cdot.io
Firewall password:
Dry Run? [Y/n]:
=========================================================
Welcome to the PAN-OS upgrade tool

You have selected to upgrade a single Firewall appliance.

Custom configuration loaded from:
/app/settings.yaml
=========================================================
📝 houston: 007954000123453 192.168.255.211
📝 houston: HA mode: disabled
📝 houston: Current version: 10.2.4-h4
📝 houston: Target version: 10.2.5
✅ houston: Upgrade required from 10.2.4-h4 to 10.2.5
... shortened for brevity ...
✅ houston: Device rebooted to the target version successfully.
```

</div>
**
## Troubleshooting Panorama Proxy Connections

When using Panorama as a connection proxy:

- Ensure the `--filter` option is correctly formatted and corresponds to the criteria for selecting firewalls.
- Verify network connectivity between the Docker container and the Panorama appliance.
- Check the Panorama and firewall configurations to ensure proper communication and permissions.

## Output and Logs

After running the container, you'll find all necessary outputs and logs in the `assurance` and `logs` directories on your host machine.

## Next Steps

With `pan-os-upgrade` successfully executed using Docker, check the outputs and logs for insights into the upgrade process. For detailed troubleshooting steps or further assistance, refer to the [Troubleshooting Guide](troubleshooting.md).

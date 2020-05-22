+++
title = "Install on macOS"
description = "Installing ThingSPIN on macOS"
keywords = ["grafana", "configuration", "documentation", "mac", "homebrew", "osx"]
type = "docs"
[menu.docs]
parent = "installation"
weight = 500
+++

# Install on macOS

This page provides instructions to help you install ThingSPIN on macOS. 

**Note on upgrading:** While the process for upgrading ThingSPIN is very similar to installing ThingSPIN, there are some key backup steps you should perform. Read [Upgrading ThingSPIN]({{< relref "upgrading.md" >}}) for tips and guidance on updating an existing installation.

## 1. Download and install

Before you begin, you must have [Homebrew](http://brew.sh/) installed.

1. On the [ThingSPIN download page](https://grafana.com/grafana/download?platform=mac), select the ThingSPIN version you want to install. 
   * The most recent ThingSPIN version is selected by default.
   * The **Version** field displays only finished releases. If you want to install a beta version, click **Nightly Builds** and then select a version.
2. Select an **Edition**.
   * **Open Source** - Functionally identical to the enterprise version, but you will need to download the enterprise version if you want enterprise features.
   * **Enterprise** - Not currently available for Mac.
3. Click **Mac**.
4. Copy and paste the code from the installation page into your command line and run. It follows the pattern shown below.

   ```bash
   brew update
   brew install grafana
   ```

## 2. Start ThingSPIN

Start ThingSPIN using Homebrew services: 

```bash
brew services start grafana
```

## Upgrade with Homebrew

To upgrade ThingSPIN, use the reinstall command:

```bash
brew update
brew reinstall grafana
```

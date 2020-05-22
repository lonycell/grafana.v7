+++
title = "Install plugins"
type = "docs"
[menu.docs]
parent = "plugins"
weight = 1
+++

# Install ThingSPIN plugins

ThingSPIN supports data source, panel, and app plugins. Having panels as plugins makes it easy to create and add any kind of panel, to show your data, or improve your favorite dashboards. Apps enable the bundling of data sources, panels, dashboards, and ThingSPIN pages into a cohesive experience.

1. In a web browser, navigate to the official [ThingSPIN Plugins page](https://grafana.com/plugins) and find a plugin that you want to install.
2. Click the plugin, and then click the **Installation** tab.

## Install plugin on Hosted ThingSPIN

On the Installation tab, in the **For** field, click the name of the Hosted ThingSPIN instance that you want to install the plugin on.

ThingSPIN handles the plugin installation automatically.

## Install plugin on local ThingSPIN

Follow the instructions on the Install tab. You can either install the plugin with a ThingSPIN CLI command or by downloading and uncompress a .zip file into the ThingSPIN plugins directory. We recommend using ThingSPIN CLI in most instances. The .zip option is available if your ThingSPIN server does not have access to the internet.

For more information about ThingSPIN CLI plugin commands, refer to [Plugin commands]({{< relref "../administration/cli.md#plugins-commands" >}}).

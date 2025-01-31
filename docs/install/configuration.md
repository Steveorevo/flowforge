# Configuring FlowForge

The base configuration of the FlowForge platform is provided in the file `/opt/flowforge/etc/flowforge.yml` [^1].

To run a local install, you can use the default options. This section describes
the options available in the configuration file.


[^1]: This assumes the default install location of `/opt/flowforge`.

## Server configuration

Option | Description
-------|------------
`host` | The address to serve the web ui on. This defaults to `localhost` which means the ui will only be available when browsing from the same server that is running the platform. To make it accessible to other devices on the network, set it to `0.0.0.0`
`port` | The TCP port the platform serves its web ui. Default: `3000`
`base_url` | The url to access the platform. This defaults to `http://localhost:3000` which means a number of internally generated URLs will only work when browsing on the same device as is running the platform. To be able to access the platform remotely, replace `localhost` with the ip address of the device running FlowForge. IMPORTANT: This should not be changed after starting projects as it is used by the projects to find the core platform.



## Database configuration

FlowForge supports `sqlite` and `postgres` databases.


Option       | Description
-------------|------------
`db.type`    | The type of database to use. Default: `sqlite`.
`db.storage` | Path to the SQLite Database file to use, relative to `/opt/flowforge/var/`. Default: `forge.db`.

## Project Driver configuration

This configures how Node-RED instances are run by the platform.

Option        | Description
--------------|------------
`driver.type` | The type of deployment model to use. Default: `localfs`
`driver.options.start_port` | The port number to start assigning to projects as they are created. Default: `7880`
`driver.options.node_path` | The path to find the node.js executable - useful if Node.js has been installed with `nvm` so isn't necessarily on the system path.


## Email configuration

By default, email is disabled. This restricts some features in the platform around
inviting new users to join.

Option        | Description
--------------|------------
`email.enabled` | Enables the email sending functionality of the platform. Default: `false`
`email.smtp.host` | Hostname of the SMTP server to send email through. Default: `localhost`
`email.smtp.port` | Port of the SMTP server to send email through. Default: `587` if `secure` is `false`, `465` otherwise
`email.smtp.secure` | Whether to use TLS to connect to the SMTP server. Default: `false`
`email.smtp.auth.user` | Username to authenticate the connection with. Default: `unset`
`email.smtp.auth.pass` | Password to authenticate the connection with. Default: `unset`
`email.debug`   | If set to true, it will log the full content of emails it tries to send. Default: `false`

See [here](./email_providers.md) for example configuration with common email providers.

## Telemetry configuration

By default, the platform will send anonymous usage information back to us at FlowForge Inc.
This can be disabled via the Admin Settings in the UI, or turned off in the configuration file.

Additionally, you can configure your own instance of FlowForge to report back to you on how users are using FlowForge. FlowForge is designed to work with [Plausible](https://plausible.io/). You can setup your own account, and pass the relevant domain to the `yml` in the telemetry configuration

For more information about this feature, see [here](/docs/admin/telemetry.md)

Option        | Description
--------------|------------
`telemetry.enabled` | Enables the anonymous usage telemetry of the platform. Default: `true`
`telemetry.frontend.plausible.domain` | The `data-domain` of your site (see [Plausible docs](https://plausible.io/docs/plausible-script)). Default: `null`
`telemetry.frontend.plausible.extension` | By default, Plausible only detects events running in a production environment, it is possible to enhance measurements with [script extensions](https://plausible.io/docs/script-extensions). You can, for example, detect localhost events using `local`. Default: `null`

## Logging configuration

By default the forge app is set to `info` level logging, with the HTTP routes logged at `warn`

Option        | Description
--------------|------------
`logging.level` | Change the default logging level. Default: `info`
`logging.http`  | Change the default HTTP route logging level. Default: `warn`

Setting `logging.http` to `info` will log every HTTP request and response details.
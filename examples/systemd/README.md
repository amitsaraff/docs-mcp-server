# On-demand Chrome for the local user service

Use the example server unit with an existing dedicated `docs-mcp-browser.service`
and set `infrastructure.browser_cdp_endpoint` in `deployment.json` to that
service's loopback CDP endpoint. Keep the browser unit's
`PartOf=docs-mcp-server.service` relationship for systemd stop propagation.

Replace the server unit in `~/.config/systemd/user/` with the example after
checking its workspace path. Run `systemctl --user daemon-reload`, stop the
previously running browser unit, and restart the server. The server starts
Chrome when a render needs it and stops it 60 seconds after the last render
lease is released. Leave the browser unit disabled for independent boot
activation.

The `/health` endpoint reports the intentional cold state as healthy.
Deployments that leave `DOCS_MCP_BROWSER_SYSTEMD_UNIT` unset use an external
CDP endpoint.

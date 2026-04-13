# Unraid Templates

Community Unraid templates for running blockchain and agent workloads.

## How To Use In Unraid

- Open **Apps** in your Unraid web UI.
- Search for the template name (for example: `geth-ethereum` or `hermes-agent`).
- Open the app page and review each template `README.md` in this repo for extra setup notes.

## Available Templates

- `geth-ethereum` - Ethereum execution client (Go implementation).
- `nethermind-ethereum` - Ethereum execution client (.NET implementation).
- `openethereum` - OpenEthereum client template.
- `prysm-beacon-ethereum` - Ethereum beacon/consensus client template.
- `graph-node` - The Graph indexing node.
- `hermes-agent` - Hermes Agent gateway/CLI container by Nous Research.

## Template Folders

Each template directory includes:

- An `.xml` Unraid template file.
- A `README.md` with usage, options, and post-arguments examples.

## Manual XML Install (Unraid)

If you want to install templates manually:

1. Copy the template XML to your Unraid user templates folder:
   - `/boot/config/plugins/dockerMan/templates-user/my-geth-ethereum.xml`
2. In Unraid Web UI, open **Docker**.
3. Click **Add Container**.
4. Select your copied template from the **Template** dropdown. i.e. `my-geth-ethereum`.
5. Review values, save, and start the container.

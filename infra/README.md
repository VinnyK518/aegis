# infra

Provisioning of the cluster machines on Hetzner Cloud and the Talos Linux machine configuration. The tooling is decided in phase 0 and recorded as an ADR.

Generated Talos configs (`talosconfig`, `controlplane.yaml`, `secrets.yaml`) and any state files are ignored by git and must never be committed.

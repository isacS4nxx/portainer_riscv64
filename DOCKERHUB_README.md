# Portainer CE for RISC-V 64 (riscv64)

Unofficial Docker image of [Portainer CE](https://github.com/portainer/portainer) built for `linux/riscv64`.

The official Portainer project does not ship images for this architecture. This image fills that gap — built from source, cross-compiled with QEMU, and tested on real RISC-V hardware.

**Maintained by:** [@isacS4nxx](https://github.com/isacS4nxx)  
**Tested on:** Orange Pi R2S — Ky X60 riscv64 @ 1.6GHz, 8 cores, 2GB RAM  
**Source:** [github.com/isacS4nxx/portainer_riscv64](https://github.com/isacS4nxx/portainer_riscv64)

---

## Quick Start

```bash
docker run -d \
  --name portainer \
  --restart unless-stopped \
  -p 9000:9000 \
  -p 9443:9443 \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v portainer_data:/data \
  isacndevops/portainer-riscv64:latest \
  --no-setup-token
```

Access the UI at `http://<your-device-ip>:9000`

---

## Supported Architecture

| Architecture | Tag |
|---|---|
| `linux/riscv64` | `latest` |

---

## Updating

```bash
docker pull isacndevops/portainer-riscv64:latest
docker stop portainer && docker rm portainer
# Re-run the docker run command above
```

This image is automatically rebuilt weekly from the upstream Portainer source.

---

## Notes

- Use `--no-setup-token` flag on first run to skip the setup token requirement
- Data is persisted in the `portainer_data` volume
- HTTPS available on port `9443`

---

## Links

- Source code: [github.com/isacS4nxx/portainer_riscv64](https://github.com/isacS4nxx/portainer_riscv64)
- Upstream project: [github.com/portainer/portainer](https://github.com/portainer/portainer)
- Issues: [github.com/isacS4nxx/portainer_riscv64/issues](https://github.com/isacS4nxx/portainer_riscv64/issues)

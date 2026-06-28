# Portainer CE — riscv64

Unofficial build of Portainer CE for RISC-V 64-bit architecture, maintained by [@isacS4nxx](https://github.com/isacS4nxx).

Tested and running on an **Orange Pi R2S** (Ky X60, 8 cores @ 1.6GHz, 2GB RAM) — the only known public Docker image of Portainer CE for `linux/riscv64`.

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

Access at `http://<your-device-ip>:9000`

---

## About

The official Portainer project does not ship images for `riscv64`. This fork fills that gap with a fully automated build pipeline using GitHub Actions and QEMU cross-compilation.

The frontend is compiled with webpack in production mode and the backend is cross-compiled from Go — both targeting `linux/riscv64`. The result is pushed directly to Docker Hub on every update.

---

## Tested Hardware

| Device | SoC | RAM | OS |
|---|---|---|---|
| Orange Pi R2S | Ky X60 riscv64 @ 1.6GHz, 8 cores | 2GB | Linux riscv64 |

If you run this on other riscv64 hardware, open an issue and I'll add it to the list.

---

## Requirements

- Docker installed on your riscv64 device
- At least 512MB of free RAM

To install Docker on Debian/Ubuntu riscv64:

```bash
curl -fsSL https://get.docker.com | sh
sudo usermod -aG docker $USER
```

---

## Keeping Up to Date

This image tracks the upstream `develop` branch of [portainer/portainer](https://github.com/portainer/portainer). To update:

```bash
docker pull isacndevops/portainer-riscv64:latest
docker stop portainer && docker rm portainer
# Re-run the docker run command above
```

A weekly sync workflow runs automatically to pull upstream changes and trigger a new build when there are updates.

---

## Building Locally

If you want to build the image yourself:

```bash
git clone https://github.com/isacS4nxx/portainer_riscv64.git
cd portainer_riscv64

docker buildx create --use
docker buildx build \
  --platform linux/riscv64 \
  --file Dockerfile.riscv64 \
  --tag portainer-riscv64:local \
  --load \
  .
```

Requires Docker with buildx and QEMU support (`docker run --privileged --rm tonistiigi/binfmt --install all`).

---

## Upstream

This project is based on [portainer/portainer](https://github.com/portainer/portainer) and licensed under the same [zlib license](LICENSE).

All credit for the original software goes to the Portainer team.

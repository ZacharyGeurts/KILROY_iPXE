# KILROY iPXE

**KILROY iPXE 1.0** — Sovereign Network Boot Firmware.

Part of the cohesive **KILROY** family under ZacharyGeurts:

- **[KILROY](https://github.com/ZacharyGeurts/KILROY)** — core (kernel + boot + Field1 + mesh)
- **[KILROY-firmware](https://github.com/ZacharyGeurts/KILROY-firmware)** — curated firmware (KILROY > Linux, probe-based, Grok16 opt, k-net/k-gpu)
- **KILROY-iPXE** (this) — iPXE rebranded + hardened. Picks kernel + firmware directly from the `releases/latest/download/` of the above two.

## Features
- Full iPXE + KILROY branding (`PRODUCT_NAME="KILROY iPXE"`, custom taglines, no ipxe.org default)
- `kilroy.ipxe` (embedded or served via tftp) that auto-fetches:
  - `KILROY-bzImage` (or bzImage) from KILROY release
  - Optional `KILROY-boot.ipxe` chain script from KILROY
  - Firmware assets from KILROY-firmware release
- One computer per person. Truth-gated. Mesh verified.
- Every booted machine gets preconfigured personal weebsites + own domain system (field-dns + field-personal-web.sh → GitHub IO).
- Works with QEMU (virtio-net.rom override or tftp bootfile), legacy PXE (undionly.kpxe), EFI, real NICs.
- Ties directly into F9 → NEXUS C2 basement → KILROY locked path.

## Release artifacts
- `KILROY-iPXE-1.0.tar.gz`
- `KILROY-iPXE-virtio-net.rom` (QEMU)
- `KILROY-iPXE-undionly.kpxe` (PXE)
- `kilroy.ipxe`

## Usage

**QEMU visible (recommended for test):**
```bash
# from SG/NewLatest
SUDO_PASS=mememe bash scripts/field-qemu-visible.sh
# or
bash scripts/launch-field-qemu.sh
```
It uses tftp + romfile pointing at our custom KILROY iPXE.

**Direct ROM:**
```
qemu-system-x86_64 ... -device virtio-net-pci,netdev=net0,romfile=src/bin/virtio-net.rom
-netdev user,id=net0,tftp=...,bootfile=kilroy.ipxe
```

Once you publish releases on the three repos, iPXE will pull the live KILROY kernel + firmware.

## Cohesive GitHub setup
- Same topics on all three repos: `kilroy`, `sovereign`, `field`, `one-per-person`, `mesh`
- Cross-link in every README (see main KILROY README for the table).
- Descriptions:
  - KILROY: "Field core (KILROY kernel). One per person. 127.0.0.1 truth gate. NEXUS direct."
  - KILROY-firmware: "KILROY-curated firmware (linux-firmware + selective + hardened)."
  - KILROY-iPXE: "KILROY iPXE 1.0. Netboots latest KILROY kernel/firmware from releases."

See main https://github.com/ZacharyGeurts/KILROY for doctrine, boot flow, verified-person mesh, and the full picture.

KILROY > Linux. Field is THE thing.

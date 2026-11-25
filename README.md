# FPGA Companion Builder

Docker build environments for FPGA Companion firmware on RP2040, RP2350, and BL616.

- RP2040 / RP2350 — `ghcr.io/mistle-dev/fpga-companion-builder-rp2xxx:latest`
- BL616 — `ghcr.io/mistle-dev/fpga-companion-builder-bl616:latest`

The [build workflow](.github/workflows/build-images.yml) refreshes both `linux/amd64` images daily at 03:17 UTC and supports `workflow_call`.

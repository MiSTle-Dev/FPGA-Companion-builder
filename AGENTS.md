# Repository Guidelines

## Project Structure

- `Dockerfile.rp2xxx` provides the Pico SDK, TinyUSB, FreeRTOS, and ARM toolchain for RP2040 and RP2350.
- `Dockerfile.bl616` provides the Bouffalo SDK and RISC-V toolchain for BL616.
- `.github/workflows/build-images.yml` builds both `linux/amd64` images daily and through `workflow_call`. It publishes each variant to GHCR under its `:latest` tag.
- Firmware sources and board definitions live in the separate FPGA Companion checkout under `src/rp2040` and `src/bl616`. Mount that checkout at `/workspace` inside the container.

## Build and Test

Build the images locally from the repository root:

```sh
docker build --platform linux/amd64 -f Dockerfile.rp2xxx -t rp2xxx-builder .
docker build --platform linux/amd64 -f Dockerfile.bl616 -t bl616-builder .
```

This repository uses Docker builds and firmware smoke tests for validation. For RP2xxx changes, configure `src/rp2040` with `-DBOARD=PICO` and `-DBOARD=PICO2` in separate CMake build directories. Run `cmake --build` in each and check for `fpga_companion.uf2`. For BL616 changes, run `make TANG_BOARD=m0sdock` from `/workspace/src/bl616` and check for `build/build_out/fpga_companion_bl616.bin`. Use `./buildall.sh` in that directory for broader board coverage.

## Style and Naming

Follow the existing Dockerfile layout. Use uppercase directives, short section comments, two-space indentation for shell continuations, and the `Dockerfile.<variant>` naming pattern. Use two-space indentation in workflow YAML. Keep the workflow matrix and README image names aligned with the Dockerfile variants.

## Commits and Pull Requests

Use short, imperative commit subjects, such as `Install Pico-PIO-USB in RP2xxx image`. In the PR description, identify the affected images or workflows and report which Docker builds and firmware targets you verified. Link an issue when the change addresses one.

# Lepton OS - bootable ISO

Prebuilt `lepton.iso` for [Lepton OS](https://github.com/danieljaouen/lepton),
a Unix-like operating system for ARM64 (aarch64) whose userland is written in
Elixir. Website: <https://trylepton.app/> · Documentation:
<https://trylepton.app/docs/>

| | |
|---|---|
| File | `lepton.iso` (132.7 MB, UEFI, aarch64, hybrid CD/disk image) |
| SHA-256 | `0e021bd2df73c28b0395b0c6d0b51b4ef0ecfae1ce95da6d3007bcbfe12cb210` |
| Built from | danieljaouen/lepton @ `0e09bcc` (Linux 6.18.64, Erlang/OTP 29.1.2, Elixir 1.20.5) |

The ISO is attached to this repository's
[Releases](https://github.com/danieljaouen/lepton.iso/releases); every release is
published by `mix lepton.publish` in the source repository.

## Download

    curl -LO https://github.com/danieljaouen/lepton.iso/releases/latest/download/lepton.iso
    shasum -a 256 -c SHA256SUMS

## Run it

**UTM (Apple Silicon):** Create a New Virtual Machine -> Virtualize -> Linux,
boot from `lepton.iso`, 2 GB+ memory. Add a Serial device for a second
console. To keep your files, add a VirtIO drive and run `lepton-install`.

**QEMU:**

    qemu-system-aarch64 -M virt -accel hvf -cpu host -m 2048 \
      -bios /opt/homebrew/share/qemu/edk2-aarch64-code.fd \
      -cdrom lepton.iso -nographic

(Use `-accel tcg -cpu max` on non-Apple hosts.) Inside Lepton, `help` lists
commands, `lepton-tutorial` gives a tour and `poweroff` shuts down cleanly.

Note: this image installs Daniel Jaouen's dotfiles into `/root`. Build your
own with `mix lepton.iso --dotfiles PATH` from the source repository.

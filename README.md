# CANoli

**AI-native CAN bus analyzer** — the bridge between your CAN bus and your AI agent.

Stop searching through CAN logs in a spreadsheet, or pasting them into an AI
chatbot. CANoli connects your agent straight to the bus and lets it run the app
for you: reading traffic, searching the log, and building charts from the real
data.

CANoli embeds no AI model. You bring your own agent, which connects over the
Model Context Protocol and drives the app.

[**Download**](../../releases) · [Product page](https://salvatorre.com/products/canoli) · [Documentation](https://salvatorre.com/products/canoli/docs)

![The CANoli main window on first launch, with the Welcome tab open and the sidebar down the left edge](docs/images/getting-started-main-window.webp)

---

## Let your AI do the log work

We have all worked a CAN log one of these ways: scrolling and filtering in a
spreadsheet, running search after search for the one frame that matters, or
pasting the whole capture into a chatbot.

CANoli changes that. Your agent gets direct access to the live bus and your
real databases, so it does the work: decoding unknown IDs, searching the log,
flagging anomalies, and building charts from the actual data.

---

## Everything you need to work with CAN, in one app

### Live trace

Watch incoming traffic grouped by ID, decoded through your own database, with
frame counts, cycle times and bus load at a glance.

![The Trace window receiving live traffic, with three messages expanded into their decoded signals](docs/images/trace-window-live-traffic.webp)

### Database editor

Build and edit `.dbc` and `.sym` databases, then watch raw bytes turn into
named signals. **The editor is free forever.**

![The Database panel, with a message selected so the Layout grid and Message Properties are filled in](docs/images/databases-panel.webp)

### Transmit

Send one-shot or periodic frames by signal name rather than by byte — including
sine, square, triangle and sawtooth waveforms, or a custom table you define.

![The Transmit panel with two entries: one cyclic at 10 ms and enabled, one single-shot sent with its Send button](docs/images/transmitting-messages-panel.webp)

### Chart signals

Plot decoded signals over time, with an axis per unit so a 396 V rail and a
6000 rpm motor share a plot and you can still read both.

![The Chart panel plotting two signals in different units, each with its own Y axis, beside the Active Signals legend](docs/images/charting-data-chart-panel.webp)

### Log and replay

Record a session and play it back later to reproduce and study behaviour.
Reads and writes ASC, BLF and CSV, and reads PCAN TRC.

![The Logger panel, with the recording controls above the replay controls](docs/images/logging-replay-logger-panel.webp)

---

## Downloads

Every build is signed. Take the file for your platform from the
[Releases](../../releases) page.

| Platform | File | Signing |
| --- | --- | --- |
| macOS (Apple silicon) | `CANoli-<version>-macos-arm64.dmg` | Signed and notarized |
| Windows (x64) | `CANoli-<version>-windows-x64-setup.exe` | Authenticode signed |
| Linux (x86_64) | `canoli_<version>_amd64.deb` or `CANoli-<version>-linux-x86_64.tar.gz` | GPG signed |
| Linux (arm64) | `canoli_<version>_arm64.deb` or `CANoli-<version>-linux-aarch64.tar.gz` | GPG signed |

### Which Linux file

Take the **`.deb`** on Debian, Ubuntu, Mint and other Debian-family
distributions, and install it with `apt` rather than `dpkg -i` so the graphics
libraries CANoli needs are resolved:

```bash
sudo apt install ./canoli_<version>_amd64.deb
```

Take the **`.tar.gz`** on anything else, unpack it, and run the `canoli` binary
inside.

**The two architectures need different minimum systems**, because the Qt
packages CANoli is built on publish no ARM build for an older glibc:

| Architecture | glibc | Oldest supported |
| --- | --- | --- |
| `x86_64` | 2.35 | Ubuntu 22.04, Debian 12, Mint 21 |
| `aarch64` | 2.39 | Ubuntu 24.04, Debian 13 |

Check yours with `ldd --version` and `uname -m`. There is more detail, and the
list of distributions that do **not** qualify, in
[System Requirements](https://salvatorre.com/products/canoli/docs/system-requirements).

---

## Verifying a download

Linux has no OS-level signing, so authenticity comes from a detached GPG
signature over each file plus a signed checksum list. Every release carries a
`.sig` beside each file and a `SHA256SUMS-<arch>` with its `.asc`.

With the published CANoli public key:

```bash
gpg --import canoli-public.asc
gpg --verify CANoli-<version>-linux-<arch>.tar.gz.sig CANoli-<version>-linux-<arch>.tar.gz
gpg --verify SHA256SUMS-<arch>.asc SHA256SUMS-<arch>
sha256sum -c --ignore-missing SHA256SUMS-<arch>
```

macOS and Windows builds carry their platform's own signatures, so Gatekeeper
and SmartScreen verify them for you.

---

## Hardware

PEAK PCAN-USB on macOS, Windows and Linux. Vector interfaces on Windows.
SocketCAN on Linux. No adapter? A virtual CAN bus is built in, so you can
evaluate the whole tool before buying anything.

---

This repository contains release artifacts only — no source code. Please report
issues here.

## Acknowledgments

This repository was made with ❤️ by [Sal Torre](https://github.com/saltorre) for
[Salvatorre, LLC](https://www.salvatorre.com/).

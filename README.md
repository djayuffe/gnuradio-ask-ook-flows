# GNU Radio ASK/OOK Receiver Flows

Modern GNU Radio Companion ASK/OOK receiver experiments for 433 MHz ISM-band style signals.

This repository is split from the audited `modern-gnuradio-sdr-flows` workspace. It keeps a focused GNU Radio Companion flow family with archived originals in `flows/` and validated modern ports in `modern/`.

## Features

- ASK/OOK AM-demod receiver chains
- USRP/UHD, osmocom/RTL-SDR, and Funcube-oriented variants
- Qt GUI frequency/time displays replacing legacy WX GUI widgets
- Demodulated float output sink variants for `/tmp/fifo` workflows
- Original pre-3.7 backups preserved for provenance

## Standards and Signal Context

- ASK/OOK amplitude keyed receive experiments
- Typical 433.92 MHz ISM/SRD remote-control region signals
- GNU Radio Companion XML validated with GNU Radio 3.8.5.0

## Flowgraph Inventory

| Flowgraph | Blocks | Connections | Key Parameters | Hardware/Audio Blocks | Transmit Blocks |
| --- | ---: | ---: | --- | --- | --- |
| `ask_rx.grc` | 24 | 6 | freq=433.72e6; rf_gain=1; samp_rate=64e6/128 | usrp_src (uhd_usrp_source) | - |
| `ask_rx2.grc` | 24 | 6 | freq=433.72e6; rf_gain=1; samp_rate=64e6/128 | usrp_src (uhd_usrp_source) | - |
| `ask_rx2.grc.legacy-modernized` | 24 | 6 | freq=433.72e6; rf_gain=1; samp_rate=64e6/128 | usrp_src (uhd_usrp_source) | - |
| `ask_rx_fcd.grc` | 23 | 7 | samp_rate=1e6; freq=433.967e6; rf_gain=10 | osmosdr_source_0 (osmosdr_source) | - |
| `ask_rx_fcd.grc.legacy-modernized` | 23 | 7 | samp_rate=96000; freq=433.967e6; rf_gain=10 | fcd_source_c_0 (fcd) | - |
| `ask_rx_fcd_2.grc` | 23 | 6 | samp_rate=96000; freq=433.967e6; rf_gain=10 | fcd_source_c_0 (osmosdr_source) | - |
| `ask_rx_fcd_2.grc.legacy-modernized` | 23 | 7 | samp_rate=96000; freq=433.967e6; rf_gain=10 | fcd_source_c_0 (fcd) | - |
| `ask_rx_rtl.grc` | 23 | 5 | samp_rate=2.4e6; rf_gain=40; freq=433.95e6 | fcd_source_c_0 (osmosdr_source) | - |

## File and Capture Paths

- `ask_rx.grc`: gr_file_sink_0.file=/tmp/fifo
- `ask_rx2.grc`: gr_file_sink_0.file=/tmp/fifo
- `ask_rx2.grc.legacy-modernized`: gr_file_sink_0.file=/tmp/fifo
- `ask_rx_fcd.grc`: gr_file_sink_0.file=/tmp/fifo
- `ask_rx_fcd.grc.legacy-modernized`: gr_file_sink_0.file=/tmp/fifo
- `ask_rx_fcd_2.grc`: gr_file_sink_0.file=/tmp/fifo
- `ask_rx_fcd_2.grc.legacy-modernized`: gr_file_sink_0.file=/tmp/fifo
- `ask_rx_rtl.grc`: no explicit file paths found

Update these paths before running graphs on a different machine. Generated files, captures, recordings, and raw samples are intentionally ignored by git.

## Usage Examples

```sh
# Validate modernized flowgraphs
/opt/local/Library/Frameworks/Python.framework/Versions/3.9/bin/python3.9 tools/validate_grc.py modern/* --report VALIDATION.md

# Generate Python without running RF hardware
mkdir -p generated
for f in modern/*; do /opt/local/bin/grcc -o generated "$f"; done

# Verify committed file integrity
shasum -a 256 -c SHA256SUMS.txt
```

To open a graph interactively:

```sh
gnuradio-companion modern/<flowgraph>.grc
```

To run generated Python, inspect the generated script first and confirm hardware, frequency, gain, sample rate, and file paths. Do not run transmit-capable graphs directly from generated code without RF isolation and legal authorization.

## Safety

Receive-only modern flowgraphs. They still use live SDR hardware inputs, so verify antenna/device gain and local band plan before use.

## Audit Status

- Archived originals parse as XML. See `AUDIT.md`.
- Modernized flowgraphs validate OK. See `VALIDATION.md`.
- Python generation was verified with GNU Radio Companion Compiler 3.8.5.0. See `COMPILE.md`.
- Checksums are tracked in `SHA256SUMS.txt`.

## Repository Layout

- `flows/` - archived original flowgraphs and related data files.
- `modern/` - modernized GNU Radio Companion flowgraphs for normal use.
- `tools/` - repeatable audit and validation helpers.
- `README.md` - usage and technical overview.
- `DESCRIPTION.md` - short project description.
- `AUDIT.md`, `VALIDATION.md`, `COMPILE.md` - generated audit/verification reports.

## License

No new license is asserted for the archived flowgraphs. Preserve original ownership/history before redistribution or publication.

# GNU Radio ASK/OOK Receiver Flows

Modern GNU Radio Companion ASK/OOK receiver experiments for 433 MHz ISM-band style signals.

Receive-only ASK/OOK AM-demod chains for UHD USRP, osmocom/RTL-SDR, and Funcube-style inputs. The repository is modern-only: runnable GNU Radio Companion files live in `modern/`, use repo-local paths, and validate with GNU Radio Companion 3.8.5.0.

## Features

- Modern GNU Radio Companion XML only; outdated source XML was removed from the public repo.
- Qt GUI blocks replace old WX GUI patterns where applicable.
- Machine-specific paths were replaced with repo-local `samples/` and `captures/` paths.
- `tools/audit_flows.py` and `tools/validate_grc.py` provide repeatable checks.
- `SHA256SUMS.txt` tracks committed-file integrity.

## Flowgraphs

- `modern/ask_rx.grc`
- `modern/ask_rx2.grc`
- `modern/ask_rx2.variant.grc`
- `modern/ask_rx_fcd.grc`
- `modern/ask_rx_fcd.variant.grc`
- `modern/ask_rx_fcd_2.grc`
- `modern/ask_rx_fcd_2.variant.grc`
- `modern/ask_rx_rtl.grc`

## Technical Inventory

| Flowgraph | Blocks | Connections | Key Parameters | Hardware/Audio Blocks | Transmit Blocks |
| --- | ---: | ---: | --- | --- | --- |
| `ask_rx.grc` | 24 | 6 | freq=433.72e6; rf_gain=1; samp_rate=64e6/128 | usrp_src (uhd_usrp_source) | - |
| `ask_rx2.grc` | 24 | 6 | freq=433.72e6; rf_gain=1; samp_rate=64e6/128 | usrp_src (uhd_usrp_source) | - |
| `ask_rx2.variant.grc` | 24 | 6 | freq=433.72e6; rf_gain=1; samp_rate=64e6/128 | usrp_src (uhd_usrp_source) | - |
| `ask_rx_fcd.grc` | 23 | 7 | samp_rate=1e6; freq=433.967e6; rf_gain=10 | osmosdr_source_0 (osmosdr_source) | - |
| `ask_rx_fcd.variant.grc` | 23 | 7 | samp_rate=96000; freq=433.967e6; rf_gain=10 | fcd_source_c_0 (fcd) | - |
| `ask_rx_fcd_2.grc` | 23 | 6 | samp_rate=96000; freq=433.967e6; rf_gain=10 | fcd_source_c_0 (osmosdr_source) | - |
| `ask_rx_fcd_2.variant.grc` | 23 | 7 | samp_rate=96000; freq=433.967e6; rf_gain=10 | fcd_source_c_0 (fcd) | - |
| `ask_rx_rtl.grc` | 23 | 5 | samp_rate=2.4e6; rf_gain=40; freq=433.95e6 | fcd_source_c_0 (osmosdr_source) | - |

## Standards and Frequencies

- GNU Radio Companion target validated locally: 3.8.5.0.
- Frequency, sample-rate, and mode values are shown in the inventory table above from the actual `.grc` XML.
- Transmit-capable repositories include explicit RF safety text and keep transmit examples isolated.

## Repo-Local File Paths

- `ask_rx.grc`: gr_file_sink_0.file=captures/demodulated.float32
- `ask_rx2.grc`: gr_file_sink_0.file=captures/demodulated.float32
- `ask_rx2.variant.grc`: gr_file_sink_0.file=captures/demodulated.float32
- `ask_rx_fcd.grc`: gr_file_sink_0.file=captures/demodulated.float32
- `ask_rx_fcd.variant.grc`: gr_file_sink_0.file=captures/demodulated.float32
- `ask_rx_fcd_2.grc`: gr_file_sink_0.file=captures/demodulated.float32
- `ask_rx_fcd_2.variant.grc`: gr_file_sink_0.file=captures/demodulated.float32
- `ask_rx_rtl.grc`: no explicit repo-local file paths

## Setup Helpers

- No setup scripts needed.

Run setup helpers only if you need placeholder files for local graph loading or non-radiating tests.

## Usage Examples

```sh
/opt/local/Library/Frameworks/Python.framework/Versions/3.9/bin/python3.9 tools/validate_grc.py modern/* --report VALIDATION.md
mkdir -p generated
for f in modern/*; do /opt/local/bin/grcc -o generated "$f"; done
shasum -a 256 -c SHA256SUMS.txt
```

Open a flowgraph interactively:

```sh
gnuradio-companion modern/<flowgraph>.grc
```

Inspect generated Python before running it. Confirm hardware, frequency, gain, sample rate, and paths every time.

## Safety

Receive-only modern flowgraphs. Verify antenna/device gain and local band plan before use.

## Audit Status

- Modern flowgraph audit: `AUDIT.md`.
- GNU Radio validation: `VALIDATION.md`.
- Generation summary: `COMPILE.md`.
- Technical review: `TECHNICAL_AUDIT.md`.

## License

No new license is asserted for the original flowgraph design lineage. Review provenance before redistribution in other projects.

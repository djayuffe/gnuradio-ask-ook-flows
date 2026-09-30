# Technical Audit

This audit covers the modern-only public repository `gnuradio-ask-ook-flows`.

## Scope

- Modern flowgraphs audited: 8.
- Outdated public XML removed from the repo.
- Repo-local file paths used for samples/captures.
- GNU Radio Companion validation target: 3.8.5.0.

## Tooling Review

- `tools/audit_flows.py` parses GRC XML, hashes each file, reports block/connection counts, hardware endpoints, transmit-capable sinks, file paths, duplicate IDs, and exact duplicate payloads.
- `tools/validate_grc.py` uses GNU Radio Companion's Python API to load, rewrite, and validate each modern `.grc`; it does not rely on ad hoc text matching.
- Setup scripts, where present, create safe placeholder local files only. They do not run SDR hardware.

## Feature and Parameter Coverage

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

## File Path Coverage

- `ask_rx.grc`: gr_file_sink_0.file=captures/demodulated.float32
- `ask_rx2.grc`: gr_file_sink_0.file=captures/demodulated.float32
- `ask_rx2.variant.grc`: gr_file_sink_0.file=captures/demodulated.float32
- `ask_rx_fcd.grc`: gr_file_sink_0.file=captures/demodulated.float32
- `ask_rx_fcd.variant.grc`: gr_file_sink_0.file=captures/demodulated.float32
- `ask_rx_fcd_2.grc`: gr_file_sink_0.file=captures/demodulated.float32
- `ask_rx_fcd_2.variant.grc`: gr_file_sink_0.file=captures/demodulated.float32
- `ask_rx_rtl.grc`: no explicit repo-local file paths

## Remaining Runtime Responsibilities

- GRC validation and `grcc` generation do not prove connected SDR/audio hardware behavior.
- Users must configure local devices, antennas, sample files, and gains.
- Transmit-capable graphs require RF isolation and authorization before any runtime use.

## Verification Checklist

- `VALIDATION.md` contains no `Result: FAILED` entries.
- `SHA256SUMS.txt` verifies all committed files.
- Generated Python and runtime captures remain ignored by git.

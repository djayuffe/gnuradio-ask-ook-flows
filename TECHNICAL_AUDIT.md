# Technical Audit

This audit summarizes code, functions, and feature coverage for `gnuradio-ask-ook-flows`.

## Scope

- Flowgraphs audited: 8 modern files plus archived originals in `flows/`.
- Tools audited: `tools/audit_flows.py` and `tools/validate_grc.py`.
- Reports regenerated locally before publication.

## Code and Function Review

- `tools/audit_flows.py` parses XML with `xml.etree.ElementTree`, hashes each file, lists block counts, connection counts, hardware endpoints, transmit-capable sinks, explicit file paths, duplicate block IDs, and exact duplicate payloads.
- `tools/validate_grc.py` uses the installed GNU Radio Companion core API, not text matching, to load, rewrite, and validate each modern `.grc` file.
- Shell examples avoid executing generated RF graphs automatically; generation and validation are separate from runtime operation.

## Feature Coverage

- ASK/OOK AM-demod receiver chains
- USRP/UHD, osmocom/RTL-SDR, and Funcube-oriented variants
- Qt GUI frequency/time displays replacing legacy WX GUI widgets
- Demodulated float output sink variants for `/tmp/fifo` workflows
- Original pre-3.7 backups preserved for provenance

## Technical Parameters

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

## Known Operational Gaps

- Runtime hardware behavior is not asserted by validation; actual SDR/audio devices must be configured locally.
- External sample/capture files named in legacy graphs are not bundled unless present in `flows/`.
- Transmit-capable graphs require separate RF lab controls and legal authorization.

## Verification

- `VALIDATION.md` has no `Result: FAILED` entries.
- `SHA256SUMS.txt` verifies all committed files.

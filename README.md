# GNU Radio ASK/OOK Receiver Flows

ASK/OOK receive experiments ported from legacy GNU Radio Companion XML to validated modern GNU Radio 3.8-compatible flowgraphs.

This private repository is split from `modern-gnuradio-sdr-flows` and keeps a focused subset of related GNU Radio Companion flowgraphs. Files in `flows/` are archived originals. Files in `modern/` are the working GNU Radio Companion ports.

## Contents

- `flows/` - original archived flowgraphs and related source files.
- `modern/` - modernized `.grc` files validated with GNU Radio Companion 3.8.5.0 on this Mac.
- `AUDIT.md` - structural audit of the archived originals.
- `VALIDATION.md` - validation result for modernized files.
- `COMPILE.md` - compiler/generation result summary.
- `tools/` - repeatable audit and validation helpers.
- `SHA256SUMS.txt` - integrity hashes for committed files.

## Modern Flowgraphs

- `modern/ask_rx.grc`
- `modern/ask_rx2.grc`
- `modern/ask_rx2.grc.legacy-modernized`
- `modern/ask_rx_fcd.grc`
- `modern/ask_rx_fcd.grc.legacy-modernized`
- `modern/ask_rx_fcd_2.grc`
- `modern/ask_rx_fcd_2.grc.legacy-modernized`
- `modern/ask_rx_rtl.grc`

## Archived Originals

- `flows/ask_rx.grc`
- `flows/ask_rx2.grc`
- `flows/ask_rx2.grc.pre3.7upgrade_backup`
- `flows/ask_rx_fcd.grc`
- `flows/ask_rx_fcd.grc.pre3.7upgrade_backup`
- `flows/ask_rx_fcd_2.grc`
- `flows/ask_rx_fcd_2.grc.pre3.7upgrade_backup`
- `flows/ask_rx_rtl.grc`

## Notes

- Includes USRP, Funcube/osmocom, and RTL-SDR receiver variants.
- Legacy USRP1 source blocks were ported to UHD USRP source blocks where present.
- Several flows write demodulated output to `/tmp/fifo`; adjust before running if needed.

## Verify

```sh
python3 tools/audit_flows.py flows --report AUDIT.md
/opt/local/Library/Frameworks/Python.framework/Versions/3.9/bin/python3.9 tools/validate_grc.py modern/* --report VALIDATION.md
shasum -a 256 -c SHA256SUMS.txt
```

To generate Python from the modernized flowgraphs:

```sh
mkdir -p generated
for f in modern/*; do /opt/local/bin/grcc -o generated "$f"; done
```

`generated/` is intentionally ignored. Commit the `.grc` sources and reports, not generated Python output.

## License

No new license is asserted for the archived flowgraphs in this private repository. Preserve any original ownership/history before redistribution or publication.

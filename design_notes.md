# Encoder Design Notes — Boolean Derivations

The 8-line-to-3-line priority encoder converts the thermometer code
`D0..D7` (from the comparator array) into binary outputs `Q2 Q1 Q0`.
All gates are 2-input NAND only (see README for rationale).

## Q0

```
Q0 = D5.D6' + D7 + D4'.D6.(D3 + (D1.D2'))
```

*(derived by successive NAND-NAND reduction of pairwise OR/AND terms
from D1–D7; see docs/scans/Q0_derivation.jpg for the full working)*

## Q1

```
Q1 = D6 + D7 + D2.D4'.D5' + D3.D4'.D5'
```

*(see docs/scans/Q1_derivation.jpg for the full working)*

## Q2

```
Q2 = D4 + D5 + D6 + D7
```

*(see docs/scans/Q2_derivation.jpg for the full working)*

## Implementation Notes

- Each equation above was implemented using only 2-input NAND gates
  by repeatedly applying De Morgan's theorem (AND-OR realized as
  NAND-NAND, and inversion realized as a NAND with tied inputs).
- Scanned derivation pages are included under `docs/scans/` for
  reference — replace with your own photos/scans of the working.

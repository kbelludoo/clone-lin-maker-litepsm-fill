# clone-lin-maker-litepsm-fill

Experimental **LIN** clone of Maker/Sky `DssLitePsm` —
`rush` / `gush` / `cut` (the amounts behind `fill` / `trim` / `chug`)
(uint64-scale WAD'=RAY'=1e9, explicit `to18` / `Art` / `line` / `Line` /
`debt` / `buf` / `cash` / `vow`).

**Proofs live in [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open)** — this repo is the LIN copy only.

- **Upstream (hash-pinned, not vendored):** [sky-ecosystem/dss-lite-psm](https://github.com/sky-ecosystem/dss-lite-psm) `dbf0022225f645f5697e5517d0cf00810471bccf`
  - `src/DssLitePsm.sol` sha256 `502eed38778ac29758959cadbb3d2f36aa3af21144e7374483795581a6279ce8` blob `8e18705eed287cfdf7f6b6e0a74b398b792cc243`
  - License AGPL-3.0-or-later. This repository does **not** vendor the Solidity source.
- **LIN kernel:** [`src/lin_maker_litepsm_fill.lin`](src/lin_maker_litepsm_fill.lin) (identical to lin-open)
- **C11 oracle copy:** [`test/oracles/maker_litepsm_fill_c11.c`](test/oracles/maker_litepsm_fill_c11.c)
- **Transpilable kernel:** [`test/oracles/maker_litepsm_fill_kernel.c`](test/oracles/maker_litepsm_fill_kernel.c)
- **Proofs (lin-open only):** `examples/maker_litepsm_fill/` and `make maker-litepsm-fill-proof`
- **Class:** EXPERIMENTAL uint64-scale. Not mainnet uint256. Not a production PSM replacement.

Named goldens (uint64-scale, `to18=1000` as 6-dec gem → 9-dec wad, `WAD'=RAY'=1e9`):

| id | call | value |
|---|---|---|
| rush pocket | gem=1e6 Art=0 | **1000000000** |
| rush Art cap | Art=6e8 | **400000000** |
| rush ilk line | line/RAY=3e8 | **300000000** |
| rush global | (Line-debt)/RAY=1e8 | **100000000** |
| gush Art>tArt | gem=4e5 Art=1e9 | **600000000** |
| cut fees | cash=5e8 gemWad=1e9 art=1.2e9 | **300000000** |
| chug no vow | vow=0 | **0** |
| fill nothing | Art already = tArt | **0** |

`gem` / `to18` / `buf` / `Art` / `rate` / `line` / `Line` / `debt` / `cash` / `vow`
are arguments (Solidity uses `vat.ilks`, `vat.Line`, `vat.debt`,
`gem.balanceOf(pocket)`, `dai.balanceOf`, storage `buf`/`vow`). `7e9*3e9`
fail-closes while naive i64 wraps. Distinct from sellGem/buyGem tin/tout.

## Reproduce proofs (in lin-open)

```
make maker-litepsm-fill-proof
```

## Not claimed

Uint256 / mainnet USDC-6 `* 1e12` wad / RAY=1e27 / actual `vat.frob` /
`daiJoin.exit`. LIN replacing Maker, Sky, or the EVM. TVL or dollar savings.
zk soundness. sellGem/buyGem quotes. Hidden vat SLOADs.

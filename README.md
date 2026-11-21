# Recovering a character sum from two theta-lift traces

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24410743.svg)](https://doi.org/10.5281/zenodo.24410743)

This result is now maintained in [theta-host-split-inert-race](https://github.com/leecrossley/theta-host-split-inert-race/tree/main/results/theta-prime-trace). This repository is archived and keeps its releases and DOI.

This is a Lean-checked identity inside the tower of theta lifts used by the pinned upstream development. Take the local Hecke traces at two consecutive steps of the tower. Subtracting one from the other, after undoing a twist, and dividing by an explicit positive factor returns, at each prime ideal, the value of the character of the segment added at the later step. Summing with weights over a finite set of prime ideals then gives exactly a weighted sum of that character.

A bound on the difference of two adjacent rows of the tower would therefore bound the weighted sum of the tower's character; a residue-class race would also need admissible data realizing that race's character. The result is an identity for supplied data. It does not construct that data, and it bounds nothing by itself.

## Statement

For admissible tower data and any finite set of prime ideals, the difference of two consecutive first Hecke traces, after untwisting and dividing by the segment trace, recovers the weighted sum of the new character.

At an unramified prime ideal $v$, let $T_k(v)$ be the sum of the local Hecke parameters after step $k$. Write $q=Nv$, $z_k(v)=(\chi_S\chi_T^{-1})(v)$ and $A_t(q)=\sum_{j=0}^{t-1}q^{(t-1)/2-j}$, where the two characters are those of step $k+1$. Then

$$
  T_{k+1}(v)-z_k(v)T_k(v)=\chi_S(v)A_t(q).
$$

For $t>0$, $A_t(q)>0$. Divide and sum over any finite set of good prime ideals with weight $(\log Nv)W(Nv/y)$. Two adjacent rows then recover the weighted character sum exactly, with the character values retaining their signs and phases. Here $W$ is the dyadic tent: $W(t)=2(1-1/t)$ for $1<t\le2$, $4/t-1$ for $2<t<4$, and zero otherwise.

The audited Lean theorems are `ThetaTransfer.theta_step_trace`, `ThetaTransfer.theta_prime_trace_extract` and `ThetaTransfer.theta_band_prime_trace` in [ThetaPrimeTrace.lean](ThetaPrimeTrace.lean).

## Scope

Lean checks the local recursion, the nonzero denominator and both finite-sum identities. The statements are identities for supplied tower data. An estimate for a specified prime race would also require admissible data for its character and a bound on the difference of the rows. Local theta-parameter formulas have precedents in the work of Atobe and Gan. [Atobe and Gan](https://arxiv.org/abs/1602.01299)

[PROOF.md](PROOF.md) has the derivation, a table mapping each step of the upstream argument to its Lean declaration, and a concrete character to test.

## Verification

For a fresh build on x86-64 Linux with Git, curl, tar, zstd and Python 3.9 or later, run

```sh
bash verify-linux.sh
```

This checks the [SHA-256 manifest](SHA256SUMS), downloads the pinned dependencies and compares the resulting kernel and axiom summary with the [recorded run](evidence/check.txt). The environment is fixed by Lean 4.33.1, a pinned Mathlib commit and a pinned source archive. Exact versions, hashes and the route for an existing installation are in [PROOF.md](PROOF.md#reproducing-the-lean-check). [Latest release](https://github.com/leecrossley/theta-prime-trace/releases/latest)

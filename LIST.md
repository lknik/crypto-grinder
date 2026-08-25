# Findings

This file is the maintained index of cryptographic works for which the project records a concrete issue.

It is intentionally terse. Full arguments belong in the relevant paper, analysis, or contribution.

An entry distinguishes the **finding** from its **scope**. A defect in one component does not by itself imply that every security property of the surrounding construction fails.

In the evidence column, a section number links into the methodology paper,
arXiv:2608.21986, and `CRT/RLWE` links to IACR ePrint 2026/1734.

## Demonstrated security breaks

| Work | Finding | Scope / status | Evidence |
|---|---|---|---|
| Talapatra, Mishra, Mukhopadhyay, *Ring-LWR based Commitments and ZK-PoKs*, AsiaCCS 2025 | Verification accepts an opener-chosen multiplier of norm at most one, so the permitted value zero opens the zero commitment to every message. All three proof protocols follow, and the extractor divides by challenge differences that can be zero divisors | Break. Binding fails with probability one for every public key; extraction is undefined for half the challenge pairs. Ring-LWR itself is not attacked | [§4.1](https://arxiv.org/abs/2608.21986) |
| Cherkaoui, Heravi, Kahrobaei, Shahandashti, *Spinel*, arXiv:2602.09882v2, 2026 | Bytes are written in base three with leading zero trits suppressed, and the variable-length codewords are concatenated without boundaries, so the encoding is not injective. `01 04` and `04 01` drive the same walk, as do the printable equal-length pair `(y` and `y(` | Break of collision and second-preimage resistance at the byte interface, deterministic and search-free. 244 of 255 nonzero bytes have an immediate second preimage. First-preimage resistance is not attacked, and the SL(4,p) navigation problem is untouched | [§4.2](https://arxiv.org/abs/2608.21986) |
| Roşca, Sakzad, Stehlé, Steinfeld, *Middle-Product LWE*, CRYPTO 2017; and Bai, Boudgoust, Das, Roux-Langlois, Wen, Zhang, *Middle-Product LWR*, ASIACRYPT 2019 | The first ciphertext component is an ordinary non-wrapping product, so its boundary coefficients peel the binary masks layer by layer through a subset-sum table | Break of the published t=9 parameter rows. Passive, one ciphertext, all 2313 masks and the plaintext recovered, success at least 0.999999730074. Abstract MP-LWE and MP-CLWR are not solved, and the theorem regime t≥98 stands | [§4.3](https://arxiv.org/abs/2608.21986) |
| Farzaliyev, Pärn, Saarse, Willemson, *Lattice-Based ZK Proofs in Action: Electronic Voting*, J. Cryptology 2025 | The printed fake-receipt simulator preserves the coefficients equal to ±2 and resamples the rest uniformly, so its marginal never equals the genuine convolution law. The transcript also permits public special decryption of the claimed vote | Break of receipt-freeness and of vote privacy against a transcript coercer, unconditional. Distance at least 1/15 for every permitted parameter; advantage 0.999999804160 at the published parameters, and the test is provably optimal. BGV and MLWE are not attacked | [§4.4](https://arxiv.org/abs/2608.21986) |
| Albrecht, Benčina, Lai, *Hollow LWE*, EUROCRYPT 2025 | Given the published permutation recovery, the remaining stage is linear algebra: a signed-graph traversal fixes one sign per connected component and the old public-key relation fixes those component signs | Break of IND-CR-CPA confidentiality for pre-update ciphertexts, conditional on the published permutation recovery, which is other authors' work and is credited as such. Recovers a valid old decryption key in O(k³+nk²) operations | [§4.5](https://arxiv.org/abs/2608.21986) |
| Vodenicarevic et al. (Massa Labs), *Two-Limb CRT Ring-LWE Encryption with Exact Decryption and Public Re-randomization*, IACR ePrint 2026/1618, 2026 | Decryption centre-lifts the second CRT limb to recover the exact noise, and the parameters set the plaintext scale to q2 mod t. Adding the same shift to one ciphertext coefficient in both limbs cancels in the plaintext until that lift wraps, at which point the recovered plaintext moves by exactly one and the inner authenticated payload rejects | Break of the composed malicious-rerandomiser claim, conditional on acceptance being observable. Binary search on the accept bit returns each noise coefficient and then the key, at most 131072 adaptive reactions from one captured ciphertext at the source's parameters. Unifying error codes does not remove the oracle, since accept against generic reject is the entire signal. The raw IND-CPA and IND$ statements are not contradicted | [§4.6](https://arxiv.org/abs/2608.21986) |
| Bombar, Couvreur, Debris-Alazard, *On Codes and Learning With Errors over Function Fields*, CRYPTO 2022 | The explicit constructive normal basis has a Galois orbit supported factorwise, so the global basis is a disjoint union of local ones and the projected Bernoulli rate does not rise | Break of the printed instance only. The degree-63 example collapses to seven degree-nine problems, 3584 candidate tests per scan. The authors' own warning that this basis may be inadequate is prior public information and is credited; an independently sampled random normal basis is not attacked | [§4.8](https://arxiv.org/abs/2608.21986) |
| Pradhan, Dutta, Jangir, Das, *A New CRT-based Fully Homomorphic Encryption*, IACR CiC 2026 | The CRT map eliminates every error coefficient for an explicitly admissible, efficiently samplable error law, so the error is publicly removable | Break for one permitted member of the admitted family, giving passive key and plaintext recovery and refuting a universal security statement. Ordinary Gaussian errors, the unspecified benchmark sampler, and standard RLWE are not attacked | [CRT/RLWE](https://eprint.iacr.org/2026/1734) |

## Assumption, specification, and parameter defects

| Work | Finding | Scope / status | Evidence |
|---|---|---|---|
| Liu, Fu, *LWE over Group Rings by Semi-direct Product*, DCC 2026 | The augmentation map that every integral group ring carries projects a genuine sample to a one-dimensional sample of bounded error width, and two samples distinguish it from uniform | Assumption defect against the natural universal reading of the full-ring decision claim, along an explicitly permitted parameter sequence. It is a search recovery of one linear functional of the secret, and generalises to every sign character. No complete PKE break | [§4.9](https://arxiv.org/abs/2608.21986) |
| Liu, Fu, *LWE over Group Rings by Semi-direct Product*, DCC 2026 | The decision definition requires a distribution over error laws while the theorem supplies only a set of Gaussians. Under an explicit Gaussian completion, both selected quotient families map onto rank-four orders and the quotient secret can be enumerated | Assumption defect against an explicit completion, not against a fully specified scheme. The rank-four image is proved maximal among quotients preserving the small-error scale, which bounds the quotient mechanism rather than every statistical attack | [§4.9](https://arxiv.org/abs/2608.21986) |
| Albrecht, Benčina, Lai, *Hollow LWE*, EUROCRYPT 2025 | The reduction turns ordinary LWE of dimension k−h into Hollow LWE of width k, but the appended parameter script invokes the lattice estimator at dimension k | Parameter certification defect. The printed 128, 192 and 256-bit labels are not certified by the source's own reduction and estimator combination. This does not by itself place the rows below those levels. Repairing both defects costs 1.24 to 1.54× in size | [§4.5](https://arxiv.org/abs/2608.21986) |
| Patarin, Vacek, Roullet, *Ultra short signatures with Dragon HFE_{LL'}*, IACR ePrint 2026/404, 2026 | Three steps in the MinRank hardening accounting fail under the source's own support-minor cost model. The split between signature and hash variables is public, so the principal block returns the Dragon ambient dimension from n+m to n; the degree-3 differential rank is carried at its average while the attacker selects the direction and pays only the lower tail; and exact-one signing leaves a degree-2 relation whose polar kernel is the common annihilator of the whole perturbation | Parameter and accounting defect. The 128-bit Dragon row moves from 2^131.89 to 2^125.53, the degree-3 128-bit rows to between 2^100.75 and 2^103.65, and the 256-bit row to 2^187.45. No MinRank attack was executed, so no key recovery is claimed. A signer mixing odd and even hypothesis weights destroys the constant relation and is not the same scheme | [§4.7](https://arxiv.org/abs/2608.21986) |
| Kim, Lee, Seo, Song, *Hint-MLWE*, CRYPTO 2023 | Read without the theorem's distribution restrictions, the parameterized definition admits a degenerate choice that reveals the randomness exactly | Assumption defect in how the definition may be cited. It does **not** contradict the Gaussian hardness theorem, which excludes that choice | [§4.10](https://arxiv.org/abs/2608.21986) |
| Cherkaoui, Heravi, Kahrobaei, Shahandashti, *Spinel*, arXiv:2602.09882v2, 2026 | The digest is described as having 2^512 possible values, but the determinant constraint and the unused top bit of each serialized word put the space at 2^465 | Parameter accounting error, independent of the encoding defect and not repaired by fixing it. The idealised classical birthday scale is 2^232.5 | [§4.2](https://arxiv.org/abs/2608.21986) |

## Coverage gaps, recorded without an attack

These are readings of what a source actually proves, not defects in it. They are listed so that a coverage gap is never mistaken for a break.

| Work | Finding | Scope / status | Evidence |
|---|---|---|---|
| Agrawal, Rossi, Yadav, Yamada, *Constant Input ABE from Evasive and Tensor LWE*, CRYPTO 2023 | The standard-LWE reduction covers only the all-zero case and one common fixed input, while the ABE theorem invokes the full varying assumption | Coverage gap. No attack. The source explains why it stops where it does | [§5](https://arxiv.org/abs/2608.21986) |
| Wee, *Circuit ABE with poly(depth, λ)-Sized Ciphertexts*, CRYPTO 2024 | Ordinary LWE supports the wide regime, while the construction providing the compression uses the narrow one, supported by adding public-coin evasive LWE | Coverage gap. No attack. The compression gain sits in the stronger part of the assumption | [§5](https://arxiv.org/abs/2608.21986) |
| Jain, Lin, Saha, *A Systematic Study of Sparse LWE*, CRYPTO 2024 | Hardness follows from ordinary LWE in dimension about the sparsity, not the nominal dimension | Coverage gap, and deliberately **not** recorded as a finding against the source, which presents this picture itself | [§5](https://arxiv.org/abs/2608.21986) |

## Reading the list

The wording in **Scope / status** states how far the evidence goes. The distinctions used here are:

- demonstrated security break;
- construction or specification defect;
- proof gap;
- parameter or accounting error;
- coverage gap;
- conditional consequence;
- known or corrected issue;
- unresolved candidate.

The table avoids stronger language than the supporting evidence justifies. Where a result depends on other authors' work, that dependence is stated in the scope column rather than absorbed into the finding.

## External submissions

Outside researchers should normally submit new material under [`contributions/`](contributions/) rather than editing this file directly.

Project maintainers update the list after reviewing the evidence and determining the appropriate scope.

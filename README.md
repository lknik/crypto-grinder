# Crypto Grinder

We grind on published cryptography with AI until the attack fails, the claim fails, or we find the boundary between the two.

Start with [`LIST.md`](LIST.md) for the findings.

If you want to run the process yourself, see [`SKILL.md`](SKILL.md).

If you found something new, [`contributions/`](contributions/) is open for pull requests. Let's make a repository of grinded results. Did you break RLWE? How about a hash function? Just make a PR.

## What this is

Crypto Grinder grew out of research on AI-assisted and AI-driven cryptanalysis.

A promising observation is turned into something testable.  Sometimes that ends in a security break. Sometimes it exposes a defect, proof gap, parameter mistake, or unsupported claim. Sometimes the attack stops and the interesting result is the boundary itself.

**You can do it too!** The methodology is described in **[AI Grinding for Fun and Cryptanalysis](papers/ai-grinding-for-fun-and-cryptanalysis.pdf)** and distilled into an agent-readable procedure in [`SKILL.md`](SKILL.md).

## Start here

### [`LIST.md`](LIST.md)

The maintained list of analyzed cryptographic works and identified issues.

Each entry records:

* the work;
* the issue;
* how far the result goes;
* where the supporting analysis or reproduction material lives.

### [`SKILL.md`](SKILL.md) to automate things


```text
claims
  ↓
joins and structure
  ↓
attack hypotheses
  ↓
witness + control
  ↓
security consequence
  ↓
push until break or boundary
```

The reasoning behind the process is in the methodology paper.

## Contributions

Found something interesting in a cryptographic paper, protocol, proof, or implementation?

External findings are welcome as pull requests under [`contributions/`](contributions/).

Create:

```text
contributions/<paper-or-project-name>/
```

and include a `README.md` explaining:

* **Target**: what paper, project, specification, or implementation you analyzed;
* **Issue**: what appears to be wrong;
* **Evidence**: how the result can be checked or reproduced;
* **Scope**: what the result establishes and where its limitations are.

Add scripts, calculations, data, test vectors, or other material if they help establish the result.

External finding PRs should modify only `contributions/**`. The project maintainers review submissions and update [`LIST.md`](LIST.md) separately.

See [`contributions/README.md`](contributions/README.md) for the minimal format.

## Papers

[AI Grinding for Fun and Cryptanalysis](https://arxiv.org/abs/2608.21986)

The methodology paper.

[Key Recovery from Residue-Confined Errors in the Pradhan CRT-RLWE Construction](https://eprint.iacr.org/2026/1734)

The CRT-RLWE cryptanalysis that informed part of the methodology.

## Citation


```bibtex
@misc{olejnik2026aigrindingfuncryptanalysis,
  title = {AI Grinding for Fun and Cryptanalysis},
  author = {Lukasz Olejnik and Bartosz Naskrecki},
  year = {2026},
  eprint = {2608.21986},
  archivePrefix = {arXiv},
  primaryClass = {cs.CR},
  url = {https://arxiv.org/abs/2608.21986}
}
```


```bibtex
@misc{cryptoeprint:2026/1734,
  author = {Lukasz Olejnik and Bartosz Naskrecki},
  title = {Key Recovery from Residue-Confined Errors in the Pradhan {CRT}-{RLWE} Construction},
  howpublished = {Cryptology {ePrint} Archive, Paper 2026/1734},
  year = {2026},
  url = {https://eprint.iacr.org/2026/1734}
}
```

If you want to cite the maintained list, `SKILL.md`, or repository material directly, cite:

```bibtex
@misc{cryptogrinder2026,
  author       = {Olejnik, Lukasz and Naskrecki, Bartosz},
  title        = {Crypto Grinder},
  year         = {2026},
  howpublished = {\url{https://github.com/lknik/crypto-grinder}},
  note         = {AI-assisted cryptanalysis, findings, and research methodology}
}
```

## License

[CC BY-NC-ND 4.0](LICENSE).
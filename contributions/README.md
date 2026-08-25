# Contributing a finding

External research contributions are welcome through pull requests under this directory.

For a new finding, create:

```text
contributions/<paper-or-project-name>/
```

For external finding submissions, please keep the pull request limited to `contributions/**`. Project maintainers update the root `LIST.md` after reviewing the result.

## Minimal format

Every contribution should contain a `README.md` with four short sections.

### Target

Identify the paper, specification, implementation, or project.

Include the title, authors or project name, a public URL, and the relevant version or date where useful.

### Issue

Describe the identified problem and the part of the construction, proof, parameterization, or implementation that it concerns.

State the claim being challenged when there is a specific one.

### Evidence

Explain how the issue can be checked.

Include the shortest practical reproduction instructions. Add scripts, calculations, data, test vectors, or other supporting material when they are useful.

There is no required internal directory layout beyond this README.

### Scope

State what the result establishes and the important conditions or limitations.

Do not claim a stronger consequence than the submitted evidence demonstrates.

## Review

A contribution is evidence submitted for review. The maintained record is [`../LIST.md`](../LIST.md), which is updated by the project maintainers after evaluating the result and its scope.

## License

You keep copyright in what you submit. By opening a pull request you grant the authors a perpetual, non-exclusive licence to use, modify, publish, and distribute it, including in later publications, and your submission is offered to the public under [CC BY-NC-ND 4.0](../LICENSE) like the rest of the repository.

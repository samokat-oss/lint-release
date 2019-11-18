# lint-version

> Lint tool for compare version in git branch and package.json

## TL;DR

Just install and start using. 😎

```
yarn add @samokat/lint-release --dev

yarn lint-release
```

## What?

We store application version in `package.json` file and [create separate git branch for every release](https://trunkbaseddevelopment.com). This tool enforce similar versions in two source.

In allows branches with names satisfying pattern `release/X.X.X` and strictly compare it with a version in `package.json`.

### Examples

|package.json version|branch name    |result |
|:------------------ |:------------- |:-----:|
|1.0.0               |master         |✅     |
|2.2.0               |development    |✅     |
|1.0.0               |feature/tl-12  |✅     |
|2.2.0               |release/2.2.0  |✅     |
|2.2.0               |release/2.2.1  |🛑     |
|1.0.0               |release/2.2.0  |🛑     |

## How?

You can use in tool on CI, or add git-hook for linting.

### CI specific

In some cases, on CI we can't use `git` for retriving branch name and CI provide it in env variables. This tool supports specific args for that case.

**Example**
If your CI provide `BRANCH_NAME` variable, you can just pass it to linter:
```
yarn lint-release --branch=$BRANCH_NAME
```

### Husky example

Never allow commit with different versions in branch and `package.json`.

```json
{
  // ...
  "husky": {
    "hooks": {
      "pre-commit": "yarn lint-release",
    }
  },
  // ...
}
```

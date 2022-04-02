Diff Actions
---

This action check if a file or directory has differences.

## Usage

If you want to check if some file has a difference, define a job like the following.

Note that multiple revisions must be fetch with [actions/checkout](https://github.com/actions/checkout)'s `fetch-deps`.

```yaml
jobs:
  file-watch:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
        with:
          fetch-depth: 0
      - uses: hyorimitsu/check-diff@v0.0.1
        id: diff
        name: diff
        with:
          target-branch: main
          target-file: test/file1.json
      - name: difference check
        if: steps.diff.outputs.file-diff > 0
        run: |
          echo 'test/file1.json is changed'
```

See [here](https://github.com/hyorimitsu/actions-diff/blob/main/.github/workflows/example.yaml) for other examples.

## Input / Output parameters

The input parameters are as follows.

|key          |required|description|
|-------------|--------|-----------|
|target-branch|true    |The branch that triggers this action.|
|target-file  |false   |The path to the file where you want to check for differences.|
|target-dir   |false   |The path to the directory where you want to check for differences.|

The output parameters are as follows.

|key      |description|
|---------|-----------|
|file-diff|If over 0, there is a difference in the `target-file`.|
|dir-diff |If over 0, there is a difference in the `target-dir`.|

## License

The scripts and documentation in this repository are released under the [MIT License](https://github.com/hyorimitsu/actions-diff/blob/main/LICENSE).

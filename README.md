<p align="center">
  <a href="https://github.com/jitterbit/get-changed-files/actions"><img alt="jitterbit/get-changed-files status" src="https://github.com/jitterbit/get-changed-files/workflows/Test/badge.svg"></a>
</p>

# Get All Changed Files

Get all of the files changed/modified in a pull request or push's commits.
You can choose to get all changed files, only added files, only modified files, only removed files, only renamed files, or all added and modified files.
These outputs are available via the `steps` output context.
The `steps` output context exposes the output names `all`, `added`, `modified`, `removed`, `renamed`, and `added_modified`.

# Usage

See [action.yml](action.yml)

```yaml
- uses: jitterbit/get-changed-files@v1
  with:
    # Format of the steps output context.
    # Can be 'json'.
    # Default: 'json'
    format: ''
```

# Scenarios

- [Get all removed files as JSON](#get-all-removed-files-as-json)

## Get all removed files as JSON

```yaml
- id: files
  uses: jitterbit/get-changed-files@v1
  with:
    format: 'json'
- run: |
    readarray -t removed_files <<<"$(jq -r '.[]' <<<'${{ steps.files.outputs.removed }}')"
    for removed_file in ${removed_files[@]}; do
      echo "Do something with this ${removed_file}."
    done
```

# Install, Build, Lint, Test, and Package

Make sure to do the following before checking in any code changes.

```bash
$ yarn
$ yarn all
```

# License

The scripts and documentation in this project are released under the [MIT License](LICENSE)

# queensac-action

`queensac-action` packages the [queensac][queensac-repo] Rust CLI as a ready-to-use GitHub Action. The Action clones a target repository, scans every document for HTTP(S) links, detects broken references, and can automatically open a pull request with fixes.

[English](README.md) | [한국어](README.ko.md)

## How It Works

- Extract links with the same logic as `queensac` using `git2` and fast tree walks.
- Validate URLs with `reqwest`, classifying invalid links, redirects, and GitHub file moves.
- Autogenerate pull requests through the GitHub App flow powered by `octocrab`.

## Usage

```yaml
- name: 👑 Run queensac
  uses: reddevilmidzy/queensac-action@v1
  with:
    repo: https://github.com/${{ github.repository }}
    branch: main
    dry-run: true
    github_app_id: ${{ secrets.QUEENSAC_APP_ID }}
    github_app_private_key: ${{ secrets.QUEENSAC_APP_PRIVATE_KEY }}
```

### Inputs

| Name | Required | Description |
| --- | --- | --- |
| `repo` | No | GitHub repository URL to scan. Defaults to the workflow repo. |
| `branch` | No | Branch to inspect and use as the PR base (defaults to `main`). |
| `dry-run` | No | When `true`, only logs invalid links without creating a PR. |
| `github_app_id` | No | GitHub App identifier used for authentication. |
| `github_app_private_key` | No | PEM-encoded private key for the GitHub App. |

## License

Apache-2.0. See [LICENSE](LICENSE).

[queensac-repo]: https://github.com/reddevilmidzy/queensac

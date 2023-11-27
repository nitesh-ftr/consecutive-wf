# Consecutive Workflow Action

Make workflow runs run consecutively.

## Usage

```yaml
jobs:
  consecutiveness:
    runs-on: ubuntu-latest
    steps:
    - uses: 
      with:
        token: ${{ secrets.GITHUB_TOKEN }}

  # your other jobs
  something:
    runs-on: ubuntu-latest
    needs: [ consecutiveness ]
    steps:
    # ...
```

### Security Notes:

#### Access Token

The token is needed to avoid rate limitation issues when performing API calls. I was thinking about making that optional but decided to just make you aware of the security risk and how to avoid it.

Please read [this section in the docs](https://docs.github.com/en/actions/learn-github-actions/security-hardening-for-github-actions#using-third-party-actions) before using some random action that asks for your secrets.

To use the latest version automatically, use the `main` branch.

```yaml
- uses: mktcode/consecutive-workflow-action@main
```

I recommend using a commit hash instead though, like in the usage example.

#### Workflow Permissions

It's always a good idea to [limit permissions](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#permissions-for-the-github_token) to the required minimum. To read information about previous runs, the workflow needs at least the `actions: read` permission.

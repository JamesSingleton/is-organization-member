# Is Organization Member

This action returns if someone belongs to a certain organization or not.

## Usage

An example workflow using the action:

```yaml
name: Is Organization Member Example

on:
  issues:
    types: [opened, labeled]

jobs:
  welcome:
    name: Welcome
    runs-on: ubuntu-latest
    steps:
      - name: Check if organization member
        id: is_organization_member
        if: github.event.action == 'opened'
        uses: jamessingleton/is-organization-member@v1
        with:
          organization: testorg
          username: ${{ github.event.issue.user.login }}
          token: ${{ secrets.GITHUB_TOKEN }}
      - name: Create Comment
        if: |
          steps.is_organization_member.outputs.result == false
        run: echo User Does Not Belong to testorg
```

> **Note:** In order to check whether a member is part of the organization
> or not, the members **must** have their "Organization Visibility" set to
> Public.
> In order to ensure your "Organization Visibility" is correct, please,
> check https://github.com/orgs/**your_organization**/people.

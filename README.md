# determine-next-version-mobile-app
This action looks at git tags in a repository that begin with `v`, and are of format `x.y.z(n)`, where `x`, `y`, `z`, and `n` are integers that represent the major, minor, patch, and version code respectively. It then sets an output with `x.y.z(n+1)`. In the GitHub action [determine-next-version](https://github.com/gps/determine-next-version) the version was in the form `x.y.z`, this action updates it to be of form `x.y.z(n)`.

## Inputs

### `gh_token`

The GitHub token used to authenticate with GitHub.

### `tag_prefix`

Prefix to look for in version tags.

**Default Value** 

If unspecified, assumed to be `v`.

## Outputs

### `next_build_version`

Next build version to use.

## Example Usage

```yml
- name: Determine next version
  uses: gps/determine-next-version-mobile-app@master
  id: next_version
  with:
    GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
    TAG_PREFIX: v

- name: Tag commit
  uses: gps/tag_commit@master
  with:
    GH_TOKEN: ${{ secrets.GITHUB_TOKEN }}
    TAG_NAME: v${{steps.next_version.outputs.NEXT_BUILD_VERSION}}
```
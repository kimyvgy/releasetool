# release-tool

There is small script can be helpful when releasing your application with [standard-version](https://github.com/conventional-changelog/standard-version).

## Features

- Parse changelog from CHANGELOG.md by the specific version.

## Usages

Please initialize `package.json` file before using.

It must contain two fields: `version` and `repository.url`. For example:
```json
{
  "version": "1.0.0-beta.1",
  "repository": {
    "url": "https://github.com/kimyvgy/release-tool"
  }
}
```

### Release new version

```bash
export v1=1.0.0-beta.3 v2=1.0.0-beta.4 \
  && standard-version --prerelease --skip.tag \
  && gcan! -m "$(releasenote changelog $v1 $v2)" \
  && git tag -a "v${v2}" -m "v${v2}"
```

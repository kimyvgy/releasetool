# releasetool

The small script is used when releasing new version with [standard-version](https://github.com/conventional-changelog/standard-version).

## Features

- Generate `.verionrc` file for `standard-version`.
- Parse changelog from `CHANGELOG.md` by the specific version. The output format: plain text, markdown.

## Installation

```bash
sudo wget -O /usr/local/bin/releasetool \
  https://github.com/kimyvgy/releasetool/releases/download/v0.1.0/releasetool-v0.1.0
```

## Usages

### Initialize .versionrc

The `.versionrc` file can be auto-created with `releasetool` by following command:

```
releasetool init
```

If you want to modify `.versionrc`, please read [conventional-changelog/conventional-changelog-config-spec](https://github.com/conventional-changelog/conventional-changelog-config-spec/tree/master/versions/2.1.0).

### package.json

Please initialize `package.json` file before using `standard-version`.
It must contain two fields: `version` and `repository.url`. For example:
```json
{
  "version": "0.1.0",
  "repository": {
    "url": "https://github.com/kimyvgy/release-tool"
  }
}
```

### Release

- First release:
```bash
standard-version --first-release --release-as=v0.1.0
```

- Release new version:
```bash
standard-version --prerelease --skip.tag \
  && git commit --amend --no-edit -m "$(releasetool changelog 0.1.0 0.2.0)" \
  && git tag -a v0.2.0 -m "$(releasetool changelog 0.1.0 0.2.0 --markdown)"

git push upstream HEAD --follow-tags
```

# release-tool

There is small script can be helpful when releasing your application with [standard-version](https://github.com/conventional-changelog/standard-version).

## Features

- Parse changelog from CHANGELOG.md by the specific version.

## Installation

```bash
sudo wget -O /usr/local/bin/releasetool https://github.com/kimyvgy/release-tool/archive/releasetool-v0.1.0
```

## Usages

### .versionrc

Create `.versionrc` file:

```
releasetool init
```

### package.json

- Please initialize `package.json` file before using.
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
  && git commit --amend --no-edit -m "$(releasetool changelog 0.1.0 0.2.0)"
  && git tag -a v0.2.0 -m "$(releasetool changelog 0.1.0 0.2.0 --markdown)"

git push upstream HEAD --follow-tags
```

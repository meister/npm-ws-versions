# Example of NPM versionng issue in a monorepo

When bumping a version in a workspace, the dependent packages are udpated as expected:

```sh
❯ npm version minor -w @meister/pkg-b --save --no-git-tag-version --no-commit-hooks
@meister/pkg-b
v1.1.0

up to date in 107ms

❯ jq '.version' -r packages/pkg-b/package.json
1.1.0

❯ jq '.dependencies' -r packages/pkg-a/package.json
{
  "@meister/pkg-b": "^1.1.0"
}
```

However when bumping a prerelease, dependency is not updated. Why? Bug?

```sh
❯ npm version preminor -w @meister/pkg-b --save --no-git-tag-version --no-commit-hooks
@meister/pkg-b
v1.1.0-0

up to date in 98ms

❯ jq '.version' -r packages/pkg-b/package.json
1.1.0-0

❯ jq '.dependencies' -r packages/pkg-a/package.json
{
  "@meister/pkg-b": "^1.0.0"
}
```
> !!! Docs have moved to the [glaredb repo](https://github.com/glaredb/glaredb) !!!

# GlareDB docs

Welcome to GlareDB documentation 👋

## Feedback and issues

Have feature requests or bug reports for [GlareDB] and/or [GlareDB Cloud]? We'd
love to hear from you - please [file an issue].

## Contributions

We welcome contributions and fixes to our documentation. For more information
on contributing, see our [Contributing guidelines].

## Development environment

GlareDB docs are built using [Just the docs]. The following are needed:

- [Ruby] and [RubyGems]
- GCC (`g++`)
  - `build-essential` APT package for debian and Ubuntu
- `make`

Once the above are installed, install [jekyll] and [bundler]:

```shell
gem install jekyll bundler
```

Next, install project dependencies:

```shell
bundler install
```

Finally, a local development server is started on `localhost:4000` with:

```shell
bundle exec jekyll serve
```

### Linting

We have some optional tooling for linting that require [Node.js LTS]. See the
`scripts` in `package.json` for available tooling.

Lint and spell check configurations are available in `cspell.json`,
`.markdownlint-cli2.jsonc` and `.prettierrc.json`.

```shell
# Checking spelling, formatting, and markdown lints.
npm run check:all

# Checks spelling
npm run cspell

# Checks code format
npm run format

# Attempts to automatically fix any formatting issues
npm run format:fix

# Checks code adheres to lint rules
npm run lint

# Attempts to automatically fix any lint violations
npm run lint:fix
```

[GlareDB]: https://github.com/GlareDB/glaredb
[GlareDB Cloud]: https://console.glaredb.com
[Contributing guidelines]: https://github.com/GlareDB/glaredb.github.io/blob/main/.github/CONTRIBUTING.md
[file an issue]: https://github.com/GlareDB/glaredb/issues/new/choose
[Just the docs]: https://just-the-docs.github.io/just-the-docs/
[Ruby]: https://www.ruby-lang.org/en/documentation/installation/
[RubyGems]: https://rubygems.org/
[Node.js LTS]: https://nodejs.org/en
[jekyll]: https://jekyllrb.com
[bundler]: https://bundler.io

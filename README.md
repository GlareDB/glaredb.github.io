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

In addition to the documentation, we have some optional tooling for static
analysis that require [Node.js LTS]. See the `scripts` in `package.json` for
available tooling.

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

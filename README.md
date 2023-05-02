# GlareDB docs

Welcome to GlareDB documentation 👋.

## Feedback and issues

Have feature requests or bug reports for [console.glaredb.com]? We'd love to
hear from you - please [file an issue].

## Contributions

We welcome contributions and fixes to our documentation. For more information
on contributing, see our [Contributing guidelines].

## Development environment

GlareDB docs are built using [Just the docs]. The following are needed:

- [Ruby]
  - Also: [RubyGems] which can typically be installed alongside `ruby`
- GCC (`g++`)
  - `build-essential` APT package for debian and Ubuntu
- `make`

In addition to the documentation, we have some optional tooling for static
analysis. The following are needed:

- [Node.js LTS]
- [Yarn]

Once the above are installed, install [jekyll] and [bundler]:

```console
gem install jekyll bundler
```

## Getting started

Install project dependencies:

```console
# From the project root
bundler install
```

Develop locally (`localhost:4000`):

```console
# From root of project
bundle exec jekyll serve
```

### Static analysis

We use `markdownlint` for linting and `prettier` for formatting. To see the
configurations, check out `.markdownlint.jsonc` and `.prettierrc.json`
respectively.

From the root of the project:

```console
# Checks code format
yarn format

# Attempts to automatically fix any formatting issues
yarn format:fix

# Checks code adheres to lint rules
yarn lint

# Attempts to automatically fix any lint violations
yarn lint:fix
```

### Adding plugins

Adding plugins:

- Add the following to your site's `Gemfile`:

```ruby
gem "<plugin>"
```

- And add the following to your site's `_config.yml`:

```yaml
plugins:
  - "<plugin>"
```

## Licensing and attribution

This repository is licensed under the [MIT License]. You are generally free to
reuse or extend upon this code as you see fit; just include the original copy of
the license (which is preserved when you "make a template"). While it's not
necessary, we'd love to hear from you if you do use this template, and how we
can improve it for future use!

The deployment GitHub Actions workflow is heavily based on GitHub's mixed-party
[starter workflows]. A copy of their MIT License is available in
[actions/starter-workflows].

<!-- Links -->

[console.glaredb.com]: https://console.glaredb.com
[Contributing guidelines]: https://github.com/GlareDB/glaredb.github.io/blob/main/.github/CONTRIBUTING.md
[file an issue]: https://github.com/GlareDB/glaredb.github.io/issues/new/choose
[Just the docs]: https://just-the-docs.github.io/just-the-docs/
[Ruby]: https://www.ruby-lang.org/en/documentation/installation/
[RubyGems]: https://rubygems.org/
[Node.js LTS]: https://nodejs.org/en
[Yarn]: https://yarnpkg.com/getting-started/install
[jekyll]: https://jekyllrb.com
[bundler]: https://bundler.io
[MIT License]: https://en.wikipedia.org/wiki/MIT_License
[starter workflows]: https://github.com/actions/starter-workflows/blob/main/pages/jekyll.yml
[actions/starter-workflows]: https://github.com/actions/starter-workflows/blob/main/LICENSE

# GlareDB docs

GlareDB docs are built using
[Just the docs](https://just-the-docs.github.io/just-the-docs/)

## Development environment

The following are needed:

- [Ruby](https://www.ruby-lang.org/en/documentation/installation/)
  - Also: [RubyGems](https://rubygems.org/) which can typically be installed
    alongside `ruby`
- GCC (`g++`)
  - `build-essential` APT package for debian and Ubuntu
- `make`

Once the above are installed, install [`jekyll`](https://jekyllrb.com) and
[`bundler`](https://bundler.io):

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

---

[MIT License]: https://en.wikipedia.org/wiki/MIT_License
[starter workflows]:
  https://github.com/actions/starter-workflows/blob/main/pages/jekyll.yml
[actions/starter-workflows]:
  https://github.com/actions/starter-workflows/blob/main/LICENSE

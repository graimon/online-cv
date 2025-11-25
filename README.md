# Online CV

Personal CV/resume website built with Jekyll. Live at **https://cv.rayware.ninja**

Based on the [Online CV Jekyll Theme](http://webjeda.com/online-cv/) by Xiaoying Riley at [3rd Wave Media](http://themes.3rdwavemedia.com/).

## Quick Start

```bash
# Install dependencies
bundle install

# Local development
bundle exec jekyll serve
# Visit http://localhost:4000

# Build for production
bundle exec jekyll build
```

## Deployment

The built site is deployed via the `graimon.github.io` repository:

```bash
bundle exec jekyll build
cp -R _site/* ../graimon.github.io/
cd ../graimon.github.io
git add . && git commit -m "Update CV" && git push
```

## Content Editing

- **English content:** `_i18n/en.yml`
- **Spanish content:** `_i18n/es.yml`
- **Site metadata:** `_config.yml`

See [CLAUDE.md](CLAUDE.md) for detailed documentation.

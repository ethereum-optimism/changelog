# changelog

This repo contains the source for Optimism's standalone changelog website [changelog.optimism.io](https://changelog.optimism.io)

## Adding Releases

To add a new releases:

1. Create a new file in `_posts` with the filename `YYYY-MM-DD-slugified-title.md`.
2. Add the frontmatter described below.
3. Write whatever content you want for the release.
4. PR, merge, then commit to master. Netlify will do the rest.

All posts need the following frontmatter:

```
---
title: Your title here
layout: version
packages:
    kovan:
      - name: foo-package
        version: 1.2.3
    mainnet:
      - name: bar-package
        version: 0.1.2
---

```

Packages described in the `packages` stanza must map to packages deployed by the monorepo, otherwise version links won't work.
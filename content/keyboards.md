---
title: "Keyboard Shortcuts"
description: ""
summary: ""
date: 2024-11-20T17:25:48-05:00
lastmod: 2024-11-20T17:25:48-05:00
draft: false
seo:
  title: "" # custom title (optional)
  description: "" # custom description (recommended)
  canonical: "" # custom canonical URL (optional)
  noindex: false # false (default) or true
---

The following are some canonical keyboard shortcuts for navigating this site:

| Keys    | Action              | Type       |
| :------ | :------------------ | :--------- |
| `C-K`   | Open Search Bar[^1] | Built-In   |
| `C-S-\` | Toggle Light/Dark   | Custom[^2] |
| `C-S-[` | Back One Page       | Custom     |
| `C-S-]` | Next One Page       | Custom     |
| `C-S-'` | To Top              | Custom     |
| `C-S-/` | To Bottom           | Custom     |
| `C-S-,` | To Site's Home      | Custom     |
| `C-S-.` | To This Page        | Custom     |

where `C-S-Key` means `Ctrl+Shift+key`, `C-Key` means `Ctrl+key`.

[^1]: If you use an extension like [vimium](https://github.com/philc/vimium) or [vimium-c](https://github.com/gdh1995/vimium-c), the `Esc` key might not work as expected when in search mode.

[^2]: In case you are also using doks and are wondering how to add custom shortcuts, you can see my simple implementation [here](https://github.com/ZebraAlgebra/portfolio-website/blob/main/layouts/partials/head/script-header.html). If you are hosting on Netlify, you would also need to modify the [CSP](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP) settings (in my case, I used the `unsafe-inline` option as specified in my [`netlify.toml`](https://github.com/ZebraAlgebra/portfolio-website/blob/main/netlify.toml#L43)) for custom inline javascripts to be able to execute in production environment.

{{< link-card title="Back to Home" href="/" >}}

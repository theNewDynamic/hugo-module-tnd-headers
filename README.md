# headers Hugo Module

WIP!

## Requirements

Requirements:
- Go 1.14
- Hugo 0.61.0


## Quick setup

## 1. Add module to your project's imports:

```yaml
# config.yaml
module:
  imports:
    - path: github.com/theNewDynamic/hugo-module-tnd-headers
```

### 2. Add redirect output format for chosen service.

#### Netlify

Set configuration so Hugo produces the headers file at the root of the site (on the Homepage)

```yaml
# config.yaml

outputs:
  homepage: 
    - HTML
    - tnd_headers_netlify
    # + any other outputs needed on the homepage.
```
OR

```yaml
# content/_index.md
title: Homepage
homepage: 
  - HTML
  - tnd_headers_netlify
  # + any other outputs needed on the homepage.
```

### Settings

Settings are added to the project's parameter under the `tnd_headers` map as shown below.

```yaml
# config.yaml
params:
  tnd_headers:
    headers:
      - target: /*
        values:
          - key: Referrer-Policy
            value: strict-origin-when-cross-origin
          - key: Feature-Policy
            value: camera 'none'; geolocation 'none'; microphone 'none'
```

## theNewDynamic

This project is maintained and love by [thenewDynamic](https://www.thenewdynamic.com).
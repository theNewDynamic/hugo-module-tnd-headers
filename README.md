# TND Headers Hugo Module

This module helps create and maintain http headers for your Hugo added either via configutation or a dynamic returning partial on the project's level.

It supports beautiful Netlify but should scope out to more services in the future.

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

### 2. Add headers output format for chosen service.

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

## API

Any given header has to be part of group which targets a URL path.

Any given group of headers are defined by the following fields. Those marked by an * are mandatory

- __target__: the URL to match (default: /*)
- __weight__: A degree of ordering when printing the gorups.(default: 0)
- __headers__\*: A list of headers which requires the following fields:
  - __field__: The [field](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields) of the header (example: Referrer-Policy )
  - __value__: The value of the header (example: trict-origin-when-cross-origin). If an array, the value, each entry will be concanated into one string.

## Configuration

Configuration is set through the site's configurationf file's using the `tnd_headers` reserved fields.

__groups__: A list of custom header groups. See below.


## Adding Custom Headers

### Though Configuration File (hardcoded)
User can add a list of header groups through the site's configuration file. Each group can use the API's available fields.

```yaml
# config.yaml
params:
  tnd_headers:
    groups:
      - headers:
        - field: Referrer-Policy
          value: strict-origin-when-cross-origin
        - field: Feature-Policy
          value: 
            - camera 'none';
            - geolocation 'none';
            - microphone 'none';
      - target: /api/*
        headers:
        - field: Content-Type
          value: application/json
```

With the following settings, the project will produce the following `_headers` file.

```
/*
  Referrer-Policy: strict-origin-when-cross-origin
  Feature-Policy: camera 'none'; geolocation 'none'; microphone 'none'
/api/*
  Content-Type: application/json
```

### Through a Returning Partial (dynamnic)

In order to add header groups dynamically, user can create a dedicated returning partial in the project at `layouts/partials/tnd-headers/AddHeaderGroups.html`. 
The partial should return a slice of maps which uses the API's available fields.

## theNewDynamic

This project is maintained and loved by [thenewDynamic](https://www.thenewdynamic.com).
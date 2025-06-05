# Robots.txt Traefik plugin

<!-- markdownlint-disable-next-line MD001 -->
#### Table of Contents

1. [Description](#description)
2. [Setup](#setup)
3. [Usage](#usage)
4. [Reference](#reference)
5. [Development](#development)
6. [Contributors](#contributors)

## Description

Robots.txt is a middleware plugin for [Traefik](https://traefik.io/) which add rules based on
[ai.robots.txt](https://github.com/ai-robots-txt/ai.robots.txt/) or on custom rules in `/robots.txt` of your website.

## Setup

```yaml
# Static configuration

experimental:
  plugins:
    robots-txt:
      moduleName: github.com/aon4o/traefik-plugin-robots-txt
      version: {{latest tagged version}}
```

## Usage

```yaml
# Dynamic configuration

http:
  routers:
    my-router:
      rule: host(`localhost`)
      service: service-foo
      entryPoints:
        - web
      middlewares:
        - my-robots-txt

  services:
   service-foo:
      loadBalancer:
        servers:
          - url: http://127.0.0.1
  
  middlewares:
    my-robots-txt:
      plugin:
        robots-txt:
          aiRobotsTxt: true
```

## Reference

| Name        | Description                                 | Default value | Example                                  |
| ------------| ------------------------------------------- | ------------- | ---------------------------------------- |
| aiRobotsTxt | Enable the retrieval of ai.robots.txt list  | `false`       | `true`                                   |
| customRules | Add custom rules at the end of the file     |               | `\nUser-agent: *\nDisallow: /private/\n` |
| overwrite   | Remove the original robots.txt file content | `false`       | `true`                                   |

## Development

This is a fork of the original Plugin by [Solution Libre](https://github.com/solution-libre). If you want to contribute, go to his [repo](https://github.com/solution-libre/traefik-plugin-robots-txt).

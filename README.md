# Sabu

`Sabu` is a simple CLI HTTP server.

## Motivation

For most simple tasks, there are plenty of static
file servers - but each with limitations. Some examples
include that [http-server](https://github.com/indexzero/http-server)
doesn't support basic auth, and [Harp](http://harpjs.com) has rigid
configuration. Some don't work with JavaScript frameworks like
Vue and React. Others require workarounds for CORS issues.

Sabu aims to be minimal and flexible. _As such, it is not (yet)
recommended for production use._

## Installation

It is recommended to install Sabu globally.

```shell
$ npm i -g sabu
```

But it can also be included locally.

```shell
$ cd path/to/your-project
$ npm i --save-dev sabu
```

## Usage

From a CLI, you can simply run Sabu to start serving files. By default,
it will look for an `index.html`, though this is not required.

```shell
$ sabu
```

By default, Saby serves on host `0.0.0.0` and port `8080`, automatically
incrementing the port if it's already in use.

## Options

For usage, run the help command.

```shell
$ sabu --help

Usage: sabu [options]

Options:
  -V, --version     output the version number
  -h, --host <s>    Host (default: "0.0.0.0"
  -p, --port <n>    Port (default: 8080)
  -q, --quiet       Quiet startup (no console output)
  -c, --config <s>  JSON config file with options
  -h, --help        output usage information
```

Sabu can also accept a JSON config file. Any filename is acceptable.

```javascript
// sabu.conf.json
{
    "source": ".",
    "host": "localhost",
    "port": 8084,
    "cors": {
        "preflightMaxAge": 5,
        "origins": ["*"],
        "allowHeaders": [
            "X-Access-Token",
            "Access-Control-Allow-Origin",
            "Access-Control-Allow-Methods",
            "Access-Control-Allow-Headers"
        ],
        "exposeHeaders": ["API-Token-Expiry"]
    }
}
```

## Common Usage

Assuming a file structure like this:

```
my-project
├── build
│   ├── css
│   ├── images
│   ├── index.html
│   ├── js
├── src
│   ├── ...
├── LICENSE
├── package.json
├── package-lock.json
├── README.md
```

A likely scenario would be:

```shell
$ cd my-project
$ sabu ./build
```

## Roadmap

1. An `init` command to generate a default config file
2. More intentional parsing of CORS config (currently just uses `Object.assign`, overwriting any default configs)
3. A `watch` option to monitor for file changes

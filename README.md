# Antikira Lua API

This repository hosts the public LuaJIT scripting documentation for Antikira, including `ffi` notes, callback reference, config access, runtime behavior, and GitHub Pages publishing setup.

## Documentation

- [Docs Home](docs/index.md)
- [Getting Started](docs/lua/getting-started.md)
- [API Overview](docs/lua/api.md)
- [FFI Notes](docs/lua/ffi.md)

## GitHub Pages

This repository includes:

- `mkdocs.yml`
- `.github/workflows/docs.yml`
- [Publishing Guide](docs/publishing.md)

Once GitHub Pages is enabled for GitHub Actions, pushes to `master` will publish the docs site.

## Scope

The docs describe the Lua API currently exposed by Antikira's in-project scripting runtime:

- callbacks
- rendering
- entities
- events
- user commands
- config value access
- `ffi`

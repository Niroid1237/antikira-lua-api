# Antikira LuaJIT Scripting

This repository contains a built-in `LuaJIT` scripting layer with `ffi` support and a menu tab for script management.

## Documentation

Markdown docs:

- [Docs Home](docs/index.md)
- [Getting Started](docs/lua/getting-started.md)
- [API Overview](docs/lua/api.md)
- [FFI Notes](docs/lua/ffi.md)

GitHub Pages setup:

- `mkdocs.yml` is included for a standalone Antikira documentation site
- `.github/workflows/docs.yml` is included for GitHub Pages deployment
- [Publishing Guide](docs/publishing.md)

## Quick Start

1. Build the solution in Visual Studio.
2. Open the in-game menu and go to `SCRIPTS`.
3. Open the scripts folder at `C:\Antikira\scripts`.
4. Start with `example.lua`.

The project auto-builds LuaJIT during Visual Studio builds through `external\luajit\src\msvcbuild.bat`.

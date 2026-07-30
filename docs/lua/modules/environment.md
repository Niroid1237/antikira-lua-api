# Module: `environment`

Script path helpers.

## `environment.scripts_path() -> string`

Returns the current scripts directory path.

Expected default:

```text
C:\Antikira\scripts
```

## `environment.script_path() -> string`

Returns the full path of the current script file.

## `environment.script_name() -> string`

Returns the current script name.

This is the same value exposed by `antikira.script_name()`.

## Example

```lua
antikira.log("scripts folder: " .. environment.scripts_path())
antikira.log("script path: " .. environment.script_path())
antikira.log("script name: " .. environment.script_name())
```

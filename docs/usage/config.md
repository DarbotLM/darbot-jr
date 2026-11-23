# `jr-extra config`

!!! abstract "Overview"

    * `jr-extra config` is a utility to manage the global configuration file.
    * Quickly start the it with `jr-extra config` or `jr-e config`.

## Commands

### `setup`

Interactive setup wizard that helps you configure your default model and API keys.

```bash
jr-extra config setup
```

This will prompt you for:

1. Your default model (e.g., `anthropic/claude-sonnet-4-5-20250929`)
2. Your API key name and value (e.g., `ANTHROPIC_API_KEY`)

### `set`

Set a specific key in the global config file.

```bash
# example: set default model
jr-extra config set DARBOT_JR_MODEL_NAME anthropic/claude-sonnet-4-5-20250929
# or interactively
jr-extra config set
```

### `unset`

Remove a key from the global config file.

```bash
jr-extra config unset DARBOT_JR_MODEL_NAME
```

### `edit`

Open the global config file in your default editor (uses `$EDITOR` or `nano`).

```bash
jr-extra config edit
```

## Configuration keys

For more configuration options, see [global configuration](../advanced/global_configuration.md).

## Implementation

??? note "Run script"

    - [Read on GitHub](https://github.com/DarbotLM/darbot-jr/blob/main/src/jrsweagent/run/utilities/config.py)
    - [API reference](../reference/run/config.md)

    ```python
    --8<-- "src/jrsweagent/run/utilities/config.py"
    ```

{% include-markdown "../_footer.md" %}

# `jr`

!!! abstract "Overview"

    * `jr` is a REPL-style interactive command line interface for using Darbot Jr in the local environment (as opposed to workflows that require sandboxing or large scale batch processing).

<figure markdown="span">
  <div class="gif-container gif-container-styled" data-glightbox-disabled>
    <img src="https://github.com/SWE-agent/swe-agent-media/blob/main/media/jr/png/jr.png?raw=true"
         data-gif="https://github.com/SWE-agent/swe-agent-media/blob/main/media/jr/gif/jr.gif?raw=true"
         alt="jr" data-glightbox="false" width="600" />
  </div>
</figure>


## Command line options

Useful switches:

- `-h`/`--help`: Show help
- `-t`/`--task`: Specify a task to run (else you will be prompted)
- `-c`/`--config`: Specify a config file to use, else we will use [`jr.yaml`](https://github.com/DarbotLM/darbot-jr/blob/main/src/jrsweagent/config/jr.yaml) or the config `DARBOT_JR_CONFIG_PATH` environment variable (see [global configuration](../advanced/global_configuration.md)).
  It's enough to specify the name of the config file, e.g., `-c jr.yaml` (see [global configuration](../advanced/global_configuration.md) for how it is resolved).
- `-m`/`--model`: Specify a model to use, else we will use the model `DARBOT_JR_MODEL_NAME` environment variable (see [global configuration](../advanced/global_configuration.md))
- `-y`/`--yolo`: Start in `yolo` mode (see below)

## Modes of operation

`jr` provides three different modes of operation

- `confirm` (`/c`): The LM proposes an action and the user is prompted to confirm (press Enter) or reject (enter a rejection message)
- `yolo` (`/y`): The action from the LM is executed immediately without confirmation
- `human` (`/u`): The user takes over to type and execute commands

You can switch between the modes with the `/c`, `/y`, and `/u` commands that you can enter any time the agent is waiting for input.
You can also press `Ctrl+C` to interrupt the agent at any time, allowing you to switch between modes.

`jr` starts in `confirm` mode by default. To start in `yolo` mode, you can add `-y`/`--yolo` to the command line.

## Miscellaneous tips

- `jr` saves the full history of your last run to your global config directory.
  The path to the directory is printed when you start `jr`.

## Implementation

??? note "Default config"

    - [Read on GitHub](https://github.com/DarbotLM/darbot-jr/blob/main/src/jrsweagent/config/jr.yaml)

    ```yaml
    --8<-- "src/jrsweagent/config/jr.yaml"
    ```

??? note "Run script"

    - [Read on GitHub](https://github.com/DarbotLM/darbot-jr/blob/main/src/jrsweagent/run/jr.py)
    - [API reference](../reference/run/jr.md)

    ```python
    --8<-- "src/jrsweagent/run/jr.py"
    ```

??? note "Agent class"

    - [Read on GitHub](https://github.com/DarbotLM/darbot-jr/blob/main/src/jrsweagent/agents/interactive.py)
    - [API reference](../reference/agents/interactive.md)

    ```python
    --8<-- "src/jrsweagent/agents/interactive.py"
    ```

{% include-markdown "../_footer.md" %}
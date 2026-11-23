# Inspector: Browse agent trajectories

!!! abstract "Overview"

    * The `inspector` is a tool that allows you to browse `.traj.json` files that show the history of a Darbot Jr run.
    * Quickly start it with `jr-e i` or `jr-extra inspector`.
    * See [output files](output_files.md) for the trajectory file format.
    * Alternative: [jless](https://jless.io/) is a great command-line JSON viewer for browsing trajectories.

<figure markdown="span">
  <div class="gif-container gif-container-styled" data-glightbox-disabled>
    <img src="https://github.com/SWE-agent/swe-agent-media/blob/main/media/jr/png/inspector.png?raw=true"
         data-gif="https://github.com/SWE-agent/swe-agent-media/blob/main/media/jr/gif/inspector.gif?raw=true"
         alt="inspector" data-glightbox="false" width="600" />
  </div>
</figure>

## Usage

```bash
# Find all .traj.json files recursively from current directory
jr-extra inspector
# or shorter
jr-e i
# Open the inspector for a specific file
jr-e i <path_to_traj.json>
# Search for trajectory files in a specific directory
jr-e i <path_to_directory>
```

## Key bindings

- `q`: Quit the inspector
- `h`/`LEFT`: Previous step
- `l`/`RIGHT`: Next step
- `j`/`DOWN`: Scroll down
- `k`/`UP`: Scroll up
- `H`: Previous trajectory
- `L`: Next trajectory
- `e`: Open current step in [jless](https://jless.io/)

### FAQ

> How can I select/copy text on the screen?

Hold down the `Alt`/`Option` key and use the mouse to select the text.

## Implementation

The inspector is implemented with [textual](https://textual.textualize.io/).

??? note "Implementation"

    - [Read on GitHub](https://github.com/DarbotLM/darbot-jr/blob/main/src/jrsweagent/run/utilities/inspector.py)

    ```python linenums="1"
    --8<-- "src/jrsweagent/run/utilities/inspector.py"
    ```

{% include-markdown "../_footer.md" %}
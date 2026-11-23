# SWE-ReX Modal

!!! note "SWE-ReX Modal Environment class"

    - [Read on GitHub](https://github.com/DarbotLM/darbot-jr/blob/main/src/jrsweagent/environments/extra/swerex_modal.py)
    - Requires [Modal](https://modal.com) account and authentication

This environment executes commands in [Modal](https://modal.com) sandboxes using [SWE-ReX](https://github.com/swe-agent/swe-rex).

## Setup

1. Install the full dependencies:
   ```bash
   pip install "Darbot Jr[full]"
   ```

2. Set up Modal authentication:
   ```bash
   modal setup
   ```

## Usage

Evaluate GPT-5 jr on SWE-bench using Modal:
```
jr-extra swebench \
    --config src/jrsweagent/config/extra/swebench_modal.yaml \
    --subset verified \
    --split test \
    --workers 100 \
    -o ./results/gpt5-mini-modal
```

{% include-markdown "../../_footer.md" %}

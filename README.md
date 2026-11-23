<div align="center">
<a href="https://github.com/DarbotLM/darbot-jr"><img src="https://github.com/DarbotLM/darbot-jr/raw/main/docs/assets/darbot-jr-banner.svg" alt="Darbot Jr banner" style="height: 7em"/></a>
</div>

# Darbot Jr

An independently maintained, compact AI software engineering agent.

[![Repository](https://img.shields.io/badge/Repository-GitHub-24292e?style=for-the-badge&logo=github)](https://github.com/DarbotLM/darbot-jr)
[![Docs](https://img.shields.io/badge/Docs-green?style=for-the-badge&logo=materialformkdocs&logoColor=white)](https://github.com/DarbotLM/darbot-jr/tree/main/docs)

> [!WARNING]
> This is **Darbot Jr v2**. Read the [migration guide](docs/advanced/v2_migration.md).

Darbot Jr is maintained at [DarbotLM/darbot-jr](https://github.com/DarbotLM/darbot-jr).
It is an independent distribution derived from an MIT-licensed agent project and retains the original copyright,
license, benchmark interfaces, and research attribution.

We now ask: **What if our agent was 100x simpler, and still worked nearly as well?**

`jr` is

- **Widely adopted**: Used by Meta, NVIDIA, Essential AI, IBM, Nebius, Anyscale, Princeton University, Stanford University, and many more.
- **Minimal**: Just some 100 lines of python for the [agent class](https://github.com/DarbotLM/darbot-jr/blob/main/src/jrsweagent/agents/default.py) (and a bit more for the [environment](https://github.com/DarbotLM/darbot-jr/blob/main/src/jrsweagent/environments/local.py),
[model](https://github.com/DarbotLM/darbot-jr/blob/main/src/jrsweagent/models/litellm_model.py), and [run script](https://github.com/DarbotLM/darbot-jr/blob/main/src/jrsweagent/run/hello_world.py)) — no fancy dependencies!
- **Performant:** Scores >74% on the [SWE-bench verified benchmark](https://www.swebench.com/); starts much faster than Claude Code
- **Deployable:** Supports **local environments**, **docker/podman**, **singularity/apptainer**, **bublewrap**, **contree**, and more
- **Compatible:** Supports all models via **litellm**, **openrouter**, **portkey**, and more. Support for `/completion` and `/response` endpoints, interleaved thinking etc.
- Maintained by DarbotLM on a simple, portable foundation
- **Tested:** [![Codecov](https://img.shields.io/codecov/c/github/DarbotLM/darbot-jr?style=flat-square)](https://codecov.io/gh/DarbotLM/darbot-jr)

<details>

<summary>More motivation (for research)</summary>

[SWE-agent](https://swe-agent.com/latest/) jump-started the development of AI agents in 2024. Back then, we placed a lot of emphasis on tools and special interfaces for the agent.
However, one year later, as LMs have become more capable, a lot of this is not needed at all to build a useful agent!
In fact, the `jr` agent

- **Does not have any tools other than bash** — it doesn't even need to use the tool-calling interface of the LMs.
  This means that you can run it with literally any model. When running in sandboxed environments you also don't need to take care
  of installing a single package — all it needs is bash.
- **Has a completely linear history** — every step of the agent just appends to the messages and that's it.
  So there's no difference between the trajectory and the messages that you pass on to the LM.
  Great for debugging & fine-tuning.
- **Executes actions with `subprocess.run`** — every action is completely independent (as opposed to keeping a stateful shell session running).
  This makes it trivial to execute the actions in sandboxes (literally just switch out `subprocess.run` with `docker exec`) and to
  scale up effortlessly. Seriously, this is [a big deal](docs/faq.md#why-no-shell-session), trust me.

This makes it perfect as a baseline system and for a system that puts the language model (rather than
the agent scaffold) in the middle of our attention.
You can see the result on the [SWE-bench (bash only)](https://www.swebench.com/) leaderboard, that evaluates the performance of different LMs with `jr`.

</details>

<details>
<summary>More motivation (as a tool)</summary>

Some agents are overfitted research artifacts. Others are UI-heavy frontend monsters.

The `jr` agent wants to be a hackable tool, not a black box.

- **Simple** enough to understand at a glance
- **Convenient** enough to use in daily workflows
- **Flexible** to extend

Unlike other agents (including our own [swe-agent](https://swe-agent.com/latest/)), it is radically simpler, because it:

- **Does not have any tools other than bash** — it doesn't even need to use the tool-calling interface of the LMs.
  Instead of implementing custom tools for every specific thing the agent might want to do, the focus is fully on the LM utilizing the shell to its full potential.
  Want it to do something specific like opening a PR?
  Just tell the LM to figure it out rather than spending time to implement it in the agent.
- **Executes actions with `subprocess.run`** — every action is completely independent (as opposed to keeping a stateful shell session running).
  This is [a big deal](docs/faq.md#why-no-shell-session) for the stability of the agent, trust me.
- **Has a completely linear history** — every step of the agent just appends to the messages that are passed to the LM in the next step and that's it.
  This is great for debugging and understanding what the LM is prompted with.

</details>

<details>
<summary>Should I use SWE-agent or Darbot Jr?</summary>

You should consider `Darbot Jr` your default choice.
In particular, you should use `Darbot Jr` if

- You want a quick command line tool that works locally
- You want an agent with a very simple control flow
- You want even faster, simpler & more stable sandboxing & benchmark evaluations
- You are doing FT or RL and don't want to overfit to a specific agent scaffold

You should use `swe-agent` if

- You want to experiment with different sets of tools, each with their own interface
- You want to experiment with different history processors

What you get with both

- Excellent performance on SWE-Bench
- A trajectory browser

</details>

<table>
<tr>
<td width="50%">
<a href="docs/usage/jr.md"><strong>CLI</strong></a> (<code>jr</code>)
</td>
<td>
<a href="docs/usage/swebench.md"><strong>Batch inference</strong></a>
</td>
</tr>
<tr>
<td width="50%">

![jr](https://github.com/SWE-agent/swe-agent-media/blob/main/media/jr/gif/jr.gif?raw=true)

</td>
<td>

![swebench](https://github.com/SWE-agent/swe-agent-media/blob/main/media/jr/gif/swebench.gif?raw=true)

</td>
</tr>
<tr>
<td>
<a href="docs/usage/inspector.md"><strong>Trajectory browser</strong></a>
</td>
<td>
<a href="docs/advanced/cookbook.md"><strong>Python bindings</strong></a>
</td>
</tr>
<tr>
<td>

![inspector](https://github.com/SWE-agent/swe-agent-media/blob/main/media/jr/gif/inspector.gif?raw=true)

</td>
<td>

```python
agent = DefaultAgent(
    LitellmModel(model_name=...),
    LocalEnvironment(),
)
agent.run("Write a sudoku game")
```

</td>
</tr>
</table>

## Let's get started!

**Option 1:** Run the CLI directly from the public repository

```bash
pip install uv && uvx --from git+https://github.com/DarbotLM/darbot-jr.git darbot-jr
```

**Option 2:** Install CLI & python bindings in current environment

```bash
pip install git+https://github.com/DarbotLM/darbot-jr.git
jr  # run the CLI
```

**Option 3:** Install from source (developer setup)

```bash
git clone https://github.com/DarbotLM/darbot-jr.git
cd darbot-jr && pip install -e .
jr  # run the CLI
```

Read more in our [documentation](docs/):

* [Quick start guide](docs/quickstart.md)
* [Using the `jr` CLI](docs/usage/jr.md)
* [Global configuration](docs/advanced/global_configuration.md)
* [Yaml configuration files](docs/advanced/yaml_configuration.md)
* [Power up with the cookbook](docs/advanced/cookbook.md)
* [FAQ](docs/faq.md)
* [Contribute!](docs/contributing.md)

## Attribution

If you found this work helpful, please consider citing the [SWE-agent paper](https://arxiv.org/abs/2405.15793) in your work:

```bibtex
@inproceedings{yang2024sweagent,
  title={{SWE}-agent: Agent-Computer Interfaces Enable Automated Software Engineering},
  author={John Yang and Carlos E Jimenez and Alexander Wettig and Kilian Lieret and Shunyu Yao and Karthik R Narasimhan and Ofir Press},
  booktitle={The Thirty-eighth Annual Conference on Neural Information Processing Systems},
  year={2024},
  url={https://arxiv.org/abs/2405.15793}
}
```

Related upstream projects:

<div align="center">
  <a href="https://github.com/SWE-agent/SWE-agent"><img src="https://raw.githubusercontent.com/SWE-agent/swe-agent-media/refs/heads/main/media/logos_banners/sweagent_logo_text_below.svg" alt="SWE-agent" height="120px"></a>
   &nbsp;&nbsp;
  <a href="https://github.com/SWE-agent/SWE-ReX"><img src="https://raw.githubusercontent.com/SWE-agent/swe-agent-media/refs/heads/main/media/logos_banners/swerex_logo_text_below.svg" alt="SWE-ReX" height="120px"></a>
   &nbsp;&nbsp;
  <a href="https://github.com/SWE-bench/SWE-bench"><img src="https://raw.githubusercontent.com/SWE-agent/swe-agent-media/refs/heads/main/media/logos_banners/swebench_logo_text_below.svg" alt="SWE-bench" height="120px"></a>
  &nbsp;&nbsp;
  <a href="https://github.com/SWE-bench/SWE-smith"><img src="https://raw.githubusercontent.com/SWE-agent/swe-agent-media/refs/heads/main/media/logos_banners/swesmith_logo_text_below.svg" alt="SWE-smith" height="120px"></a>
  &nbsp;&nbsp;
  <a href="https://github.com/codeclash-ai/codeclash"><img src="https://raw.githubusercontent.com/SWE-agent/swe-agent-media/refs/heads/main/media/logos_banners/codeclash_logo_text_below.svg" alt="CodeClash" height="120px"></a>
  &nbsp;&nbsp;
  <a href="https://github.com/SWE-bench/sb-cli"><img src="https://raw.githubusercontent.com/SWE-agent/swe-agent-media/refs/heads/main/media/logos_banners/sbcli_logo_text_below.svg" alt="sb-cli" height="120px"></a>
</div>

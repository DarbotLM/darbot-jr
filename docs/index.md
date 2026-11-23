<div align="center">
<img src="assets/darbot-jr-banner.svg" alt="Darbot Jr banner" style="height: 7em"/>

<h1 style="margin-bottom: 1ex;">The 100 line AI agent that's actually useful</h1>

</div>

<div align="center">

<a href="https://github.com/DarbotLM/darbot-jr">
    <img alt="GitHub Release" src="https://img.shields.io/github/v/release/DarbotLM/darbot-jr?style=for-the-badge&logo=github&label=GitHub&labelColor=black&color=green" alt="GitHub Release">
</a>
</div>

!!! warning "This is Darbot Jr v2"

    Read the [migration guide](advanced/v2_migration.md).

In 2024, [SWE-bench](https://swebench.com) & [SWE-agent](https://swe-agent.com) helped kickstart the coding agent revolution.

We now ask: **What if our agent was 100x simpler, and still worked nearly as well?**

`jr` is

- **Widely adopted**: Used by Meta, NVIDIA, Essential AI, IBM, Nebius, Anyscale, Princeton University, Stanford University, and many more.
- **Minimal**: Just [100 lines of python](https://github.com/DarbotLM/darbot-jr/blob/main/src/jrsweagent/agents/default.py) (+100 total for [env](https://github.com/DarbotLM/darbot-jr/blob/main/src/jrsweagent/environments/local.py),
[model](https://github.com/DarbotLM/darbot-jr/blob/main/src/jrsweagent/models/litellm_model.py), [script](https://github.com/DarbotLM/darbot-jr/blob/main/src/jrsweagent/run/hello_world.py)) — no fancy dependencies!
- **Performant:** Scores >74% on the [SWE-bench verified benchmark](https://www.swebench.com/); starts much faster than Claude Code
- **Deployable:** Supports **local environments**, **docker/podman**, **singularity/apptainer**, **bublewrap**, **contree**, and more
- **Compatible:** Supports all models via **litellm**, **openrouter**, **portkey**, and more. Support for `/completion` and `/response` endpoints, interleaved thinking etc.
- Built by the Princeton & Stanford team behind [SWE-bench](https://swebench.com), [SWE-agent](https://swe-agent.com), and more
- **Tested:** [![Codecov](https://img.shields.io/codecov/c/github/DarbotLM/darbot-jr?style=flat-square)](https://codecov.io/gh/DarbotLM/darbot-jr)

??? note "Why use Darbot Jr for research?"

    [SWE-agent](https://swe-agent.com/latest/) jump-started the development of AI agents in 2024. Back then, we placed a lot of emphasis on tools and special interfaces for the agent. However, one year later, a lot of this is not needed at all to build a useful agent!

    In fact, the `jr` agent:

    - **Does not have any tools other than bash** — it doesn't even use the tool-calling interface of the LMs.
      This means that you can run it with literally any model.
      When running in sandboxed environments you also don't need to take care of installing a single package — all it needs is bash.
    - **Has a completely linear history** — every step of the agent just appends to the messages and that's it.
      So there's no difference between the trajectory and the messages that you pass on to the LM.
      Great for debugging & fine-tuning.
    - **Executes actions with `subprocess.run`** — every action is completely independent (as opposed to keeping a stateful shell session running). This makes it trivial to execute the actions in sandboxes (literally just switch out `subprocess.run` with `docker exec`) and to scale up effortlessly.
      Seriously, this is [a big deal](faq.md#why-no-shell-session), trust me.

    This makes it perfect as a baseline system and for a system that puts the language model (rather than the agent scaffold) in the middle of our attention.
    You can see the result on the [SWE-bench (bash only)](https://www.swebench.com/) leaderboard, that evaluates the performance of different LMs with `jr`.

??? note "Why use Darbot Jr as a tool?"

    Some agents are overfitted research artifacts. Others are UI-heavy frontend monsters.

    The `jr` agent wants to be a hackable tool, not a black box.

    - **Simple** enough to understand at a glance
    - **Convenient** enough to use in daily workflows
    - **Flexible** to extend

    Unlike other agents (including our own [swe-agent](https://swe-agent.com/latest/)), it is radically simpler, because it:

    - **Does not have any tools other than bash** — it doesn't even use the tool-calling interface of the LMs.
      Instead of implementing custom tools for every specific thing the agent might want to do, the focus is fully on the LM utilizing the shell to its full potential.
      Want it to do something specific like opening a PR?
      Just tell the LM to figure it out rather than spending time to implement it in the agent.
    - **Executes actions with `subprocess.run`** — every action is completely independent (as opposed to keeping a stateful shell session running).
      This is [a big deal](faq.md#why-no-shell-session) for the stability of the agent, trust me.
    - **Has a completely linear history** — every step of the agent just appends to the messages that are passed to the LM in the next step and that's it.
      This is great for debugging and understanding what the LM is prompted with.

??? note "Should I use Darbot Jr or swe-agent?"

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

<table>
<tr>
<td width="50%">
<a href="usage/jr"><strong>CLI</strong></a> (<code>jr</code>)
</td>
<td>
<a href="usage/swebench/"><strong>Batch inference</strong></a>
</td>
</tr>
<tr>
<td width="50%">
  <div class="gif-container" data-glightbox-disabled>
    <img src="https://github.com/SWE-agent/swe-agent-media/blob/main/media/jr/png/jr.png?raw=true"
         data-gif="https://github.com/SWE-agent/swe-agent-media/blob/main/media/jr/gif/jr.gif?raw=true"
         alt="jr" data-glightbox="false" />
  </div>
</td>
<td>
<div class="gif-container" data-glightbox-disabled>
  <img src="https://github.com/SWE-agent/swe-agent-media/blob/main/media/jr/png/swebench.png?raw=true"
       data-gif="https://github.com/SWE-agent/swe-agent-media/blob/main/media/jr/gif/swebench.gif?raw=true"
       alt="swebench" data-glightbox="false" />
</div>
</td>
</tr>
<tr>
<td>
<a href="usage/inspector/"><strong>Trajectory browser</strong></a>
</td>
<td>
<a href="advanced/cookbook/"><strong>Python bindings</strong></a>
</td>
</tr>
<tr>
<td>
<div class="gif-container" data-glightbox-disabled>
  <img src="https://github.com/SWE-agent/swe-agent-media/blob/main/media/jr/png/inspector.png?raw=true"
       data-gif="https://github.com/SWE-agent/swe-agent-media/blob/main/media/jr/gif/inspector.gif?raw=true"
       alt="inspector" data-glightbox="false" />
</div>
</td>
<td>
<pre><code class="language-python">agent = DefaultAgent(
    LitellmModel(model_name=...),
    LocalEnvironment(),
)
agent.run("Write a sudoku game")</code></pre>
</td>
</tr>
</table>


!!! info "Upgrading to v2?"

    Check out our [v2 migration guide](advanced/v2_migration.md) for all the changes and how to update your code.

## Continue reading:

<div class="grid cards">
  <a href="quickstart/" class="nav-card-link">
    <div class="nav-card">
      <div class="nav-card-header">
        <span class="material-icons nav-card-icon">launch</span>
        <span class="nav-card-title">Installation & Quick Start</span>
      </div>
      <p class="nav-card-description">Get started with Darbot Jr</p>
    </div>
  </a>

  <a href="usage/jr/" class="nav-card-link">
    <div class="nav-card">
      <div class="nav-card-header">
        <span class="material-icons nav-card-icon">flash_on</span>
        <span class="nav-card-title">Usage: Simple UI</span>
      </div>
      <p class="nav-card-description">Learn to use the <code>jr</code> command</p>
    </div>
  </a>

  <a href="faq/" class="nav-card-link">
    <div class="nav-card">
      <div class="nav-card-header">
        <span class="material-icons nav-card-icon">help</span>
        <span class="nav-card-title">FAQ</span>
      </div>
      <p class="nav-card-description">Common questions and answers</p>
    </div>
  </a>

  <a href="advanced/yaml_configuration/" class="nav-card-link">
    <div class="nav-card">
      <div class="nav-card-header">
        <span class="material-icons nav-card-icon">settings</span>
        <span class="nav-card-title">Configuration</span>
      </div>
      <p class="nav-card-description">Setup and customize your agent</p>
    </div>
  </a>

  <a href="advanced/cookbook/" class="nav-card-link">
    <div class="nav-card">
      <div class="nav-card-header">
        <span class="material-icons nav-card-icon">fitness_center</span>
        <span class="nav-card-title">Power up</span>
      </div>
      <p class="nav-card-description">Start hacking the agent!</p>
    </div>
  </a>
</div>

## 📣 New features

Please check the [github release notes](https://github.com/DarbotLM/darbot-jr/releases) for the latest updates.

## 📣 Documentation updates

* Jul 27: More notes on [local models](models/local_models.md)

{% include-markdown "_footer.md" %}

# Installation

Ready to dive in? Let's get you set up!

## Prerequisites

Ensure you have [Python](https://www.python.org/downloads/) *version 3.11* installed.

If you'd like to use this ***as a tool*** and you *don't* need to mess with the `opsbox` code, we recommend that you [install in an isolated environment](#recommended-install-in-an-isolated-environment).
To do that, you'll want to install either [UV](https://docs.astral.sh/uv/) or [pipx](https://pipx.pypa.io/stable/).

If you'd like to ***develop*** for opsbox or want to [install from source](#not-recommended-install-from-source), you will *need* [UV](https://docs.astral.sh/uv/).
It's what we use in this project to manage dependencies.

If you'd like to run ***rego plugins*** *(you probably do)* you'll need to [install a local copy of OPA](#installing-opa-for-rego-compatibility).

## (Recommended) Install in an isolated environment

If you are primarily using opsbox as a tool, we recommend installing it in it's own *isolated environment*.

Normally, when you install through `pip`, you install into the **system-wide** package directory, which can lead to havoc, *especially* on distros reliant on python.

Installing in our own environment allows us to avoid:

- Version conflicts in system-wide dependencies
- Polluting global namespace with our package and all of our plugins
- Breaking systems reliant on a system python

To manage these isolated tool environments for this project, you can use either [UV](https://docs.astral.sh/uv/) or [pipx](https://pipx.pypa.io/stable/).

!!! note "Which One?"

    UV is a tool and project environment manager, while pipx is simply a tool environment manager.

    If you ever want to develop opsbox in the future, it might be prudent to install UV, as that's what we use to manage packages.

    However, if you only want to use packaged plugins, either or will work.

### UV as tool manager

#### Installation

To install just the opsbox tool with UV acting as the tool environment manager, you'll want to run:

```bash
uv tool install opsbox
```

In UV you can add packages during the install process using the `--with` flag.

```bash
uv tool install --with "opsbox-cli-output" "opsbox[aws]" # installing the AWS extras group, alongside the CLI output
```

To add new packages to the environment after installing, simply *rerun the command with all desired packages in the `--with` flag.*

!!! warning "UV and caching"

    Sometimes, you might run into issues where UV downloads the *wrong version* or *can't find the package requested*.
    
    To fix this, it's helpful to clear the UV cache through the following command:
    ```bash
    uv cache clean
    ```
    and retry the install process.

#### Execution

To execute the opsbox binary in UV, simply run either:

```bash
uv tool run opsbox ...
```

or

```bash
uvx opsbox ...
```

!!! warning "UV & Tool Environments"

    Virtual environment plugin detection *will not work* if you use the `--with` flag with anything other than `uv tool install`. This is because the execution-time `--with` flag acts differently, creating a temporary virtual environment on execute time.

    To add a package to the tool's virtual environment, you'll need to run the entire install command again with the proper packages in the `--with` flag.

### pipx as tool manager

#### Installation

To install just the opsbox tool with pipx acting as the tool environment manager, you'll want to run:

```bash
pipx install opsbox
```

In pipx you can add packages after the install process using the `inject` flag.

```bash
pipx inject opsbox opsbox-cli-output # installing the CLI output into the opsbox venv
```

!!! tip
    
    You can replace every mention of the bare `opsbox` package with the `"opsbox[aws]"` extras group to install AWS plugins.

#### Execution

To execute the opsbox binary in pipx, you'll need to add it to your path.

To do this, run:

```bash
pipx ensurepath
```

Then, you can access it by calling `opsbox` by name in your shell.

## (Not Recommended) Install from source

If you'd like to develop on top of opsbox, or just want a local copy of it to see what's going on as you run it, you can install from our git repository.

You will *need* [UV](https://docs.astral.sh/uv/) to continue, as that's what manages our dependencies.

!!! warning "Read this first"

    While you *can* install this from source if you want to use this as a tool, we don't recommend it.

    If you want to use pre-packaged plugins with this style of install, you'll have to install them into the *same virtual environment running opsbox* or point to a plugin directory, which means ***you'll have to install all plugin dependencies into the main virtual environment***.

    This means a lot more manual dependency management and directory making, which is not ideal for users that aren't looking for the development benefits this install method provides.

### Installation
First, start by cloning our github repo.

```bash
git clone https://github.com/sudoersllc/opsbox-core.git
```

Next, we'll want to sync our python dependencies through UV by running the following *at the root of the repo*:
```bash
uv sync
```

This will create a `.venv` folder for our virtual environment, and download our dependencies.

!!! note "Python Version Issues While Syncing? Read This"

    If you run into python versioning issues when running these commands on your copy of the repo, you might be able to install and pin the projects python version to our required 3.11.

    In your clone, run the following:
    ```bash
    uv python install 3.11
    ```

    Then, delete the `.python-version` file in the repo and run:
    ```bash
    uv python pin 3.11
    ```

    This should repin your python version to the UV-managed python interpreter.

### Execution
To execute from this style of install, you'll want to run the `opsbox/main.py` file in your python virtual environment.

You can do this by either activating your .venv and running it using python, or you could do it using UV in the following way from the *root of your repo*:
```bash
uv run ./opsbox/main.py ...
```

This will run that file in the projects .venv, and will be ***the main thing you run instead of `opsbox` wherever you see it being mentioned***.

## Installing OPA for Rego Compatibility
Our program comes with compatibility for the Rego language, which is used to filter out data from various providers and return metrics for various services.

***Hint: You probably want to use it if you're running any AWS plugins!***

The first thing to do is to download the OPA binary to a safe space, following [these instructions](https://www.openpolicyagent.org/docs/latest/#running-opa).

After you have downloaded and are able to run the OPA binary, add it to your path.

!!! tip "Adding to system PATH"

    **Linux/macOS**

    1. **Open your shell's config file:** This is usually `~/.bashrc` (Bash), `~/.zshrc` (Zsh), or `~/.config/fish/config.fish` (Fish).

    2. **Add the directory:** Find the `PATH` line. If it's missing, add this line at the end, replacing `/path/to/your/opa/directory` with the actual directory:

    ```bash
    export PATH=$PATH:/path/to/your/opa/directory
    ```

    3. **Save and apply:** Save the file, then run `source ~/.bashrc` (or your file's name) in your terminal, or just restart your terminal.

    **Windows**

    1. **Search for "environment variables":**  Open "Edit the system environment variables".

    2. **Edit PATH:** Click "Environment Variables...", then edit the "Path" variable (either User or System).  System changes need admin rights.

    3. **Add the directory:** Click "New" and enter the full path to the directory. Example: `C:\path\to\your\opa\directory`

    4. **Save and restart:** Click "OK" on all windows. Open a *new* command prompt or PowerShell window.

    **Important Notes:**

    * **Executable Name:** Make sure OPA has the right name and extension (e.g., `.exe` on Windows).
    * **Permissions (Linux/macOS):** Use `chmod +x /path/to/your/opa` to give your OPA execute permissions.

***Once added to your path, rego plugins should be able to find and detect your OPA install.***

!!! note "Using Servers"

    While unlikely, you may have an existing OPA server you want to use.

    Simply pass the url base in the `opa_url` parameter, and we'll take care of the rest.

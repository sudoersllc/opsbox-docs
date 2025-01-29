# Running

Depending on how you installed opsbox, there are a variety of ways to execute it.

## If you have a tool install
If you installed through the `uv tool` pipeline as specified [here](./installation.md#uv-as-tool-manager), you'll want to run opsbox like so:
```bash
uvx opsbox ... # uvx is an alias of uv tool run
```

If you installed through the `pipx install` pipeline as specified [here](./installation.md#pipx-as-tool-manager),
you *should* have `opsbox` in your path.

```bash
opsbox ...
```

Plugins in your tool environment should be automatically found and availbale for use.

If not, refer back to the [installation instructions](./installation.md#recommended-install-in-an-isolated-environment) and find the instructions for your chosen tool, which will tell you how to install packages in your tool environment.

## If you have a cloned repo isntall
If you followed the instructions [here](./installation.md#not-recommended-install-from-source), you should have a `opsbox/main.py` file that you will run in your created virtual environment.

You can run in-project using UV like so:
```bash
uv run ./opsbox/main.py ... 
```

Plugins in the *projects* virtual environment will be automatically found, and local plugins can be pointed to by following the instructions [here](./configuration.md#working-with-local-plugins)

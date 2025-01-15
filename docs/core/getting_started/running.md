### Running OpsBox
To run Opsbox from a *venv*, simply call the python module `opsbox`.

With uv, this looks like `uv run opsbox ...`
Without, it looks like `python -m opsbox ...`

When run *outside of a venv*, use the `main.py` script found in `core`.

An example call to opsbox must at least include the `modules` argument, like so:

```bash
uv run opsbox --modules your_input-your_optional_assistant-your_output --opa_url http://your-opa-url 
```

A recommended command to start is stray_ebs

```bash
uv run opsbox --modules stray_ebs-cli_out --opa_url http://localhost:8181/ --aws_access_key_id {YOUR_ACCESS_KEY_ID} --aws_secret_access_key {YOUR_SECRET_ACCESS_KEY} --aws_region us-east-1
```

or, if not using UV:

```bash
python -m opsbox --modules your_input-your_optional_assistant-your_output --opa_url http://your-opa-url 
```

```bash
python -m opsbox --modules stray_ebs-cli_out --opa_url http://localhost:8181/ --aws_access_key_id {YOUR_ACCESS_KEY_ID} --aws_secret_access_key {YOUR_SECRET_ACCESS_KEY} --aws_region us-east-1
```
Make sure you have any of the prerequisite packages for the plugins you want to use!

### Configuration

#### Modules
Opsbox uses a series of modules specified at runtime to analyze different environments.
These modules *have their own* arguments and required settings that will be looked for upon startup, and *must* specified as a pipeline in the following format:

```
input_1,input_2-assistant_1-assistant_2-output_1,output_2
```

Where:

    - The first arguments are the input plugins we want to use, seperated with a comma
    - The middle arguments are the assistants we want to use, seperated by a hyphen
    - The last arguments are the outputs we want to use, sepereated by a comma

For instance, if we wanted to check for stray EBS volumes and output the results to the main after running through a cost assistant, we would need to use the following pipeline:

```
stray_ebs-cost_savings-main_out
```

Of course, the assistant and the module the check uses will require additional parameters, such as an OpenAI key. Keep reading to figure out how to set these up.

#### Local plugin development
To develop and use plugins locally, simply point opsbox to the directory where your plugins are located using the `plugin_dir` configuration argument.

As long as the plugins you specify are found in this directory, opsbox will use them instead of the virtual environment-installed packages.

```uv run opsbox ... --plugin_dir ./plugins```


#### Open Policy Agent (Rego Only)
Opsbox uses OPA to upload and execute rego checks.

Open Policy Agent (OPA) is an open-source policy engine that allows organizations to enforce policies as code across various environments. Its policy language, Rego, enables users to define rules that govern the behavior of systems and applications.

We use rego check plugins as ways to get information on various systems and see how they function

Before running any rego-based input plugins, ensure you have access to an OPA (Open Policy Agent) instance. For local testing, you can run a test OPA instance as follows:

You can run a local test OPA instance by following the steps in [installation](installation.md) and running the following command:

```bash
    docker run -d -p 8181:8181 opa-policy
```


To do this, one required configuration parameters is needed:

- `opa_url` : URL to upload rego policies to

If you created a docker container in the last step, you should be able to access the local OPA

#### Specifying configuration
Configuration can be specified with each required item being specified in a credential file located in the home directory, a command-line argument, an enviornment variable, or in a json configuration file.

##### Configration File
You can specify most or all of the arguments as a json dictionary stored in `~/.opsbox.json`, similar to the AWS main.

##### Custom Configuration File Path
To use a configuration file in another part, simply use the `--config <filepath>` argument.

##### Command-line Arguments
You can specify all the arguments as double-dashed arguments after the `--modules` argument.

##### Resolution order
Configuration will be looked for based on what modules are specified. Each argument will be resolved in the following order:

1. If `--config` is specified, look in that file first.
2. Then, if it is in the home configuration file, load that.
2. Then, if it is in the command line arguments, load that.
3. Finally, if it is nowhere else, enviroment variables are used.


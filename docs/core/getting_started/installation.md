# Installation

Ready to dive in? Let's get you set up!

## Prerequisites
Ensure you have the following installed on your machine:

- [Python](https://www.python.org/downloads/) == 3.11
- [UV](https://docs.astral.sh/uv/) for dependency management

**Installing Python:**

Visit the [official Python website](https://www.python.org/downloads/) and download the latest version of Python for your operating system.

**Installing UV**

UV can be installed in various ways. The recommended method is to use the installer script:


*For Linux/Mac*

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

*For Windows*
```powershell
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
```
## Installing Opsbox Through PyPI

Simply run `pip install opsbox` to install the minimal set of opsbox tools.

If using UV, initilize your project using `uv init`.

then `uv add opsbox`

*Note: If you want to install AWS plugins, use the aws extras group, `opsbox[aws]`*

## Installing Opsbox Through Github

1. **Clone the Repository**

    ```bash
    git clone https://github.com/sudoersllc/Opsbox.git
    cd Opsbox
    ```

2. **Install with uv**

    We use [`uv`] for managing dependencies. If you don't have it installed, you can get it via pip:

    ```bash
    pip install uv
    ```



    Now, let's install Opsbox:

    ```bash
    uv sync
    ```

    This command will install all required dependencies specified in `pyproject.toml`.

## Using Rego Plugins
Open Policy Agent (OPA) is an open-source policy engine that enables organizations to implement policy as code across diverse environments. Its policy language, Rego, allows users to define rules that dictate system and application behavior.

We use rego code to gather details about connected systems, alongside an Open Policy Agent (OPA) server, then format it for consumption by a language model.

### Create a OPA Policy docker image
To run OpsBox with rego plugins, you'll need an OPA server. This is because OpsBox uses OPA to enforce policies on all resources that are being managed.

if you don't have OPA installed on your machine, or you dont have a running OPA instance, you can create a docker image for OPA.

Start by [installing docker](https://docs.docker.com/engine/install/).

Create a dockerfile and add the following code:
```docker
    # Use the official OPA image
    FROM openpolicyagent/opa:latest

    # Expose OPA's default port
    EXPOSE 8181

    # Run OPA with the specified policy file
    CMD ["run", "--server", "--addr", "0.0.0.0:8181"]
```


Navigate to the directory and Build the Docker image:
```bash
    docker build -t opa-server .
```
or you can also follow the offical OPA documentation to create the engine: [OPA Documentation](https://www.openpolicyagent.org/docs/latest/)

Finally, run the OPA server as follows:
```bash
    docker run -d -p 8181:8181 --name opa-server opa-server
```

Or the docker image can be found here
(https://hub.docker.com/r/openpolicyagent/opa/)

```bash
    docker run -d -p 8181:8181 --name opa openpolicyagent/opa run --server --addr=0.0.0.0:8181*
```
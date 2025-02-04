
# Creating Rego Check Plugins for Opsbox

Rego check plugins are vital for gathering data from a provider plugin, applying a defined policy, and formatting the raw result into a readable format. Let's explore how to create one!

## Before You Start

If you haven't read the **Plugin Basics** and **Providers** documents, please take a moment to do so. They provide essential information for successfully gathering data, including:

- Setting up a proper **hookimpl marker** to register hook implementations
- Gathering required arguments for various plugins
- Information on setting up your plugin info document
- Details on providers to help you get started

While Rego checks don't typically use `activate` or configuration models, feel free to include them if needed!

## Requirements

Rego check plugins require three things:

1. **A manifest file** detailing the location of the Rego file, the provider to gather data from, and the meaning of the check results.
2. **A Rego file** with a policy that returns meaningful results from the provider data.
3. **A Python class** with a hook implementation that converts the Rego check results into a human-readable format.

## Manifest File

In addition to the `[info]` section of your manifest TOML file *(see [development basics](./development_basics.md/#define-plugin-info-toml-file)), you also need to include a `[rego]` header:

```toml
[info]
name = "Plugin Name"
module = "plugin_module"
class_name = "PluginClassInModule"
type = "rego"
uses = ["rego"]

[rego]
rego_file = "path/to/regofile.rego"
description = "Description of policy results"
```

- **type** must be `"rego"`.
- **uses** list must contain `"rego"`.
- **rego_file** points to the rego file.
- **description** describes the rego check itself.

These fields tell Opsbox what it needs to know to accurately manage Rego checks.

## Defining Hook Implementations

Rego checks implement the hooks from `RegoSpec`. 

The key method to implement is `report_findings(self, data: "Result") -> "Result"`. This hook takes in a Result with rego-processed details from the rego check specified and formats it into an LLM-usable text format, returning the result.

If you want to have user-settable parameters, you must also use the `inject_data(self, data: "Result") -> "Result"` method. This method will intercept data from the provider and modify it's `Result` object.

!!! note 

    More info about the result object can be found [here](./development_basics.md#how-to-use-the-result-model-in-your-plugin).

## What to include in your pyproject file
One key thing to note for building *installable distributions** is the inclusion of rego files in your metadata, in addition to adding an entrypoint in your `pyproject.toml` file to the module and class of your plugin. [(*see development basics for more!*)](./development_basics.md/#step-1-add-entrypoint)

Change the following section in your pyproject.toml file to this to include both your manifest and rego files:
```toml
[tool.setuptools.package-data]
"plugin_name" = ["manifest.toml", "*.rego"] # include "*.rego" if you are making a rego plugin.
```

## Example non-parameterized rego code
In order to get a feel of what this is like, let's take a look at our route53 check, `empty_zones`.

### Input Data
This check uses the route53 provider, which generates input data that looks like this:

```json
{
    "hosted_zones": [
        {
            "id": "/hostedzone/7ZSTMBU7PTBT23B",
            "name": "example2.com.",
            "record_count": 0,
            "private_zone": false
        },
        ...
    ],
    "records": [
        {
            "zone_id": "/hostedzone/7Z4TMBU7PTBT23B",
            "name": "api.example.com.",
            "type": "CNAME",
            "ttl": 300,
            "records": [
                {
                    "Value": "www.example.com."
                }
            ]
        },
        ...
    ],
    "health_checks": [
        {
            "id": "ee156676-1aef-4696-94c6-f85ff628abae",
            "type": "HTTP",
            "ip_address": "192.0.2.1",
            "port": 80,
            "resource_path": "/",
            "failure_threshold": 3
        }
    ]
}
```

!!! note

    It is *very important* to look at the results from the provider provided by your environment to develop the rego code you rely on. 
    
    Sometimes, you might have different parameters set up than our testing data.


### Rego Policy
Here's what the rego policy for this check looks like:

```rego
package aws_rego.r53_checks.empty_zones.empty_zones

import rego.v1

# Find hosted zones with no records
empty_hosted_zones contains zone if {
	some zone in input.hosted_zones
	not records_exist_for_zone(zone.id)
}

# Check if records exist for a given zone
records_exist_for_zone(zone_id) if {
	some record in input.records
	record.zone_id == zone_id
}

allow if {
	some zone in input.hosted_zones
	not records_exist_for_zone(zone.id)
}

# Generate details for empty hosted zones
details := {"empty_hosted_zones": [zone | zone := empty_hosted_zones[_]]}
```

We can see that we:

- Use `input.<key>` to gather information retreived from the provider
- Return a `details` dictionary that contains the results of the rego evaluation.

!!! note "Designing rego code"

    It is important to note that there are a series of "best practices" for rego.

    These can mostly be found by simply using [Regal](https://www.openpolicyagent.org/integrations/regal/) to lint your rego code. 
    
    *Be careful what you ignore, some versions of OPA might be more or less strict on conformity to guidelines!*

### Example output data
When we take our rego check and run it straight against our testing data, we get this:

```json
{
    "details": {
        "empty_hosted_zones": [
            {
                "id": "/hostedzone/7ZSTMBU7PTBT23B",
                "name": "example2.com.",
                "private_zone": false,
                "record_count": 0
            }
        ]
    }
}
```
This is a dictionary of empty zones, as computed on *provider data* with a *rego evaluation*.

This is the data we will use to generate a nice, formatted version of our result, and it what normally goes into our `details` attribute (minus the `details` key, of course).

### Example formatting
Here is how we format the rego check's result into a readable format:

```python
class EmptyZones:
    """Plugin for identifying Route 53 hosted zones with no DNS records."""

    def report_findings(self, data: "Result"):
        """Report the findings of the plugin.
        Attributes:
            data (Result): The result of the check.
        Returns:
            Result: The result containing the findings.
        """
        details = data.details
        logger.info(f"Details: {details}")

        # Directly get empty hosted zones from the Rego result
        empty_zones = details.get("empty_hosted_zones", [])
        
        # Format the empty zones list into YAML for better readability
        try:
            empty_zones_yaml = yaml.dump(empty_zones, default_flow_style=False)
        except Exception as e:
            logger.error(f"Error formatting empty hosted zones: {e}")
            empty_zones_yaml = ""

        # Template for the output message
        template = """The following Route 53 hosted zones have no DNS records:
        
{empty_zones}"""
        logger.info(empty_zones_yaml)
        
        # Generate the result with formatted output
        if empty_zones:
            return Result(
                relates_to="r53",
                result_name="route53_empty_zones",
                result_description="Route 53 Hosted Zones with No Records",
                details=data.details,
                formatted=template.format(empty_zones=empty_zones_yaml),
            )
        else:
            return Result(
                relates_to="r53",
                result_name="route53_empty_zones",
                result_description="Route 53 Hosted Zones with No Records",
                details=data.details,
                formatted="No empty Route 53 hosted zones found.",
            )
```

You can see we:

- Take in a rego check's `Result` object and mainly use it's `details` attribute to format and build a result
- Returned a new `Result` object with the formatted template.

From here, your check is complete!

If you want to package it for wider distribution from PyPI, start with reading [this portion of development basics](./development_basics.md/#packaging-your-plugin-for-distribution), then read [this portion again](#what-to-include-in-your-pyproject-file) after initializing your project in the format from development basics.

## Parameterizing your rego code (Advanceed, Optional)
You can add parameters to your rego code by implementing the `inject_data(self, data: "Result") -> "Result"`
method.

What this method does is intercept data *after* the provider but *before* it is sent to the rego check.

The sole argument to this check is the provider data `Result` object, and the user modifies the `Result.details` attribute of this object to add parameters accessible inside the rego code by using the `input.<key>` syntax, like all other access of input data.

This allows for a bunch of fun, interesting dynamic attributes to be added to your rego checks to make them more powerful.

One of the more common things to do with this input injection method is to ***parameterize your rego functions*** by injecting user-specified arguments into the `input` object.

### Defining the arguments
First thing to do when needing accessible arguments is to add a config model that's returned from `grab_config`, along side a proper setter of `set_data`.

Let's take a look at another plugin, this time the `overdue_api_keys` from the AWS IAM checks plugin, to see how it does it:

```python
class OverdueAPIKeysConfig(BaseModel):
    iam_overdue_key_date_threshold: Annotated[
        datetime,
        Field(
            default=(datetime.now() - timedelta(days=90)),
            description="How long ago a key was last used for it to be considered overdue. Default is 90 days.",
        ),
    ]

class OverdueAPIKeysIAM:
    """Plugin for identifying IAM keys that are overdue for rotation."""

    @hookimpl
    def grab_config(self) -> type[BaseModel]:
        """Return the plugin's configuration pydantic model.
        These should be things your plugin needs/wants to function."""
        return OverdueAPIKeysConfig

    @hookimpl
    def set_data(self, model: type[BaseModel]) -> None:
        """Set the data for the plugin based on the model.

        Args:
            model (BaseModel): The model containing the data for the plugin."""
        self.conf = model.model_dump()
    ...
```

This is very much like any other plugin in how it defines it's data.

!!! tip

    For more info on how to specify a configuration for a plugin that's stored, check out [here](./development_basics.md/#define-configuration-optional)

### Inject into input
Next, let's see it's `inject_data` function:

```py
class OverdueAPIKeysIAM:
    ...

    @hookimpl
    def inject_data(self, data: "Result") -> "Result":
        """Inject data into the plugin.

        Args:
            data (Result): The data to inject into the plugin.

        Returns:
            Result: The data with the injected values.
        """
        timestamp = int(self.conf["iam_overdue_key_date_threshold"].timestamp() * 1e9)
        data.details["input"]["iam_overdue_key_date_threshold"] = timestamp
        return data
```

You can see we:

- Grab the argument and format it for input
- Inject this data into the `data.details["input"]` dictionary to be recognized as an input

!!! tip

    Normally for data injection you want to inject in the same` data.details["input"]` dictionary. This allows you to specify `input.<key>` in the rego file, which is the default way to access this data in OPA.

This is the basic formula you'll want to follow for writing parameterized rego checks.

---

By following these guidelines, you can create effective Rego check plugins for Opsbox, making your cloud infrastructure management more insightful and automated. Happy coding! 🚀

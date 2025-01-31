# Configuration
Before you can run opsbox, you must know how to configure it.

Opsbox runs on a flexible, modular arguments-based configuration system.

Each and every plugin can specify desired parameters, needed information, and other details that it wants from the user, which the user can set from a file, command line, or environment variable.

## Where to Specify Configuration
Argument values can be specified in 4 places:

- The default arguments file (`~/.opsbox.json`)
- A file specified with the `--config <path>` flag
- Double-dashed command line arguments and flags
- Environment variables.

***This is also the resolution order!***

Both the default and specified configuration files consist of a **JSON dictionary**, where each *key* corresponds to an *argument name* and each *value* is the *value you want that argument to have*.

## Specifying your pipeline
This is an argument that is core to how opsbox functions and works.
It is *highly recommended* to take a look over this next section.

Opsbox uses a series of plugins specified at runtime to analyze different environments.

These plugins *have their own* arguments and required settings that will be looked for upon startup, and *must* specified as a pipeline in the following format:

```
input_1,input_2-assistant_1-assistant_2-output_1,output_2
```

Where:

- The first arguments are the input plugins we want to use, seperated with a comma
- The middle arguments are the assistants we want to use, seperated by a hyphen
- The last arguments are the outputs we want to use, sepereated by a comma

For instance, if we wanted to get data related to AWS EBS volumes that have gone astray, we can use the `stray_ebs` plugin from our plugins repo and specify a pipeline like so:

```
stray_ebs-cost_savings-cli_out
```

In this pipeline:

- We take `stray_ebs` as our input.
- `cost_savings` will work on the data from stray_ebs and format it in it's own way (providing cost savings recommendations)
- `cli_out` will handle the formatted output of `cost_savings` and display it to the user on the cli.


!!! note

    Keep in mind plugins all have their own parameters they look for!

## Logging
Opsbox provides a lot of customization over it's logging practices.

There are 4 configuration parameters that help you see what you want to see:

- `--log_level`, which specifies the minimum level of logs you want to see.
    Must be one of "TRACE", "DEBUG", "INFO", "WARNING", "ERROR", and "CRITICAL". 
- `--log_file`, which specifies a path to a log file you want to output to.
- `--init_debug`, which allows you to see traces from the *very beginning* of our program's execution.
    Useful mostly for people developing these parts of opsbox.
- `--verbose`, which allows you to see the data that flows in certain parts of the application on the CLI.

By default, we output to `stdout`, and we specify the "INFO" logging level.

## Getting Help
Opsbox has a colorful help system that can lend a helping hand.

To access ***general, application wide parameters and help***, run `opsbox --help` *without* any modules specified.

If you'd like to see the ***arguments for a specific pipeline***, run `opsbox --help` *with* the pipeline you want specified.

If you'd like to *see all plugins from the help screen*, add the `--see_all` argument.

## Working with local plugins
When developing plugins, you will want to point to the directory in which they can be found.

This can be done using the `--plugin_dir` argument, which should point to a directory that contains a plugin in its or its children's subdirectories.

!!! warning "Buyer Beware"

    When specifying this argument, ***you will lose access to plugins stored in your virtual environment.***

    In addition, this argument requires that ***all plugin dependencies be installed in your executing virtual environment***.


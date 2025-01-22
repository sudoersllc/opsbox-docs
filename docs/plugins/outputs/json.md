# TextFileOutput Plugin

## Overview

The JSONFileOutput Plugin writes the results of checks to json files, allowing for easy storage and review of the output data.

### Commands to install the plugin
to install the plugin use the following command
```bash
uv add opsbox-json-file-output
```

## Key Features

- **File Output**: Writes results to json files.
- **Customizable Output Folder**: Allows specifying the folder where the results will be saved.
- **Detailed Logging**: Provides detailed logs of the results.

## Configuration Parameters

### Text File Configuration

- **output_folder**: The folder to output the results to (default: `./findings/`).

## Example Configuration

```yaml
output_folder: ./findings/
```
# TextFileOutput Plugin

## Overview

The TextFileOutput Plugin writes the results of checks to text files, allowing for easy storage and review of the output data.


*This output plugin can be used by adding `text_out` to your pipeline.*

!!! note "Installation Package Name"

    `opsbox-text-file-output` is the name of this package.

    To use it, add `opsbox-text-file-output` to your project.


## Key Features

- **File Output**: Writes results to text files.
- **Customizable Output Folder**: Allows specifying the folder where the results will be saved.
- **Detailed Logging**: Provides detailed logs of the results.

## Configuration Parameters

| Parameter      | Type    | Description                              | Required | Default       |
|----------------|---------|------------------------------------------|----------|---------------|
| output_folder  | str\|None | The folder to output the results to.     | No       | ./findings/   |
# Contributing to Opsbox

Thank you for your interest in contributing to Opsbox! 

We welcome contributions in the form of bug reports, feature requests, documentation improvements, new rego checks, and code changes. To ensure a smooth and efficient collaboration process, please follow these rules and guidelines.

## Code of Conduct
***By participating in the Opsbox project, you agree to abide by the following guidelines:***

1. **Respectful Interaction**: Treat all participants with respect. Consider different viewpoints and experiences.
2. **Inclusivity**: Promote a diverse and inclusive environment.
3. **Effective Communication**: Use clear and constructive language. Be open to feedback and collaborate effectively.
4. **Issue Reporting**: Report any unacceptable behavior to the project maintainers.

## Getting started
Opsbox uses [Git](https://git-scm.com/) and [GitHub](https://github.com/) to manage our repository.

We also use [UV](https://docs.astral.sh/uv/) to manage the project.

To get started, 

1. Clone to your local machine:
    ```bash
    git clone https://github.com/sudoersllc/opsbox-core.git
    cd opsbox-core
    ```
2. Install UV for dependency management
3. Sync the project dependencies:
    ```bash
    uv sync
    ```
4. Install precommit hooks:
    ```bash
    uv run pre-commit install
    ```

After this, you should be free to start development!
Make a new branch according to our [branching standards](git_management.md), and start coding according to our [style guide](style_guide.md). *(Don't worry, they aren't too long)*




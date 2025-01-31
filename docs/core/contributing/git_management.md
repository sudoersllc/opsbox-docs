# Git Management
Opsbox has a series of guidelines and best practices when making git branches that helps us keep our code more organized.

To get started and download the repository, follow the instructions [here](index.md#getting-started).

## Branching Strategy
A good branch should be:

- **Atomic** : Branches should focus on *one thing* and *one thing only!* 
    Don't try to do too much in a branch, as this leads to branch muddying and hidden changes that aren't well known propogating through the codebase.
- **Self-Contained** : Branches shouldn't *rely on other branches*!
    If a branch on one of our repos relies on the merging of another branch in order to make the code run, you're doing it wrong. This one leads to wreathes of git commits instead of nice little branching trees, which complicates looking at the git history.
- **Encompassing** : Branches should *completely encompass their feature*!
    This essentially means that we'd rather have one branch for a feature that's really good rather than 18 branches for the same feature that all tie into each other. This keeps code & git history cleaner than it would otherwise be.

When working in the opsbox repo,

- Create a new branch for each task you work on based on `dev`. This helps in managing and reviewing changes effectively.
- Branch names should be descriptive and follow the convention: `feature/your-feature-name`, `fix/your-bugfix-name`,`infra/hosting-related-change`, etc.

## Precommit Hooks
We use precommit hooks to ensure code quality and consistency. Make sure to install and use them:
```bash
uv run pre-commit install
```
These hooks will automatically run checks and formatting tools before you commit changes.

## Testing your code
`opsbox-core` comes with complete support for the pytest testing environment. For more information on how to write tests using pytest, refer to the [pytest documentation](https://docs.pytest.org/en/stable/).

Additionally, you can find examples and best practices for writing tests in our [testing guide](../testing/testing.md).

When you are ready to test, simply run:
```bash
uv run pytest . # runs pytest at the root dir of the project
```

A nice report should be displayed telling you where you're passing and failing tests.

!!! tip

    Sometimes, you need a little more info on why a test failed.

    In these cases, it's helpful to add the `-s` flag to pytest, which will increase verbosity.

## Formatting code
We use [ruff](https://github.com/charliermarsh/ruff) for formatting and linting. 
Make sure to run `ruff` before submitting your changes.
```bash
uv run ruff check . # for linting
uv run ruff format . # for formatting
```

!!! tip

    You can add the `--fix` flag to your ruff command and it will try and fix linting issues for you!

## Submitting Changes

1. Ensure your code follows the coding standards mentioned [here](style_guide.md).
2. Run all tests to make sure nothing is broken.
3. Lint and check your code with ruff.
3. Commit your changes with a clear and concise commit message:
   ```bash
   git add .
   git commit -m "Add feature/fix for ..."
   ```
4. Push your branch to GitHub:
   ```bash
   git push origin feature/your-feature-name
   ```
5. Open a pull request on GitHub and describe your changes in detail.

We look forward to seeing your contributions!
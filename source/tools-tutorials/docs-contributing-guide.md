# Docs Contributing Guide

Thank you for your interest in contributing to the Rigs of Rods project documentation. This guide will walk you through the process of setting up your environment, making changes, and submitting your contributions. The documentation is built using MkDocs with the Material for MkDocs theme and deployed directly to GitHub Pages.

??? note "Make Quick Edits with the ":material-file-document-edit-outline:" Icon"
    Every page has a ":material-file-document-edit-outline:" icon in the top-right corner. Clicking this icon will take you directly to the source file on GitHub, where you can make edits and propose changes without needing to clone the repository locally. This comes in handy for small fixes like typos, broken links, or minor clarifications.

## Prerequisites

Before you start, ensure you have the following installed:

* **[git](https://git-scm.com/downloads)**: To clone the repository and push your changes.
* **[Python 3.9+](https://www.python.org/downloads/)**: MkDocs is a Python-based tool.
* **pip**: Python package manager, which is usually bundled with Python itself.

You can alternatively use something like [GitHub Desktop](https://github.com/apps/desktop) in place of using git itself.

## Setting Up Your Environment

1. Fork the Repository:
    * Fork the repository on GitHub to your own personal GitHub account.
2. Clone your Fork:
    ```bash
    $ git clone https://github.com/<YOUR_USERNAME>/docs.rigsofrods.org ror-docs
    $ cd ror-docs
    ```
3. Set Up a Virtual Environment (optional, but recommended):
    ```bash
    $ python -m venv venv
    $ source venv/bin/activate # On Windows, use `venv/Scripts/activate`
    ```
4. Install Dependencies:
    ```bash
    pip install -r requirements.txt
    ```

## Making Changes

1. Create a New Branch:
    ```bash
    $ git checkout -b my-cool-change
    ```
2. Make Your Changes:
    * The documentation is written in Markdown (`.md`) and located in the `source/` directory.
3. Update the Navigation:
    * Open `mkdocs.yml` at the root directory.
    * Add the new page to the `nav:` section, for example:
    ```yaml
    nav:
        - My new page: tools-tutorials/my-new-page.md
    ```

## Previewing Your Changes

1. Run the MkDocs Development Server:
    ```bash
    $ mkdocs serve
    ```
    * This will start a local server at `http://127.0.0.1:8000/` where you can preview your changes in real-time.
2. Check for Errors:
    * Ensure there are no build errors or broken links. MkDocs will display errors in the terminal if any exist.

## Submitting Your Contributions

1. Commit Your Changes:
    ```bash
    $ git add .
    $ git commit -m "Your descriptive commit message"
    ```
2. Push to Your Fork:
    ```bash
    git push
    ```
3. Create a Pull Request (PR):
    * Go to your fork on GitHub and click "Compare & Pull Request."
    * Write a clear title and description for your PR, explaining the changes you made.
    * Submit the PR and wait for feedback from the maintainers.

## Style Guide

To maintain consistency across the documentation, please follow these guidelines:

1. Markdown Formatting:
    * Use headings (`#`, `##`, `###`) to structure your content.
    * Use fenced code blocks for code snippets:
    ```markdown
    ```python
    print("Hello world")
    ```
2. Language and Tone
    * Use clear, concise, and friendly language.
    * Write in an active voice whenever possible.
3. Admonitions:
    * Use Material for MkDocs admonitions to highlight important information:
    ```markdown
    !!! note
        This is a note.
    ```
4. Links:
    * Use relative links for internal documentation pages.
    * Use descriptive anchor text for external links.

## Code of Conduct

By contributing, you agree to follow our [Contributor Code of Conduct](../rules/contributor-code-of-conduct.md). Please be respectful and inclusive in all interactions.

Finally, thank you for contributing to the Rigs of Rods project and community! Your efforts will help make the project better for everyone.
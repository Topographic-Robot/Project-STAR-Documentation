Line Endings
============

In this project, **Unix-style line endings** (`LF`, represented as ``\n``) are mandatory across all files. This ensures consistency, particularly when working on cross-platform projects where differences in line endings can cause unnecessary diffs or issues in version control.

Guidelines
----------

- **Always use Unix-style (`LF`) endings**: Ensure that every file in the project, whether it’s source code, header files, scripts, or configuration files, uses Unix-style line endings.

- **Avoid Windows-style (`CRLF`) endings**: Windows uses `CRLF` (``\r\n``) line endings, which should be avoided to prevent inconsistencies. Many version control systems and code editors can introduce unwanted `CRLF` line endings, so make sure to configure your tools appropriately.

- **Editor Configuration**: Set your text editor or IDE to automatically use Unix-style line endings for all files in the project. In most editors, this can be done by adjusting the settings:

  - **VS Code**: Ensure `"files.eol": "\n"` is set in your settings.

  - **Vim/Neovim**: Use `set fileformat=unix`.

  - **Sublime Text**: Enable ``\n`` in the line endings preferences.

  - **Git**: Set the global config with `git config --global core.autocrlf input` to ensure Git handles line endings correctly.

Checking for Line Endings
-------------------------

- **Git**: Git can automatically detect and handle line endings. Use the following command to prevent Git from converting line endings:

  .. code-block:: bash

    git config --global core.autocrlf input

- **Editor Plugins**: Many text editors support plugins or extensions that can detect and fix line ending issues. Consider using one to enforce consistent Unix-style line endings.

Why Unix Line Endings?
----------------------

- **Cross-Platform Compatibility**: Unix-style line endings are standard on most Unix-like systems (Linux, macOS), and maintaining this consistency helps ensure compatibility across all platforms.
  
- **Version Control**: Using a consistent line ending format prevents unnecessary diffs in version control. Mixing `LF` and `CRLF` line endings can result in changes being flagged that aren't actual code changes.

General Guidelines
------------------

- Ensure all files use Unix-style (`LF`) line endings.

- Configure your text editor to enforce Unix-style line endings.

- Use Git settings to automatically handle line endings during commits.

- Avoid mixing line endings in the same file to maintain consistency.


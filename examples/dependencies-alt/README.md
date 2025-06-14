# Alternate Dependencies Example

Demonstrates how to require your script's user to have at least one of a list
of dependencies (commands) installed prior to using your script.

This example was generated with:

```bash
$ bashly init
$ bashly add colors
# ... now edit src/bashly.yml to match the example ...
$ bashly generate
```

-----

## `bashly.yml`

````yaml
name: cli
help: Sample application that requires alternate dependencies
version: 0.1.0

commands:
- name: download
  help: Download something

  # This is the explicit way of defining dependencies.
  # The generated script will be halted (with a friendly error message) if
  # any of these programs are not installed:
  dependencies:
    # Abort with just the default 'missing dependency: git' message if git
    # is not found
    git:

    # Abort with an additional help message if ruby is not found
    ruby: visit $(blue_underlined https://www.ruby-lang.org) to install

    # Abort if both curl and wget are not found, and show an additional help
    # message.
    # Note that the path to the first found dependency will be available to
    # your script in the `deps` associative array.
    http_client:
      command: [curl, wget]
      help: install with $(green sudo apt install curl)
````



## Output

### `$ ./cli download`

````shell
# This file is located at 'src/download_command.sh'.
# It contains the implementation for the 'cli download' command.
# The code you write here will be wrapped by a function named 'cli_download_command()'.
# Feel free to edit this file; your changes will persist when regenerating.
args: none

deps:
- ${deps[git]} = /usr/bin/git
- ${deps[http_client]} = /usr/bin/curl
- ${deps[ruby]} = /home/vagrant/.rbenv/versions/3.4.1/bin/ruby


````




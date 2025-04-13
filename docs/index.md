# Welcome to MkDocs

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Commands

* `mkdocs new [dir-name]` - Create a new project.
* `mkdocs serve` - Start the live-reloading docs server.
* `mkdocs build` - Build the documentation site.
* `mkdocs -h` - Print help message and exit.

## Project layout

    mkdocs.yml    # The configuration file.
    docs/
        index.md  # The documentation homepage.
        ...       # Other markdown pages, images and other files.


## Syntax testing
```yaml title="test.yaml" linenums="1" hl_lines="2-3"
a:
  aa: "aa"
  ab: "ab"
b:
  ba: "ba"
  bb: "bb"
```

=== "Python"
    ```py
    def main():
        print("Hello world!")
    ```

=== "JavaScript"
    ```js
    console.log("Hello world")
    ```

!!! note "Note"
    This is a simple note.

!!! warning "Warning"
    This is a warning!

!!! danger "Danger!"
    This is dangerous!

??? info "Collapsible"
    This is an important text!
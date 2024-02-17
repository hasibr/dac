# Diagrams as Code

Diagrams as code is a practice where system architecture diagrams are created using code, enabling its persistence and tracking in version control.

A community list of Text to Diagram tools and their comparisons is maintained at [text-to-diagram.com](https://text-to-diagram.com/).

This repository aims to help quickly get started with generating diagrams using these tools in a containerized environment.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Terrastruct (D2 Language)](#terrastruct-d2-language)
    - [Documentation](#documentation)
    - [Usage](#usage)
- [Diagrams (Python Language)](#diagrams-python-language)
    - [Documentation](#documentation-1)
    - [Usage](#usage-1)


## Prerequisites

The software / tools required for this include:

- Rancher Desktop or Docker Desktop

## Terrastruct (D2 Language)

[Terrastruct](https://terrastruct.com/) is a general-purpose diagramming tool that is specialized for software engineering. It uses [D2](https://d2lang.com/), a diagram scripting language, to turn text into diagrams.

### Documentation

- Documentation: [link](https://d2lang.com/)
- Cheatsheet: [link](https://terrastruct-site-assets.s3.us-west-1.amazonaws.com/documents/d2_cheat_sheet.pdf)

### Usage

1. Edit `terrastruct/diagram.d2` to code your diagram.

3. Run the `terrastruct/diagram.d2` program in the container.

    ```sh
    docker run --rm -it \
        --user "$(id -u):$(id -g)" \
        --volume "${PWD}":/src \
        --workdir /src \
        --publish 127.0.0.1:8080:8080 \
        terrastruct/d2 \
        --watch --sketch terrastruct/diagram.d2
    ```

    The `--watch` flag runs this in watch mode, and will re-render your diagram when changes are detected.

    The `--sketch` flag renders the diagram to give the aesthetic of a hand-drawn sketch.

    Navigate to [http://127.0.0.1:8080](http://127.0.0.1:8080) in your browser to see the rendered diagram.

    It will create the rendered diagram as `diagram.svg` in the `terrastruct` folder.

## Diagrams (Python Language)

[Diagrams](https://github.com/mingrammer/diagrams) is a Python library that lets
you draw cloud system architecture using Python code. It uses [Graphviz](https://graphviz.org/) to render the images. The prerequisites for
running the Python program and rendering the diagram as an image is made
available as a Docker image here.

### Documentation

- Documentation: [link](https://diagrams.mingrammer.com/docs/guides/diagram)
- Examples: [link](https://diagrams.mingrammer.com/docs/getting-started/examples)

### Usage

1. Edit `diagrams/diagram.py` to code your diagram.

2. Build the Docker image.

    ```sh
    docker build --tag diagrams --file docker/diagrams/Dockerfile .
    ```

3. Run the `diagrams/diagram.py` program in the container. Since this project
    directory is mounted as volume in the container, it will generate the
    diagram image file (`web_service.png`) in the project root directory.

    ```sh
    docker run --rm -it \
        --volume "${PWD}":/src \
        --workdir /src \
        diagrams \
        python diagrams/diagram.py
    ```

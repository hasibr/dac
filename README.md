# Diagrams as Code

[Diagrams](https://github.com/mingrammer/diagrams) is a Python library that lets
you draw cloud system architecture using Python code. The prerequisites for
running the Python program and rendering the diagram as an image is made
available as a Docker image here.

## Prerequisites

The software / tools required for this include:

- Docker Desktop or Rancher Desktop

## Usage

1. Edit `diagram.py` to code your diagram.

    See [documentation](https://diagrams.mingrammer.com/docs/guides/diagram)
    and [examples](https://diagrams.mingrammer.com/docs/getting-started/examples).

2. Ensure a Docker daemon is running.

3. Build the Docker image.

    ```sh
    docker build --tag diagrams --file docker/Dockerfile .
    ```

4. Run the `diagrams.py` program in the container. Since this project
    directory is mounted as volume in the container, it will generate the
    diagram image file (`web_service.png`) in this directory.

    ```sh
    docker run --rm -it \
        --volume "${PWD}":/diagram \
        --workdir /diagram \
        diagrams \
        python diagram.py
    ```

FROM python:3-bookworm

# Install pre-requisites
# diagrams uses Graphviz to render the diagrams
RUN apt-get update && apt-get install -y \
    graphviz \
    && rm -rf /var/lib/apt/lists/*

# Install diagrams
RUN pip install diagrams

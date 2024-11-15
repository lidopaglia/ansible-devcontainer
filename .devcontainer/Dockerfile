FROM mcr.microsoft.com/devcontainers/python:1-3.12-bookworm

# refresh package cache and install useful tools
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get install -y sshpass vim iputils-ping

RUN pip install --upgrade pip && export PIP_ROOT_USER_ACTION=ignore \
    && python3 -m pip install poetry~=1.8.4

WORKDIR /workspaces/ansible

COPY poetry.lock pyproject.toml ./
RUN poetry install

# symlink dynamic poetry env to ~/venv
RUN venv=$(poetry env list | head -n 1 | cut -d ' ' -f 1) && \
    ln -s ~/.cache/pypoetry/virtualenvs/$venv ~/venv && \
    unset venv

CMD ["/bin/bash", "-c", "SHELL=/bin/bash poetry shell"]

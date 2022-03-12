FROM python:3.9.6-buster AS builder

# Install python packages
WORKDIR /tmp
COPY ./pyproject.toml .
COPY ./poetry.lock .
RUN pip install --upgrade pip && \
    pip install poetry && \
    poetry config virtualenvs.create false && \
    poetry install --no-dev && \
    rm -rf .cache && \
    rm -rf .pyproject.toml && \
    rm -rf .poetry

WORKDIR /home/work
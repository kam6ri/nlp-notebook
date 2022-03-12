FROM python:3.9.6-buster AS builder

# Install python packages
WORKDIR /tmp
COPY ./pyproject.toml .
COPY ./poetry.lock .
RUN pip install --upgrade pip && \
    pip install poetry && \
    poetry config virtualenvs.create false && \
    poetry install --no-dev && \
    rm -rf /tmp/* && \
    rm -rf /root/.cache

FROM python:3.9.6-slim-buster
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

WORKDIR /tmp

# Install mecab and ipadic
ENV MECABRC=/etc/mecabrc
RUN apt-get update && \
    apt-get install --no-install-recommends -y \
    mecab \
    libmecab-dev \
    mecab-ipadic \
    mecab-ipadic-utf8 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Install nodejs
RUN apt-get update && \
    apt-get install --no-install-recommends -y \
    curl && \
    curl -fsSL https://deb.nodesource.com/setup_16.x | bash - && \
    apt-get install -y nodejs

COPY --from=builder /usr/local/bin /usr/local/bin
COPY --from=builder /usr/local/share/jupyter /usr/local/share/jupyter
COPY --from=builder /usr/local/lib/python3.9/site-packages /usr/local/lib/python3.9/site-packages

WORKDIR /home/jovyan/work
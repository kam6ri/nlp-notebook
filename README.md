# :memo: nlp-notebook
This is a Docker integrated environment for natural language processing

## How to use
### Initial build for Docker image
To begin with, you have to build a Docker image by `build` command.
```bash
docker-compse build
```

### Start up Docker containers
Let's start up docker containers by `up` command in background `-d`.
```bash
docker-compse up -d
```

To build images before starting containers, use `--build` option.
```
docker-compse up -d --build
```

### Use an interactive shell in container
To run `bash` in the running `jupyter` container and connect it, use `exec` command.
```
docker-compse exec jupyter /bin/bash
```

### Download additional dictionary for MeCab
```
# Connect to running jupyter container
docker-compse exec jupyter /bin/bash

# Download mecab-ipadic-neologd
download_mecab_ipadic_neologd

# Download mecab-unidic-neologd
download_mecab_unidic_neologd
```
It is recommended that you run this script periodically, as the dictionary database to which you are downloading is updated frequently.  

Let's try to use these dictionary.
```python
import MeCab
 
# Use mecab-ipadic-neologd
mecab = MeCab.Tagger("-d /var/lib/mecab/dic/ipadic-neologd")
# Use mecab-unidic-neologd
# mecab = MeCab.Tagger("-d /var/lib/mecab/dic/unidic-neologd")

sent = "彼女はペンパイナッポーアッポーペンを踊った。"
print(mecab.parse(sent))
```
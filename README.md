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
 
 sent = "彼女はペンパイナッポーアッポーペンを踊った。"

# Use mecab-ipadic-neologd
mecab = MeCab.Tagger("-d /var/lib/mecab/dic/ipadic-neologd")
print(mecab.parse(sent))
# 彼女	名詞,代名詞,一般,*,*,*,彼女,カノジョ,カノジョ
# は	助詞,係助詞,*,*,*,*,は,ハ,ワ
# ペンパイナッポーアッポーペン	名詞,固有名詞,一般,*,*,*,Pen-Pineapple-Apple-Pen,ペンパイナッポーアッポーペン,ペンパイナッポーアッポーペン
# を	助詞,格助詞,一般,*,*,*,を,ヲ,ヲ
# 踊っ	動詞,自立,*,*,五段・ラ行,連用タ接続,踊る,オドッ,オドッ
# た	助動詞,*,*,*,特殊・タ,基本形,た,タ,タ
# 。	記号,句点,*,*,*,*,。,。,。
# EOS

# Use mecab-unidic-neologd
mecab = MeCab.Tagger("-d /var/lib/mecab/dic/unidic-neologd")
print(mecab.parse(sent))
# 彼女	カノジョ	カノジョ	彼女	名詞-固有名詞-一般		
# は	ワ	ハ	は	助詞-係助詞		
# ペンパイナッポーアッポーペン	ペンパイナッポーアッポーペン	ペンパイナッポーアッポーペン	ペンパイナッポーアッポーペン	名詞-普通名詞-一般		
# を	オ	ヲ	を	助詞-格助詞		
# 踊っ	オドッ	オドル	踊る	動詞-一般	五段-ラ行	連用形-促音便
# た	タ	タ	た	助動詞	助動詞-タ	終止形-一般
# 。			。	補助記号-句点		
# EOS

# Use default dictionary
mecab = MeCab.Tagger()
print(mecab.parse(sent))
# 彼女	名詞,代名詞,一般,*,*,*,彼女,カノジョ,カノジョ
# は	助詞,係助詞,*,*,*,*,は,ハ,ワ
# ペンパイナッポーアッポーペン	名詞,一般,*,*,*,*,*
# を	助詞,格助詞,一般,*,*,*,を,ヲ,ヲ
# 踊っ	動詞,自立,*,*,五段・ラ行,連用タ接続,踊る,オドッ,オドッ
# た	助動詞,*,*,*,特殊・タ,基本形,た,タ,タ
# 。	記号,句点,*,*,*,*,。,。,。
# EOS
```
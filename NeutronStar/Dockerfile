# ベースとなるイメージを指定
FROM ubuntu:20.04
# 新たにディレクトリを作成
RUN mkdir codes
# Workingディレクトリの指定
WORKDIR /codes
# インストール
RUN apt-get -y update \
    && apt-get -y upgrade \
    && apt-get install -y git \
    && apt-get install -y gcc g++ \
    && apt-get install -y cmake \
    && apt-get install -y csh \
    && apt-get install -y curl \
    && apt-get install -y libnuma-dev\
    && apt-get install -y python3-pip \
    && wget https://bootstrap.pypa.io/pip/3.10/get-pip.py \
    && python3 get-pip.py \
    && mkdir /code \
    && rm -rf /var/lib/apt/lists/* \
    && localedef -i en_US -c -f UTF-8 -A /usr/share/locale/locale.alias en_US.UTF-8
# 環境変数の設定
ENV LANG en_US.utf8
# requirements.txtを追加しディレクトリを移動
ADD requirements.txt /codes
# GitHubからAI-Fenmanのリポジトリをクローン
RUN git clone https://github.com/SJ001/AI-Feynman.git \
    && cd AI-Feynman && git reset --hard 28edde1a36a166a081de84999ab4fd40071957db \
    && cd .. \
    && pip install -r requirements.txt \
    && chmod +777 AI-Feynman/Code/* \
    && cd AI-Feynman/Code/ && ./compile.sh \
    && apt-get autoremove -y


# python3.10のイメージをダウンロード
FROM python:3.10.9

RUN apt-get update && \
    apt-get upgrade -y && \
    apt-get install -y --no-install-recommends cmake # for xlearn install

# コンテナにアクセスした際のデフォルトディレクトリ
WORKDIR /app

# @see https://zenn.dev/rihito/articles/7b48821e4a3f74
# poetryのインストール先の指定
ENV POETRY_HOME=/opt/poetry
# poetryインストール
RUN curl -sSL https://install.python-poetry.org | python3 - && \
# シンボリックによるpathへのpoetryコマンドの追加
    cd /usr/local/bin && \
    ln -s /opt/poetry/bin/poetry && \
    poetry config virtualenvs.create false

# poetryの定義ファイルをコピー (./app/配下に存在すると想定)
COPY pyproject.toml poetry.lock ./

# poetryでライブラリをインストール (pyproject.tomlが既にある場合)
RUN poetry install

# scikit-surprise
RUN poetry run python -m pip install --no-use-pep517 scikit-surprise

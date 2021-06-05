# 変更をする可能性が低いものを上から順番に書いてくれる
# 実行時にキャッシュしてくれるため(らしい)

# docker hubのイメージ名と:タグ名
FROM php:8.0-fpm-buster
SHELL ["/bin/bash", "-oeux", "pipefail", "-c"]

# サーバの環境変数を設定
  #composerをroot権限で実行できるように
ENV COMPOSER_ALLOW_SUPERUSER=1 \
  COMPOSER_HOME=/composer

# 別のdockerイメージのcomposerファイルを自分のイメージにコピー
# composerコマンドを実行できるようにする
COPY --from=composer:2.0 /usr/bin/composer /usr/bin/composer

# RUN命令は1ライナーにした方が最終的なイメージの容量が減る
# RUN命令を何回も実行するとレイヤーがどんどん増えてしまう
RUN apt-get update && \
  apt-get -y install git unzip libzip-dev libicu-dev libonig-dev && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/* && \
  docker-php-ext-install intl pdo_mysql zip bcmath

COPY ./php.ini /usr/local/etc/php/php.ini

# ログイン時の作業ディレクトリ指定
WORKDIR /work

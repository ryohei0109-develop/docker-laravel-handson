# docker-laravel-handson
----
●Webサーバについて

・nginxのdefault.confについて
nginx(Webサーバ:9000)にアクセスが来たら、
アプリケーションサーバ(app)に処理を投げる
・docker間通信ができるので、コンテナ名で名前解決してくれる

    location ~ \.php$ {
        fastcgi_pass app:9000;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }

・webサーバは特に拡張インストールする必要がないので、
「nginx」フォルダ以下にDockerfileを作っていない

----
●アプリケーションサーバについて

dockerフィルに書くと、ビルドするたびにLaravelがインストールされちゃう(その中のContollerファイル等が無くなる)
→Laravelは1回インストールだけで良い

・ビルドしてDockerイメージが作成される
→作成されたイメージをDockerHub等にあげておくと、以後、イメージ名を指定するだけでイメージをとってこれる
イメージをビルドしてコンテナを作るので、
設定ファイルを変更したらイメージを変更してビルドに反映させたい！

※volumesの設定ファイルは、docker compose upするだけで読み込んで反映される

- イメージの中にlaravel含めちゃうと開発できない
- apt-getでインストールしているものは開発中に変更することないからイメージの中にいれておきたい

----
●DBサーバについて

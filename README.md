# docker-laravel-handson

●nginxのdefault.confについて
nginx(Webサーバ:9000)にアクセスが来たら、
アプリケーションサーバ(app)に処理を投げる
・docker間通信ができるので、コンテナ名で名前解決してくれる

    location ~ \.php$ {
        fastcgi_pass app:9000;
        fastcgi_param SCRIPT_FILENAME $realpath_root$fastcgi_script_name;
        include fastcgi_params;
    }



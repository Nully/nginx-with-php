# Nginx with PHP

nginx-with-phpはCentOS6系で動作確認をしており、Debian系OSでは動作しません。

- 公開ユーザーについて
- Nginxの設定
- php-fpmの設定
- phpの設定

# 公開ユーザーについて

ここで定義する公開ユーザーは ```www``` ユーザーを指します。
すでにwwwユーザーが存在する場合、特に追加などは行われません。

# Nginxの設定

Nginxとphp-fpmhはリバースプロキシとして動作します。

php-fpmのソケットパスは ```/var/run/php-fpm/php-fpm.sock``` です。

Nginxのアクセスログやエラーログは ```/var/log/nginx/``` に保存され、
logrotateでローテーションされます。

# php-fpmの設定

php-fpmはユーザーグループともにnginxで動作しています。

php-fpmのエラーログは ```/var/log/php-fpm/``` に保存され、
logrotateでローテーションされます。

# phpの設定

phpの動作はphp.iniで決まります。
そのため、playbookに予め本番環境か開発環境かの設定を追加します。

本番環境の場合playbookに以下を追加します。

```
vars:
  is_production: yes
```



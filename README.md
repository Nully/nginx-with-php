# Nginx with PHP

nginx-with-phpはCentOS6系で動作確認をしており、Debian系OSでは動作しません。

- 使い方
- 公開ユーザーについて
- Nginxの設定
- php-fpmの設定
- phpの設定

## 使い方

ansibleのroleとして動作するため、gitのsubmoduleとして登録してください。

`` git submodule add https://github.com/Nully/nginx-with-php.git role/nginx-with-php ```

## 公開ユーザーについて

ここで定義する公開ユーザーは ```www``` ユーザーを指します。
すでにwwwユーザーが存在する場合、特に追加などは行われません。

## Nginxの設定

Nginxとphp-fpmhはリバースプロキシとして動作します。

php-fpmのソケットパスは ```/var/run/php-fpm/php-fpm.sock``` です。

Nginxのアクセスログやエラーログは ```/var/log/nginx/``` に保存され、
logrotateでローテーションされます。

## php-fpmの設定

php-fpmはユーザーグループともにnginxで動作しています。

php-fpmのエラーログは ```/var/log/php-fpm/``` に保存され、
logrotateでローテーションされます。

## phpの設定

phpの動作はphp.iniで決まります。
そのため、playbookに予め本番環境か開発環境かの設定を追加します。

本番環境の場合playbookに以下を追加します。

```
vars:
  is_production: yes
```

開発環境と本番環境で異なるのは

- display_errors
- error_reporting

の2項目です。

開発環境ではデバッグを行うため、error_reportingをE_NOTICE以上出力し、
エラーの出力を有効に指定ます。

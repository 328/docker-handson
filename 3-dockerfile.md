# Dockerfileを作ってみる

2-command.mdではコマンドを利用して、  
既存イメージ利用しnginx等のアプリケーションを実行しました。

## Dockerfileの作成

```
FROM centos:centos7
MAINTAINER 328
RUN yum -y install httpd
CMD rm -rf /run/httpd/* /tmp/httpd* && /usr/sbin/httpd -D FOREGROUND
```

- FROM
 - ベースとなるイメージを選択
- MAINTAINER
 - Dockerfile作った人とかコメント. (なくても良い)
- RUN
 - インストール作業とか, ソースのビルドとかを行う
- CMD
 - httpdとか、プロセス起動用のコマンドを記載する
 - pidファイルをrmしてるのは、コンテナ再起動時にpidファイルが残っていると起動しなくなるから

### ビルド

```
$ docker build -t apachetest .
$ docker images <- imageの確認
```

### 起動

```
$ docker run -d -p 8080:80 apachetest
```

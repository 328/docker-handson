## よく利用するdockerコマンドたち

使うdockerコマンドのリスト

```
  build       Build an image from a Dockerfile
  exec        Run a command in a running container
  images      List images
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  logs        Fetch the logs of a container
  ps          List containers
  pull        Pull an image or a repository from a registry
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
```

### コンテナを起動してみる

DockerHubからイメージを取得

```
$ docker pull hello-world
```

イメージの起動

```
$ docker run hello-world
```

### /bin/bash を起動してみる

```
$ docker pull centos
$ docker run -it centos /bin/bash
```
-i, --interactive    ホスト側の入力とコンテナの標準出力に繋げる (コマンドが打てる状態になる)
-t, --tty            コンテナ側の標準出力とホスト側の出力を繋げる

```
$ docker run centos /bin/bash # これはどうなる？
```

### サービスを起動してみる

```
$ docker run -p 80:80 nginx
$ docker run -p 80:80 -d nginx
```

-p ポートフォワーディング HOST:CONTAINER
-d バックグラウンド実行

### ファイルをマウントしてみる

`index.html`を作成
```
<p>hello world</p>
```

```
$ docker run -v $(pwd)/index.html:/usr/share/nginx/html/index.html -p 8080:80 -d --name ngx_container nginx
```

-v ホストのディレクトリやファイルをマウントできる (ro, read only optionも指定可能)

--name container名をつける

### コンテナが起動しているかを確認

```
$ docker ps
```

### 起動中のコンテナの中に入る

ファイルがきちんとマウントされているか確認

```
$ docker exec -it ngx_container /bin/bash <-コンテナに入る
# cat /usr/share/nginx/html/index.html
# exit <- コンテナから抜ける
```

### コンテナの停止と再起動

```
$ docker stop ngx_container
$ docker kill ngx_container
$ docker start ngx_container
$ docker restart ngx_container
```

### コンテナの名前変更

```
$ docker rename ngx_container hogehoge
```

### コンテナの削除

```
$ docker rm ngx_container
```

### Dockerイメージの削除

```
$ docker rmi nginx
```

#### tips

コンテナを全て削除

```
$ docker kill `docker ps -aq`
$ docker rm `docker ps -aq`
```

Dockerイメージを全て削除

```
$ docker rmi `docker images -aq`
```

viが無いイメージでviが使いたい

```
$ docker run -v /usr/bin:/usr/bin -p 8080:80 -d --name ngx_container nginx
```

====================================

# Dockerのコマンド集

```
Commands:
  attach      Attach local standard input, output, and error streams to a running container
  build       Build an image from a Dockerfile
  commit      Create a new image from a container's changes
  cp          Copy files/folders between a container and the local filesystem
  create      Create a new container
  deploy      Deploy a new stack or update an existing stack
  diff        Inspect changes to files or directories on a container's filesystem
  events      Get real time events from the server
  exec        Run a command in a running container
  export      Export a container's filesystem as a tar archive
  history     Show the history of an image
  images      List images
  import      Import the contents from a tarball to create a filesystem image
  info        Display system-wide information
  inspect     Return low-level information on Docker objects
  kill        Kill one or more running containers
  load        Load an image from a tar archive or STDIN
  login       Log in to a Docker registry
  logout      Log out from a Docker registry
  logs        Fetch the logs of a container
  pause       Pause all processes within one or more containers
  port        List port mappings or a specific mapping for the container
  ps          List containers
  pull        Pull an image or a repository from a registry
  push        Push an image or a repository to a registry
  rename      Rename a container
  restart     Restart one or more containers
  rm          Remove one or more containers
  rmi         Remove one or more images
  run         Run a command in a new container
  save        Save one or more images to a tar archive (streamed to STDOUT by default)
  search      Search the Docker Hub for images
  start       Start one or more stopped containers
  stats       Display a live stream of container(s) resource usage statistics
  stop        Stop one or more running containers
  tag         Create a tag TARGET_IMAGE that refers to SOURCE_IMAGE
  top         Display the running processes of a container
  unpause     Unpause all processes within one or more containers
  update      Update configuration of one or more containers
  version     Show the Docker version information
  wait        Block until one or more containers stop, then print their exit codes
```

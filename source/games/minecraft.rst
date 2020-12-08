==================
マインクラフト
==================


サーバ構築
===========

とりあえずhttps://www.howtoforge.com/tutorial/minecraft-server-ubuntu/を参考にしたやつ
クライアントのバージョンで怒られる?(クラはもちろん最新)
ubuntu1804

::

  $ sudo apt update
  $ sudo apt install git build-essential
  $ sudo apt install openjdk-11-jre-headless
  $ sudo useradd -r -m -U -d /opt/minecraft -s /bin/bash minecraft
  $ sudo passwd minecraft
  $ su - minecraft
  $ mkdir ~/backups ~/tools ~/server
  $ git clone https://github.com/Tiiffi/mcrcon.git ~/tools/mcrcon
  $ cd ~/tools/mcrcon
  $ gcc -std=gnu11 -pedantic -Wall -Wextra -O2 -s -o mcrcon mcrcon.c
  $ ./mcrcon -v
    mcrcon 0.7.1 (built: Dec  8 2020 05:35:13) - https://github.com/Tiiffi/mcrcon
    Bug reports:
            tiiffi+mcrcon at gmail
            https://github.com/Tiiffi/mcrcon/issues/
  $ wget https://launcher.mojang.com/v1/objects/a0d03225615ba897619220e256a266cb33a44b6b/server.jar -P ~/server
  $ cd ~/server
  $ java -Xmx1024M -Xms1024M -jar server.jar nogui
  ### ここでエラるけど，このあと出てくるファイルを編集
  $ vim ~/server/eula.txt
  - eula=false
  + eula=true
  $ vim ~/server/server.properties
  - rcon.password=
  - enable-rcon=false
  + rcon.password=[password]
  + enable-rcon=true
  $ java -Xmx512M -Xms512M -jar server.jar nogui


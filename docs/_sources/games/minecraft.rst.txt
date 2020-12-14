==================
マインクラフト
==================


サーバ構築HelloWorld
=======================

**バニラ**

とりあえずhttps://www.howtoforge.com/tutorial/minecraft-server-ubuntu/を参考にしたやつ
クライアントのバージョンで怒られる?(クラはもちろん最新)
ubuntu1804

::

  $ sudo apt update
  $ sudo apt install git build-essential
  $ sudo apt install openjdk-11-jre-headless    //これ8ジャネ
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

対応

::

  $ wget https://launcher.mojang.com/v1/objects/35139deedbd5182953cf1caa23835da59ca3d7cd/server.jar  ### バージョンを逐一確認するべき
  (https://www.minecraft.net/ja-jp/download/server)
  して，~/server/eula.txtの編集だけするようにしたらとりあえずできた．

**統合版**

::

  $ wget [url]    ※https://minecraft.gamepedia.com/Bedrock_Edition_1.16.200 ここからdownloadのところからコピる．
  $ unzip [落ちてきたファイル]
  $ ./bedrock_server

**forge**
ver 1.12.2でやってる．

::

  $ wget https://files.minecraftforge.net/maven/net/minecraftforge/forge/1.12.2-14.23.5.2854/forge-1.12.2-14.23.5.2854-installer.jar[:w
  $ wget https://files.minecraftforge.net/maven/net/minecraftforge/forge/1.12.2-14.23.5.2854/forge-1.12.2-14.23.5.2854-universal.jar
  $ java -jar ./forge-1.12.2-14.23.5.2854-installer.jar nogui --installServer
  $ java -Xms512M -Xmx 512M -jar forge-1.12.2-14.23.5.2854-universal.jar nogui
  $ vim eula.txt
  - eula=false
  + eula=true
  $ java -Xms512M -Xmx 512M -jar forge-1.12.2-14.23.5.2854-universal.jar nogui


**spigot**
https://hub.spigotmc.org/jenkins/job/BuildTools/
軽いって噂だったけどめっちゃ重いんだよね．
もしかしたらチャンクが多いのかもしれん．

::

  $ wget https://hub.spigotmc.org/jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar
  $ java -Xmx512M -jar BuildTools.jar --rev 1.16.4     // 多分メモリもっと上げないと普通に死ぬ．
  $ java -Xms512M -Xmx512M -jar ./spigot-1.16.4.jar nogui
  $ vim eula.txt
  - eula=false
  + eula=true
  $ java -Xms512M -Xmx512M -jar ./spigot-1.16.4.jar nogui
  

バージョン問題に関して
=========================

僕がずっとプレイヤーたちはどうしているのか気になっていたバージョン問題に関して，一つの回答を示しているサイトがあった．

https://riminosu13.hatenablog.com/entry/2020/08/24/192012

modの数が多いので，1.12.2か1.7.10が良いとのこと．

大手modサイト curseforge: https://www.curseforge.com/minecraft/mc-mods

Mod
=======

いくつか種類があるのでまずはそれの説明

- Minecraft Forge
- Spigot(Bukit?)
- Spongeforge



クライアントmodでとりあえず導入した方がいいやつ
-------------------------------------------------

※ちなみにこれはforge

optifineとシェーダー
`````````````````````

optifine自体は軽量化modで，描画処理のパフォーマンス向上のためのもの．
シェーダーは基本的にこれを前提としている?ので，導入すべき．
ただ，描画系のmodはこれを競合を起こすことがよくある．

optifineとKUDA-Shaders(最も有名なシェーダー?)の導入について: https://homanage.net/game/index.php?category=minecraft&name=kage

その他リンク:
- optifine公式: https://optifine.net/home
- KUDA-Shaders公式: https://dedelner.net/kuda-shaders/

テクスチャパックについて
``````````````````````````

ブロックやモブやアイテムやインタフェースのテクスチャを変えるためのファイル群のこと．

https://minecraft-ja.gamepedia.com/%E3%83%86%E3%82%AF%E3%82%B9%E3%83%81%E3%83%A3%E3%83%BC%E3%83%91%E3%83%83%E3%82%AF#:~:text=%E3%83%86%E3%82%AF%E3%82%B9%E3%83%81%E3%83%A3%E3%83%BC%E3%83%91%E3%83%83%E3%82%AF%20(Texture%20pack)%E3%81%AF,%E3%81%8C%E6%A0%BC%E7%B4%8D%E3%81%95%E3%82%8C%E3%81%A6%E3%81%84%E3%82%8B%E3%80%82

とりあえず小さくて良さげなテクスチャパック: 
https://mizunomcmemo.blogspot.com/p/resourcepack.html
http://www.mediafire.com/file/bknbzxz05dbl37n/Mizuno%2527s_16_Craft_JE_1.16.4-1.0.zip/file

デフォルトテクスチャの32x版のやつ．
ベタっとした感じあるけどマイクラ感を全く損なわないのでいい．:
https://faithful.team/faithful-1-12/
https://www.curseforge.com/minecraft/texture-packs/faithful-32x

一括破壊系
````````````

- CutAll
- DigAll
- MineAll

https://www.curseforge.com/minecraft/mc-mods/break-all-of-the-same-block-and-more/files
https://minecraft.fandom.com/ja/wiki/%E4%BE%BF%E5%88%A9%E7%B3%BBMOD

サーバにも導入する必要あり．
on/offのキーバインドはクライアント固有

- Fast Leaf Decay

https://www.curseforge.com/minecraft/mc-mods/fast-leaf-decay

葉っぱすぐ消えるmod．Cutallでも似たようなことできるけど，多分あっちの機能使うと葉っぱ分耐久が落ちそうな気がする．(そうした方が実装楽)からこれ入れた．
サーバだけでいい．

Map
-------

Xareros World Map:
https://www.curseforge.com/minecraft/mc-mods/xaeros-world-map

とりあえず，高機能すぎるものが多いので，全体Mapだけ追加できるこれを入れた．
本当はマーク機能も欲しかったけど，他のが本当に高機能すぎるし，かつミニマップを持ってるためこれ．
とりあえずクライアントだけで大丈夫そう．


サーバ管理系
===============

ホワイトリスト
-------------------

https://minecraft.server-memo.net/whitelist/


spigotでjava版と統合版でマルチプレイする方法
================================================
spigotの構築のあと

https://novablog.work/minecraft-crossplay/

::

  $ cd ~/spigot/plugins
  $ wget https://ci.nukkitx.com/job/GeyserMC/job/Geyser/job/master/lastSuccessfulBuild/artifact/bootstrap/spigot/target/Geyser-Spigot.jar
  $ wget https://ci.nukkitx.com/job/GeyserMC/job/Floodgate/job/master/lastSuccessfulBuild/artifact/bukkit/target/floodgate-bukkit.jar
  // start stop, make configs
  $ vim 
  iroiro
  $ vim 
  iroiro
  $ java 




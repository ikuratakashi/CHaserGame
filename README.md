# CHaser Game client - Python3

```
  ____ _   _                        ____    _    __  __ _____   ___ ___ 
 / ___| | | | __ _ ___  ___ _ __   / ___|  / \  |  \/  | ____| |_ _|_ _|
| |   | |_| |/ _` / __|/ _ \ '__| | |  _  / _ \ | |\/| |  _|    | | | | 
| |___|  _  | (_| \__ \  __/ |    | |_| |/ ___ \| |  | | |___   | | | | 
 \____|_| |_|\__,_|___/\___|_|     \____/_/   \_\_|  |_|_____| |___|___|
                                                                        
-- FG204 2nd EDITION Ver2.31 --
```

CHaserのクライアントとして起動することで、自分でコマンドラインから自機を操作できるようにしました。

通常のCHaserクライアントとして実行できます。ただし、サーバ側でタイムアウト時間を大きく設定してください。

タイムアウト時間を変更するには、サーバプログラムで以下の設定を変更してください。

```
サーバ設定 -> 通信タイムアウト時間
```

# 実行方法

### 通常の起動方法
```sh
 python CHaserGame.py
```
通常通り、ポート番号、名前、ホスト名のキー入力が求められます。

### COOLで起動する場合
```sh
 CHaserGame.py -c c
```

### HOTで起動する場合
```sh
 CHaserGame.py -c h
```

`-c` を引数にした場合には、CHaser.pyに記載されている、ポート番号、名前、ホスト名の値を読み込みます。

CHaser.pyの設定部分

```python
#定数 起動パラメータ
#SERVER_IP = "192.1.2.207"
SERVER_IP = "192.168.3.16"  # ホストのIP
LISN_PORT_C = "2009"        # coolのポート番号
LISN_PORT_H = "2010"        # hotのポート番号
USER_NAME_C = "COOL"        # cool時の名前
USER_NAME_H = "HOT"         # hot時の名前
```

## シェル(bash)での実行方法（macなどunix用）

run.sh がクライアントの起動シェルです。
ホストの設定に合わせて修正してください。

COOLで起動する場合
```sh
 ./run.sh c
```

HOTで起動する場合
```sh
 ./run.sh h
```

## 自分の環境での動かし方(Ikuraのmac環境のメモ)

COOLで起動する場合
```sh
python3.12 CHaserGame.py -c c
```

HOTで起動する場合
```sh
python3.12 CHaserGame.py -c h
```

# 遊び方

自分のターンになると、周辺の状況が表示されて、自機に対する操作の番号を入力します。

```
****************************************************************
 自分のターン[Turn:1]
----------------------------------------------------------------
AreaMap [Action After]
----------------------------------------------------------------
. . $
. + .
$ . .
----------------------------------------------------------------
Level:1 / HP:100 / Exp:0/100
Weapon:BLOCK(999) / BOM(1) / EYE(5) / ?????(1)
Weapon Use:
----------------------------------------------------------------
[Action] ←:4 →:6 ↑:2 ↓:8 Search:s Look:l Weapon:w ...
```
### Level、HP、Exp
自機のステータス（表示されていますが、未実装です）

### BLOCK(999) / BOM(1) / EYE(5) / ?????(1)
所持しているweaponの一覧。( )内は個数

### WeaponUse:
使用中のWeaponの一覧

`例）WeaponUse:EYE(10/15)`

EYEを使用中。15ターン有効で残りは10ターン。

### [Action] ←:4 →:6 ↑:2 ↓:8 Search:s Look:l Weapon:w ...
行動の選択

- ←:4 →:6 ↑:2 ↓:8 移動方向(walk_upなど)
- Search:s サーチ(search_upなど)
- Look:l ルック(look_upなど)
- Weapon:w Weaponの使用

## Weaponについて

独自のコマンドとして `weapon` を用意しました。`w` を入力してエンターを押すと、武器の使用コマンドが表示されます。
```
[Move] ←:4 →:6 ↑:2 ↓:8 Search:s Look:l Weapon:w ...w
Weapon : 武器を選択して使用します。
[Weapon] BLOCK:b BOM:bom EYE:e ?????:0 HELP:h Cancel:未入力 ...
```

- BLOCK:b ブロックを置きます。
- BOM:bom ボムを設置（未実装）
- EYE:e 周辺のマップを表示します。移動したことのある位置の周辺やSearchやLookの内容を記録して表示します。
- ????:0 効果が不明な武器の使用をします（未実装）
- HELP:h 各Weaponのヘルプが表示されます。
- Cancel:未入力 Weaponの使用をキャンセルします。

EYEの実行例
```
----------------------------------------------------------------
? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ?
? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ?
? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ?
? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ?
? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ?
? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ?
? ? ? ? ? ? ? ? ? ? ? ? ? ? . . # ? ? ? ? ? ? ? ? ? ? ? ? ? ?
? ? ? ? ? ? ? ? ? ? ? ? ? ? . ^ # ? ? ? ? ? ? ? ? ? ? ? ? ? ?
? ? ? ? ? ? ? ? ? ? ? ? ? ? $ . # ? ? ? ? ? ? ? ? ? ? ? ? ? ?
? ? ? ? ? ? ? ? ? ? ? ? . . . . $ ? ? ? ? ? ? ? ? ? ? ? ? ? ?
? ? ? ? ? ? ? ? ? ? ? ? $ . . . . ? ? ? ? ? ? ? ? ? ? ? ? ? ?
? ? ? ? ? ? ? ? ? ? ? ? . . $ . . ? ? ? ? ? ? ? ? ? ? ? ? ? ?
? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ?
? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ?
? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ?
? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ?
? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ? ?
----------------------------------------------------------------
Level:1 / HP:100 / Exp:0/100
Weapon:BLOCK(999) / BOM(1) / EYE(4) / ???(3)
Weapon Use:EYE(10/15)
----------------------------------------------------------------
```
GetReadyやwalkなどの戻り値を地図として記憶しています。最新の状態ではないので注意が必要です。
- ? まだ見ていない場所
- $ アイテム
- \# 壁
- ^ 自機（向いている方向によって文字が異なります 上:^ 右:> 下:v 左:<）
- C 敵（自分がhotの場合）
- H 敵（自分がcoolの場合）

# その他
コマンドの入力待ちの状態で、サーバ側でゲームセットとなった場合に、コマンドを入力した後にゲームセットの情報を受信します。

### CHaser.pyの修正箇所
CHaserの基本モジュールのCHaser.pyに若干手を加えています。

### 起動パラメータの追加

- 起動時にcoolかhotを引数で選択 `-c {c|h}`

# CHaserGameが起動しない場
CHaserGameが起動せずにエラーとなる場合は、ライブラリの読み込みに失敗している可能性が高いです。

以下のライブラリを使用していますので、再度ローカルにインストールしてください。

- colorama
コマンドラインに表示する時の文字色を設定する時に、OS依存を埋めてくれます。

- pyfiglet
指定した文字をアスキーアートで表示してくれます。

## ライブラリの再インストール方法

1. CHaserGame.pyと同じ階層に `lib` フォルダを作成（libフォルダが無い場合）

以下のようなフォルダ階層にしてください。

```
CHASERGAME
 ├ lib
 ├ CHaserGame.py

``` 

2. インストール実行のコマンドを入力し、エンターキーを押す

```cmd
pip install colorama --target /lib
```
```cmd
pip install pyfiglet --target /lib
```

これを実行した後に、CHaserGameを起動すると、起動画面が正常に表示されると思います。

# ソース内容について

いくつかのクラスに機能が分かれています。重要なものから順に挙げています。

## clsSystemAdministrator
システム全体を管理する予定のクラスです。名前はAdministratorと大袈裟ですが、今のところは、オープニングなどを表示しているクラスです。一見どうでもいいクラスと化していますが、ゲームを盛り上げるためにもこういったクラスは超重要です。

オープニングで初期化をしているように見えますが、ネタばれするとダミーです。

## clsWeapon
武器のクラスです。武器のひとつずつを表します。

## clsWeapons
武器を管理するクラスです。複数の武器をひとまとめにしています。

## clsPlayerData
プレイヤーのクラスです。

重要なメソッドとして `DoActionPlayer` を作りました。このメソッドを実行することで、行動したり、向いている方向など記憶することができます。

一応、プロパティの `log:[]` で行動のログをメモリ上に記録しています。何かに使えるかもしれません。

## clsAreaTalbe -- 継承 -> clsAreaTalbeEx
周辺の情報を管理するクラスです。継承をしていますが、あまり意味はありません。Pythonの継承を試してみたかっただけです。

CHaserクラスの行動に関するメソッドの戻り値を記憶するようになっているので、競技用のプログラムを作るときに、行動の判定や指定した位置に移動したいときなどに使えると思います。

clsPlayerDataクラスと依存関係があるので、使いたいときはclsPlayerDataクラスも一緒にコピーする必要があります。

プロパティの`arealist`が周辺情報です。2次元配列になっているので、イメージしやすいと思います。
以下のようなソースで参照できると思います。

### 全部を参照する場合
```python
for row in self.arealist:
    for field in row:
        print(f"{field} ",end="") #内容を表示
    print() #改行
```

### 一つずつを参照する場合
```python
print(f"{self.arealist[1][2]} ") #内容を表示
```

インスタンス化するときに記憶領域のサイズを指定していますが、必ず31以上の奇数に指定してください。奇数でないと、プレイヤーの中心が取れない為です。

奇数だと、中心が取れる。
```
# # #
# C #
# # #
``` 

偶数だと、中心が取れない。
```
# # # # 
# # # # 
# # # # 
# # # # 
``` 

※重要なメソッド

### UpdateAreaList()
周辺の情報を更新するメソッドです。

### PrintArea()
周辺の情報を画面に表示するメソッドです。

## clsGameMaster
ゲーム全体を管理するクラスです。重要かと思っていたのですが、大したことはしていませんでした（こんなハズじゃなかったのに...）もっと重要な役割を与えてあげないと名前負けしています。

## clsActionResult
プレイヤーの行動の結果のクラスです。

## clsBeep
Beep音を鳴らす為のクラスです。ライブラリをインストールしたけどエラーになったりと、動作がどうも不安定なのでコメントアウトしています。

他にもいろんなクラスがありますが、ソースにコメントを書いてあるのでそちらを参照してください。

あと、変数や定数などはどんな記述の仕方があるのか調べながら宣言したので、色んな方法で記載してあります。定数のクラスを作ってまとめたかったのですが、後でまとめて対応しようと思っていて、そのままにしてあります。なので、クラスをコピーして別のソースで使用する場合は、グローバルな感じで宣言されている変数もコピーするように注意してください。
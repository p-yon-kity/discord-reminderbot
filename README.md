
# このBotについて

- Discordでリマインダーを使うBotです(リマインドの定期実行も可能)
- スラッシュコマンド（[eunwoo1104 / discord-py-slash-command](https://github.com/eunwoo1104/discord-py-slash-command)）が使えるため、コマンドを覚える必要がなく、それぞれのオプションの意味が表示されます
  - [有名なリマインダーBotが定期実行に寄付が必要](https://qiita.com/kbt0401/items/1d26f2c99580647e12dc)という記事を見て作ってみました
- 以下の招待リンクからお試しできます
  - 招待リンク: <https://discord.com/api/oauth2/authorize?client_id=873515660674756639&permissions=2147723280&scope=bot%20applications.commands>
  - 止まってたりしたらこっそり教えてください(その前に、`/remind-task-check`で直るかもしれません)

## 機能

### `/remind-list`

- ギルドで使用すると、自分がそのギルドで登録したリマインドを表示します
- BotとのDMで使用すると、自分が登録したリマインドを表示します
- オプション
  - status
    - 実行予定のリマインドリスト(デフォルトと同じ)
      - 今後リマインドされるリストを表示します
    - キャンセルしたリマインドリスト
      - キャンセルされたリマインドリストを表示します
    - 終了したリマインドリスト
      - リマインドしたリストを表示します
  - reply_is_hidden
    - 自分のみ
      - 実行結果は自分だけ見ることができます
    - 全員に見せる
      - 実行結果はBotからのリプライとして表示されます

### `/remind-make`

- リマインドを登録します（登録したリマインドが**今は**表示されます）
  - 秘密なリマインドはコレで登録せず、ご自身のカレンダーやTODOへ登録するようにしてください
- 必須のオプション(3つ)
  - date(リマインド日時)
    - mm/dd形式
    - 日数でも登録できる(`0`で当日、`1`で1日後)
    - yyyy/mm/dd形式で年も含めて登録
    - mm-dd形式もOK(yyyy-mm-dd形式もOK)
  - time(リマインド時間)
    - hh:mi形式(例→`23:12`)
    - xxh(xx時間後という意味。例→`10h`)
    - xxmi(xx分後という意味。例→`10mi`)
  - message(メッセージ)
    - リマインドするメッセージ
    - メンションしたい場合、通常のメッセージと同様に、@xxxx形式で入力してください（リマインド時にメンションされます）
- オプション
  - repeat_interval(繰り返し間隔)
    - XX分: **XX**mi
    - XX時間: **XX**h
    - X日:  **X**d
    - Xヶ月: **X**m
    - X年: **X**y
      - Xは数字(例→`10mi`)
      - 通知した後、上記で指定しただけ遅らせた年月で通知するリマインドを作成します
  - repoeat_max_count(繰り返し最大回数)
    - 数字を設定
    - 例→`2`としたら、1回目の通知の後に**繰り返し間隔だけ遅らせたリマインドが作成されます**。2回目を通知し、それ以降は通知されません
      - 具体例: `/remind-make date:2021/3/26 time:21:00 message:@here test!!! repeat_interval:2d repeat_max_count:2`
        - 2021/3/26 21:00に「@here test!!!」が通知され、2回目として2021/3/28 21:00に「@here test!!!(2)」が通知されます
        - 2回目以降は勝手に、メッセージに連番をふります(URLの場合のみ連番をふりません)
      - 追加で通知したい場合は別途リマインドを作成してください
  - channel(リマインドするチャンネル)
    - #xxxxで指定したチャンネルにリマインドします
    - そのままチャンネル名を指定することもできます
    - このオプションが**ない場合、コマンドを実行したチャンネルにリマインドします**
  - reply_is_hidden
    - 自分のみ
      - 実行結果は自分だけ見ることができます
    - 全員に見せる
      - 実行結果はBotからのリプライとして表示されます

### `/remind-cancel`

- リマインドをキャンセルします
- 必須のオプション(1つ)
  - cancel_no(キャンセルするリマインドのNo)
    - 数字
    - あなたが登録したリマインドのNoである必要があります（他人のリマインドはキャンセルできません）
- オプション
  - reply_is_hidden
    - 自分のみ
      - 実行結果は自分だけ見ることができます
    - 全員に見せる
      - 実行結果はBotからのリプライとして表示されます

### `/remind-list-guild-all`

- ギルド内のみ、かつ、ギルドの管理者権限保持者のみ使用可能
- そのギルドで登録されているリマインドをすべて表示します
- オプション
  - status
    - 実行予定のリマインドリスト
      - 今後リマインドされるリストを表示します
    - キャンセルしたリマインドリスト
      - キャンセルされたリマインドリストを表示します
    - 終了したリマインドリスト
      - リマインドしたリストを表示します
  - reply_is_hidden
    - 自分のみ
      - 実行結果は自分だけ見ることができます
    - 全員に見せる
      - 実行結果はBotからのリプライとして表示されます

### `/remind-list-all`

- BotとのDMのみ、かつ、Botのオーナー(DiscordのBotのトークンを生成した人)のみ使用可能
- Botに登録されているリマインドをすべて表示します
- オプション
  - status
    - 実行予定のリマインドリスト
      - 今後リマインドされるリストを表示します
    - キャンセルしたリマインドリスト
      - キャンセルされたリマインドリストを表示します
    - 終了したリマインドリスト
      - リマインドしたリストを表示します
  - reply_is_hidden
    - 自分のみ
      - 実行結果は自分だけ見ることができます
    - 全員に見せる
      - 実行結果はBotからのリプライとして表示されます

### `/remind-task-check`

- BotのTaskが正常に動いているかチェックする(止まってたらTaskを開始するはず)
- オプション
  - reply_is_hidden
    - 自分のみ
      - 実行結果は自分だけ見ることができます
    - 全員に見せる
      - 実行結果はBotからのリプライとして表示されます

### `delete-old-data`

- Botのオーナー(DiscordのBotのトークンを生成した人)のみ使用可能
- ステータスが「完了」のリマインドをすべて削除(添付ファイルの容量が厳しいため)

### その他のコマンドは検討中です(リマインドの削除など実装予定)

## 環境変数

### DISCORD_TOKEN

- あなたのDiscordのトークンを記載（トークンは厳重に管理し、公開されないよう配慮すること！）
- 例: DISCORD_TOKEN="fdj2iur928u42q4u239858290"

### LOG_LEVEL

- ログレベル(DEBUG/INFO/WARNING/ERROR)
- 例: LOG_LEVEL="INFO"

### ENABLE_SLASH_COMMAND_GUILD_ID_LIST(**使用するにはソースの修正が必要です**)

- この環境変数を使用する場合、ソースの修正をしてください
  - それぞれのメソッドにある、@cog_ext.cog_slashのguildsについてのコメントアウトを解除する必要があります
- スラッシュコマンドを有効にするギルドID(複数ある場合は「;」を間に挟むこと)
- 例
  - 1件の場合: ENABLE_SLASH_COMMAND_GUILD_ID_LIST=18471289371923
  - 2件の場合: ENABLE_SLASH_COMMAND_GUILD_ID_LIST=18471289371923;1389103890128390

### KEEP_DECRYPTED_FILE

- 復号されたファイルを残すかどうか(TRUEの時のみ残す。デフォルトでは復号されたファイルは削除される)
- 例: KEEP_DECRYPTED_FILE=FALSE

### IS_HEROKU

- Herokuで動かすかどうか
  - Herokuの場合、ファイルが削除されるので、discordの添付ファイルを使って保管を試みる(ファイルが削除されていたら、読み込む)
- 例: IS_HEROKU=FALSE

### IS_REPLIT

- Repl.itで動かすかどうか
  - Repl.itの場合、sqlite3の保管が怪しいので、discordの添付ファイルを使って保管を試みる
- 例: IS_REPLIT=TRUE

### RESTRICT_ATTACHMENT_FILE

- Bot自身が添付したファイルのみ読み込むように制限するかどうか
  - Bot以外(他のBotや人間)が添付したファイルのみを読み込むようになります
- 例: RESTRICT_ATTACHMENT_FILE=TRUE

### PRIORITY_GUILD

- 優先してファイルを添付するギルド(1件のみ指定してください)
  - 権限の問題で、Botがファイル保管に失敗することがあるため、失敗時に添付するギルドを指定できる
- 例: PRIORITY_GUILD=99999999999

### REMIND_CONTROL_CHANNEL_NAME

- リマインダーのデータを保存するチャンネル名を指定できます(未指定の場合remind_control_channel)
  - 他のギルドもその名前のチャンネルが保存先に使われるので気をつけてください
  - テスト中に複数のリマインダーBot動かしてて困ったので作成した環境変数です(基本開発に使うもの)
- 例: REMIND_CONTROL_CHANNEL_NAME=リマインドチャンネル

## 動かし方

- wikiに書くつもりです(時期未定)
- わからないことがあれば[Discussions](https://github.com/tetsuya-ki/discord-reminderbot/discussions)に書いてみてください

### 普通に動かす場合

#### 前提

- poetryがインストールされていること
- `.env.sample`をコピーし、`.env`が作成されていること(それぞれの環境変数の意味は[環境変数](#環境変数)を参照ください)

#### 動かす

- 以下のコマンドを実行

```sh
poetry run python discord-reminderbot.py
```

### docker-composeを用いた起動手順

#### 前提(docker-compose)

- `docker`,`docker-compose`コマンドが利用できること

#### 環境変数の設定

- `.env`の準備の代わりに、`docker-compose.override.yml`を作成して環境変数を記載

```docker
version: "3"

services:
  app:
    environment:
      - DISCORD_TOKEN=__あなたのDicordトークン__
      - LOG_LEVEL=INFO
      - ENABLE_SLASH_COMMAND_GUILD_ID_LIST= __あなたのGuild_IDを入力(数字/複数あるなら;を挟むこと。グローバルコマンドの場合は入力しないこと！(その場合1時間程度登録に時間がかかる可能性があります))__
      - KEEP_DECRYPTED_FILE=FALSE
      - IS_HEROKU=FALSE
      - IS_REPLIT=FALSE
      - RESTRICT_ATTACHMENT_FILE=FALSE
      - PRIORITY_GUILD=__あなたのGuild_IDを入力(数字)__
      - REMIND_CONTROL_CHANNEL_NAME=remind_control_channel
```

#### 起動・停止操作

- Dockerイメージのビルド
`docker-compose build`

- 起動
`docker-compose up -d`

- 停止
`docker-compose down`

- ログ出力
`docker-compose logs -f`

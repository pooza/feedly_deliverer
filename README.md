# feedly-bot

Feedlyの新着エントリーをSlackに喋らせる。

## ■設置の手順

- 常時起動のUNIX系サーバでさえあれば、どこでも設置可。

### リポジトリをクローン

```
git clone git@github.com:pooza/feedly-bot.git
```

### 依存するgemのインストール

```
cd feedly-bot
bundle install
```

### local.yamlを編集

```
vi config/local.yaml
```

以下、設定例。

```
access_token:
  token: __YOUR_TOKEN__ #アクセストークン
  expires_on: 2017-03-23 #アクセストークンの期限日
slack:
  hook:
    url: https://hooks.slack.com/services/*********/*********/************************
```

### syslog設定

feedlrというプログラム名で、syslogに出力している。  
必要に応じて、適宜設定。以下、rsyslogでの設定例。

```
:programname, isequal, "feedlr" -/var/log/feedlr.log
```

## ■操作

loader.rbを実行する。root権限不要。  
cronで60分毎等で起動。

## ■設定ファイルの検索順

local.yamlは、上記設置例ではconfigディレクトリ内に置いているが、実際には以下の順に検索している。

- /usr/local/etc/feedly-bot/local.yaml
- /etc/feedly-bot/local.yaml
- 設置先/config/local.yaml

同様に、local.yamlというファイルは、実際には以下の順に検索している。

- local.yaml
- local.yml

設置先ディレクトリもファイル名も、そのファイルが発見できた時点で、以降の検索をやめる。

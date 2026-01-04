# radish-play.sh
[NHKラジオ らじる★らじる](https://www.nhk.or.jp/radio/) / [radiko](http://radiko.jp/) / [ListenRadio](http://listenradio.jp/) / [渋谷のラジオ](https://shiburadi.com/) で現在配信中の番組を保存するシェルスクリプトを改造し、単純に再生するようにしたものです。


## 必要なもの
- curl
- libxml2 (xmllintのみ使用)
- jq
- FFmpeg (3.x以降 要AAC,HLSサポート)


## 使い方
```
$ ./radish-play.sh [options]
```

| 引数 | 必須 |説明 |備考 |
|:-|:-:|:-|:-|
|-t _SITE TYPE_|○|対象サイト|nhk: NHK らじる★らじる<br>radiko: radiko<br>lisradi: ListenRadio<br>shiburadi: 渋谷のラジオ
|-s _STATION ID_|△|放送局ID|`-l` オプションで表示されるID<br>渋谷のラジオは指定不要|
|-d _MINUTE_|○|録音時間(分)(Not In Use)||
|-i _MAIL_||ラジコプレミアム ログインメールアドレス|環境変数 `RADIKO_MAIL` でも指定可能|
|-p _PASSWORD_||ラジコプレミアム ログインパスワード|環境変数 `RADIKO_PASSWORD` でも指定可能|
|-o _PATH_||出力パス|未指定の場合カレントディレクトリに `放送局ID_年月日時分秒.(m4a or mp3)` というファイルを作成<br>拡張子がない場合または配信側の形式と異なる場合には拡張子を自動補完します(Not In Use)|
|-l||放送局ID/名称表示|結果は300行以上になります、また取得は(割と)重いです|


## 実行例
```
NHK らじる★らじる
$ ./radish-play.sh -t nhk -s tokyo-fm
```

```
radikoエリア内の局
$ ./radish-play.sh -t radiko -s LFR
```

```
radikoエリア外の局 (ラジコプレミアム)
$ ./radish-play.sh -t radiko -s HBC
```

```
radikoエリア外の局 (ラジコプレミアム 環境変数からログイン情報設定)
$ export RADIKO_MAIL="foo@example.com"
$ export RADIKO_PASSWORD="password"
$ ./radish-play.sh -t radiko -s HBC
```

```
ListenRadio
$ ./radish-play.sh -t lisradi -s 30058
```

```
渋谷のラジオ
$ ./radish-play.sh -t shiburadi
```


## 注意点

また渋谷のラジオの録音時にではffmpegから "Application provided invalid, non monotonically increasing dts to muxer in stream" というメッセージが吐き出されるのですが、音声は聴けるようなのでとりあえずそのままにしています。


## 動作確認環境
- Raspberry Pi OS Debian 12(Bookworm)
    - curl 7.88.1
    - xmllint using libxml version 20914
    - jq 1.6
    - ffmpeg 5.1.6-0+deb12u1+rpt3

-Hardware: Raspberry Pi Zero 2W, Raspberry Pi Zero W
但し radikoエリア外の局の動作検証は行っていません


##  メンテナー
kikegami0841 ([https://ss1.xrea.com/ike.s206.xrea.com/wordpress/](https://ss1.xrea.com/ike.s206.xrea.com/wordpress/))

- forked from ([jg1uaa/radish-play](https://github.com/jg1uaa/radish-play))

## ライセンス
[MIT License](LICENSE) 
fork元に準ずる

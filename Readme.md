# BP通知Bot
## 注意点
* 不具合や要望等は、開発者の[X(旧Twitter)](https://twitter.com/MatchaMiG)までお願いいたします。
## 導入方法
**【注意】 Bot導入にはサーバの管理者権限が必要です。**
### 開発者のBotを導入する場合
1. [Botリンク](https://discord.com/api/oauth2/authorize?client_id=1157941242001362964&permissions=134144&scope=bot) から導入したい鯖に参加させてください
### 個人でサーバーを用意して稼働する場合
1. 下記環境変数を設定
    | 環境変数名 | 値 | 備考 |
    |:--|:--|:--|
    | Token | Botのトークン | [Discord Developer Portal](https://discord.com/developers/applications/) にて取得可能 |
    | RaidNotifyCh | レイド通知チャンネル設定を保存するファイルのパス | 拡張子は .pickle |
    | RegnasClockNotifyCh | レグナス時計通知チャンネル設定を保存するファイルのパス | 拡張子は .pickle |
    | NowRaid | 開催中のレイドミッション名 | 区切り文字は「, (カンマ)」でスペースは無視される |
2. 【補足】 [Discord Developer Portal](https://discord.com/developers/applications/)
     * トークンの取得手順はわからなければ各々調べてください
     * BOT設定の内、以下の設定はONにすること
       * **Privileged Gateway Intents**
         * `MESSAGE CONTENT INTENT`
       * **Bot Permissions**
         * `GENERAL PERMISSIONS`
           * `Read Messages/View Channels`
         * `TEXT PERMISSIONS`
           * `Send Messages`
           * `Mention Everyone` (※`@everyone`しないなら不要)
3. プログラムを起動: `py -m bp_notify_bot`
   * 起動方法は環境に適した方法を利用してください
   * [Railway](https://railway.app/)で利用可能なDockerfileも同梱しています

## 利用方法
### ヘルプコマンド
* `/help`: ヘルプコマンド
  * 本書へのGitHubでのリンクを提示します

### レイド通知コマンド
1. `/set_raid_notification`: レイド通知チャンネル設定コマンド  
   * このコマンドを使用したチャンネルをレイド通知対象のチャンネルとして設定
   * 設定を変更したい場合も、このコマンドを使用
   * 下記説明に従って、各引数を設定  
     * **offset**: レイド通知を開催時刻から何分ずらして通知するかの設定 (**必須**)
       * -60 ~ 120(分)の整数値で設定可能 (範囲外の値は無視)
         * 正の場合、〇〇分前 に通知 (例) offset=5: 5分前 / offset=0: 0分前
         * 負の場合、〇〇分後 に通知 (例) offset=-60: 60分後
       * 複数設定可能
         * 数値と"-(マイナス)"以外の文字(スペース可)で値の間を区切ること  
          (例) 30, 10, -10, -60: 30分前/10分前/10分後/60分後 の4つ設定
     * **mention**: メンション設定 (任意)
       * メンションしたいロールやユーザ(@everyoneや@here含む)を設定
       * 複数設定可能
         * Discord上で青紫がかってれば区切り等は意識しなくてok
       * 未設定の場合/入力した値が不正な場合、メンションなし
     * **type**: メッセージタイプ (任意)
       * 下記数値の中から選択   
          | 値 | タイプ | 例 |
          |:-:|:--|:--|
          | 1 | シンプル | レイド開催 |
          | 2 | 受付嬢 | 大型エネミーの出現が確認されました。星脈孔に向かい討伐任務に参加してください。 |
          | 3 | 御令嬢 | 大型エネミーが出現しましてよ～～！冒険者の皆様はご討伐くださいませ～～！！ |
          | 2816 | ニワトリ ※ネタ枠 | ｺｹｺｺｺｯｺｹｺｺｺｯｺｹｺｺｯｺｺｯｹｺｯｹｺｹｹｹｯｹｹｺｹｯｺｺｹｺｹｯｺｹｹｺｹｯｺｹｺｺｯｺｺｯｹｹｺｹｺｯｺｹｹｺｯｹｺｹｹｯｺｺｯｺｹｺｹｺｯ |
        
       * 未設定の場合/入力した値が不正な場合、1のシンプルに設定

2. `/unset_raid_notification`: レイド通知チャンネル設定解除コマンド  
   * 引数なし
   * このコマンドを使用したチャンネルをレイド通知対象から解除

---
### レグナス時計通知コマンド
> 【注意】 通知がすごい数来ます 
1. `/set_clock_notification`: レグナス時計通知チャンネル設定コマンド  
   * このコマンドを使用したチャンネルをレグナス時計通知対象のチャンネルとして設定
   * 設定を変更したい場合も、このコマンドを使用
   * 下記説明に従って、各引数を設定  
     * **offset**: レグナス時計通知を時間帯切替日時から何分ずらして通知するかの設定 (**必須**)
       * 0 ~ 24(分)の整数値で設定可能 (範囲外の値は無視)
         * 〇〇分前 に通知 (例) offset=5: 5分前 / offset=0: 0分前
       * 複数設定可能
         * 数値と"-(マイナス)"以外の文字(スペース可)で値の間を区切ること  
          (例) 10, 0: 10分前/0分前 の2つ設定
     * **mention**: メンション設定 (任意)
       * メンションしたいロールやユーザ(@everyoneや@here含む)を設定
       * 複数設定可能
         * Discord上で青紫がかってれば区切り等は意識しなくてok
       * 未設定の場合/入力した値が不正な場合、メンションなし
     * **type**: メッセージタイプ (任意)
       * 下記数値の中から選択   
          | 値 | タイプ | 例 |
          |:-:|:--|:--|
          | 1 | シンプル | 時間帯移行 夜 > 昼 |
          | 2 | 受付嬢 | もなく時間帯が昼になります。 |
          | 3 | 御令嬢 | 昼になりますわ～～～！！ |
          | 2816 | ニワトリ ※ネタ枠 | ｹｹｺｺｹｯｹｺｹｹｺｯｹｺｯｺｺｯｹｹｯ |
        
       * 未設定の場合/入力した値が不正な場合、1のシンプルに設定

2. `/unset_clock_notification`: レグナス時計通知チャンネル設定解除コマンド  
   * 引数なし
   * このコマンドを使用したチャンネルをレグナス時計通知対象から解除

---
### レグナス時計機能
* こちらはコマンド等はありません
* Botのステータス欄に「現在の時間帯」及び「現在の時間帯の期間(現実の日本時間)」が表示されます
* ブルプロの時間計算が一部特殊なため、時間がずれる場合がありますがご了承ください
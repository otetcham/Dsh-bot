<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="docs/images/logo-dark.svg">
    <img src="docs/images/logo.svg" alt="DeepSeek Bot" width="260">
  </picture>
</p>

# Dsh-bot

[English](README.md) | [中文](README.zh.md) | 日本語

![version](https://img.shields.io/badge/version-v0.1_preview-blue) ![DSH](https://img.shields.io/badge/DSH-0.2.1--alpha.1-4D6BFE) ![license](https://img.shields.io/badge/license-Apache_2.0-green)

DeepSeek Bot（DS Bot）は、[DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness)（DSH）向けの bot プラグインです。DSH を bot として使えるようにし、自分で作成した bot と会話したり作業したりできます。

![Chief に一言伝えるだけで、bot とグループチャットをセットアップ](docs/images/team.png)

## インストール

まず DSH をインストールし、その中で少なくとも 1 つのモデルを設定してください。DS Bot は DSH のモデルをそのまま利用します。

**DSH Desktop（Windows、macOS）**

1. サイドバーで **Plugins** → **Add plugin** を選択します。
2. **Package name or address** に `ds-bot` を入力します。中国本土では **Registry** を **Mainland China mirror** に設定します。
3. **Install** を選択してから **Enable now** を選択します。変更が次回起動時に反映されると表示された場合は、DSH を完全に終了して再起動します。

npm に接続できない場合、手順 2 では [Releases](https://github.com/FeiZhuLulu/DeepSeek-Bot/releases) からダウンロードした `ds-bot-0.1.2.tgz` のフルパス、または `github:FeiZhuLulu/DeepSeek-Bot#v0.1.2&path:/ds-bot`（Git が必要）も指定できます。

**DSH Web（Windows、macOS、Linux）**

Node.js `22.19` 以上と pnpm が必要です。

```sh
npx @deepseek-ai/dsh@0.2.1-alpha.1 plugin --profile web add ds-bot
npx @deepseek-ai/dsh@0.2.1-alpha.1 web
```

## セットアップ

他の bot やグループチャットのセットアップは、bot と会話しながら行うことを強くおすすめします。

## 機能

### Bot

1 つの bot と 1 つの画面で、会話も作業もすべて行えます。背後のコンテキストを気にする必要はありません。bot の詳細ページでは bot の情報を確認でき、使用するモデルも選べます。モデルはいつでも切り替えられますが、1 つの bot では長期間同じモデルを使い、本当に必要なときだけ切り替えることをおすすめします。

bot にはメモリ機能もあります。bot はあなたの好みを記憶し、次回以降の作業に反映します。メモリは bot の詳細ページで管理することも、bot に直接伝えて管理することもできます。

![Bot details: model, memory, usage](docs/images/details.png)

### メイン bot

メイン bot はあなたの Chief です。非常に高い権限を持ち、他の bot とグループチャットを管理します。DS Bot を初めて開いたときには、Chief というメイン bot がすでに用意されています。Chief に話しかけると、セットアップを案内してくれます。

要するに、質問があればメイン bot に聞いてください。

### グループチャット

DS Bot にはグループチャットがあります。複数 bot の協調作業には有効ですが、コストは明確に増えます。そこで DS Bot では、各グループチャットに管理者を置きます。通常は管理者があなたのメッセージに返信し、必要に応じて他の bot を呼び出します。特定の bot を直接 @ メンションして、その bot から直接返信を受けることもできます。

![Group chat: the admin, Chief, hands the work to Writer and Coder](docs/images/group.png)

### 使用量

**Settings** → **Usage** では、トークン使用量を時間別・bot 別・モデル別で確認できます。

![Usage page](docs/images/usage.png)

## データ

すべてのデータは、DSH ホームディレクトリ（デフォルトは `~/.dsh`）の `bot/` と `sessions/` に保存され、あなた自身のコンピューター内に留まります。プラグインをアンインストールしても、このデータは削除されません。

## 開発

プラグインのソースは [`ds-bot/`](ds-bot/) にあります。オプションと内部構造は [`ds-bot/README.md`](ds-bot/README.md)、開発とテストは [CONTRIBUTING.md](CONTRIBUTING.md)、バージョン間の変更は [CHANGELOG.md](CHANGELOG.md) を参照してください。

## 謝辞

- [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness): DS Bot は DSH のプラグインシステム上に構築されています。各 bot は DSH セッションであり、DSH のツールとモデルを利用します。
- [esbuild](https://esbuild.github.io/): プラグインのインターフェースコードをバンドルします。
- 以下のプロジェクトが公開しているアイデアに感謝します。DS Bot はその設計思想を参考にしていますが、コードは含んでいません。
  - [AgentMemoryRepo](https://github.com/AgentMemoryRepo/agentmemoryrepo): Bot メモリの Markdown 形式。
  - [OpenAI Codex](https://github.com/openai/codex): 圧縮時にユーザーの元メッセージを要約の近くに残す方法、およびチャット検索のメッセージアンカー。
  - [OpenMausBot](https://github.com/milind-soni/OpenMausBot): グループチャットのラウンド進行と @mention リレー。
  - [Hermes Agent](https://github.com/NousResearch/hermes-agent) と [Hermes Bot Mode](https://github.com/NousResearch/Hermes-Bot-Mode): グループチャットでメンバーごとにセッションを分ける方式、および過去のユーザーメッセージを引き継ぐハンドオフ。
  - [OpenCode](https://github.com/sst/opencode)、[goose](https://github.com/block/goose)、[pi](https://github.com/badlogic/pi-mono)、[Gemini CLI](https://github.com/google-gemini/gemini-cli): 長いチャットをいつ要約するか、そしてハンドオフノートに何を含めるか。
  - [obelisk](https://github.com/tommy0103/obelisk): SQLite 全文インデックスを使ったチャット検索。
- DS Bot を試し、質問し、バグ報告をしてくれるすべての方々。

## ライセンス

[Apache License 2.0](LICENSE)。現状のまま（"as is"）提供され、いかなる保証もありません。サードパーティコードとそのライセンスは [NOTICE](NOTICE) に記載しています。

## 免責事項

DS Bot は独立したコミュニティプロジェクトです。**DeepSeek の公式製品ではなく**、DeepSeek との提携・承認・スポンサー関係はありません。“DeepSeek”“DeepSeek Harness” などの名称はそれぞれの所有者の商標であり、ここではこのプラグインが何と連携するかを説明する目的でのみ使用しています。

bot はあなた自身のモデル利用枠を消費し、依頼に応じてファイルの読み書きやコマンド実行を行います。重要な操作は必ず自分で確認してください。

# ai-workspace

Claude Code を使った AI 駆動開発環境をセットアップするためのツールキットです。

## ディレクトリの概念

このツールキットでは **WORKSPACE_DIR** と **PROJECT_DIR** という 2 つのディレクトリ概念を区別しています。

| 概念 | 説明 |
|---|---|
| **WORKSPACE_DIR** | Claude Code を実行するカレントディレクトリ（CWD）。`.ai-agent/` や `.claude/skills/` などの設定ファイルはここに配置される |
| **PROJECT_DIR** | 実際のソースコードが格納されている Git リポジトリのルート |

- WORKSPACE_DIR 直下に `.git/` がある場合、PROJECT_DIR は `.`（同一ディレクトリ）になります
- WORKSPACE_DIR 直下に `.git/` がない場合、サブディレクトリ内の Git リポジトリが PROJECT_DIR として検出されます
- 複数の Git リポジトリが存在する場合は、セットアップ時にどれを対象とするか確認されます

この設計により、1 つのワークスペースから複数プロジェクトを管理したり、ソースコードと AI 設定ファイルを分離して管理することができます。

## 使い方

### 初期セットアップ

`/autodev-init` スキルを実行すると、対話的にプロジェクトの開発環境を構築できます。具体的には：

1. プロジェクトの情報をヒアリング（概要、技術スタック、開発フェーズなど）
2. `.ai-agent/` ディレクトリに戦略ドキュメント（steering docs）を生成
3. 開発ワークフロー用のスキル群を `.claude/skills/` にインストール
4. `CLAUDE.md`、`README.md`、`LICENSE` を整備

### インストールされるスキル

セットアップ後、以下のスキル（スラッシュコマンド）が使えるようになります：

| コマンド | 用途 |
|---|---|
| `/autodev-start-new-task` | 個別タスクの開始 |
| `/autodev-start-new-project` | 長期プロジェクトの開始 |
| `/autodev-start-new-survey` | 技術調査の開始 |
| `/autodev-create-pr` | PR の作成 |
| `/autodev-create-issue` | GitHub Issue の作成 |
| `/autodev-review-pr` | PR のコードレビュー |
| `/autodev-import-review-suggestions` | レビュー指摘の取り込み |
| `/autodev-replan` | ロードマップの再策定 |
| `/autodev-steering` | Steering ドキュメントの更新 |
| `/autodev-discussion` | アイデアの対話的な整理 |
| `/autodev-switch-to-default` | デフォルトブランチへの切り替え |

### 始め方

このワークスペースで開発したいプロジェクトがあれば、`/autodev-init` を実行してセットアップを開始してください。プロジェクトの概要を対話的にヒアリングしながら、AI エージェントによる開発に必要なドキュメントとスキルを一括で整備します。

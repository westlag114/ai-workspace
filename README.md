# ai-workspace

Claude Code を使った AI 駆動開発環境をセットアップするためのツールキットです。

## ディレクトリ構成と使い方

このツールキットでは **WORKSPACE_DIR** と **PROJECT_DIR** を分離する構成を採用しています。

| 概念 | 説明 |
|---|---|
| **WORKSPACE_DIR** | Claude Code を実行するカレントディレクトリ（CWD）。AI 設定ファイル（`.ai-agent/`、`.claude/`）を配置する場所 |
| **PROJECT_DIR** | 実際のソースコードが格納されている Git リポジトリ。WORKSPACE_DIR のサブディレクトリとして配置する |

### セットアップ手順

#### 1. このリポジトリを clone する

```bash
git clone https://github.com/your-org/ai-workspace.git
cd ai-workspace
```

#### 2. 開発対象のプロジェクトを clone する

ワークスペース内に、開発したいプロジェクトのリポジトリを clone します。

```bash
# 例: my-app を開発する場合
git clone https://github.com/your-org/my-app.git

# 複数プロジェクトを扱う場合は並べて clone
git clone https://github.com/your-org/my-api.git
```

#### 3. Claude Code を起動して `/autodev-init` を実行する

ワークスペースのルート（`ai-workspace/`）で Claude Code を起動し、`/autodev-init` を実行します。
`my-app/` が PROJECT_DIR として自動検出され、対話的にセットアップが進みます。

> **注意**: `/autodev-init` で生成される `.ai-agent/`、`.claude/skills/`、`CLAUDE.md` などの AI 設定ファイルはワークスペースのローカルファイルです。プロジェクト側のリポジトリには影響しません。

#### セットアップ後のディレクトリ構成

```
my-workspace/                  ← WORKSPACE_DIR（CWD）
├── .ai-agent/                 ← AI 設定（ワークスペースに配置）
│   ├── steering/
│   │   ├── product.md
│   │   ├── tech.md
│   │   ├── market.md
│   │   └── work.md
│   ├── structure.md
│   ├── projects/
│   ├── tasks/
│   └── surveys/
├── .claude/
│   └── skills/                ← スキル定義（ワークスペースに配置）
│       ├── autodev-start-new-task/
│       ├── autodev-create-pr/
│       └── ...
├── CLAUDE.md
├── README.md
└── my-app/                    ← PROJECT_DIR（ソースコード）
    ├── .git/
    ├── src/
    ├── package.json
    └── ...
```

### なぜ分離するのか

- **ソースコードを汚さない**: AI 設定ファイルはワークスペース側に置くため、プロジェクト本体のリポジトリに変更が入らない
- **複数プロジェクトの管理**: 1 つのワークスペースに複数の PROJECT_DIR を配置して、横断的に作業できる
- **Git 管理不要**: ワークスペース自体は Git 管理しないため、セットアップが簡単でプロジェクト側の履歴を汚さない

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

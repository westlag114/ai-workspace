# ai-workspace

Claude Code を使った AI 駆動開発環境をセットアップするためのツールキットです。

## ディレクトリ構成と使い方

このツールキットでは **WORKSPACE_DIR** と **PROJECT_DIR** を分離する構成を採用しています。

| 概念 | 説明 |
|---|---|
| **WORKSPACE_DIR** | Claude Code を実行するカレントディレクトリ（CWD）。AI 設定ファイル（`.ai-agent/`、`.claude/`）を配置する場所 |
| **PROJECT_DIR** | 実際のソースコードが格納されている Git リポジトリ。WORKSPACE_DIR のサブディレクトリとして配置する |

### 具体例：セットアップ手順

#### 1. ワークスペースを作成する

```bash
mkdir my-workspace && cd my-workspace
git init   # ワークスペース自体を Git 管理する
```

#### 2. 開発対象のプロジェクトをサブディレクトリに配置する

```bash
# 既存リポジトリを clone する場合
git submodule add https://github.com/your-org/my-app.git

# または既存のローカルリポジトリをサブモジュールとして追加
git submodule add /path/to/local/my-app
```

#### 3. このツールキットのスキルをコピーする

```bash
# claude-code/skills/ を .claude/skills/ としてコピー、または
# /autodev-init の実行時に自動でインストールされます
```

#### 4. `/autodev-init` を実行する

Claude Code をワークスペースのルートで起動し、`/autodev-init` を実行します。
`my-app/` が PROJECT_DIR として自動検出され、以下のような構成が生成されます：

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
- **設定の独立管理**: ワークスペースとプロジェクトを別々にバージョン管理できる

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

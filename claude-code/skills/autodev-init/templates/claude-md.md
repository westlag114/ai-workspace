# {プロジェクト名}

## ディレクトリ構成

このワークスペースは以下の 2 ディレクトリで構成されています。

| ディレクトリ  | パス            | 内容                                                      |
| ------------- | --------------- | --------------------------------------------------------- |
| WORKSPACE_DIR | `.`（CWD）      | `.ai-agent/`, `.claude/skills/`, `CLAUDE.md`, `README.md` |
| PROJECT_DIR   | `{PROJECT_DIR}` | ソースコード、`.git/`, `package.json` 等                  |

- **git / gh コマンド**: `git -C {PROJECT_DIR} ...` / `cd {PROJECT_DIR} && gh ...`
- **`.ai-agent/` や `.claude/skills/`**: WORKSPACE_DIR（CWD）にある

## AI エージェント向けドキュメント

このリポジトリでは `.ai-agent/` ディレクトリに AI エージェント向けのドキュメントを管理しています。

- `.ai-agent/steering/` - プロダクト・技術戦略ドキュメント
- `.ai-agent/structure.md` - ディレクトリ構造の説明
- `.ai-agent/tasks/` - タスク管理
- `.ai-agent/projects/` - プロジェクト管理
- `.ai-agent/surveys/` - 技術調査

タスクに着手する前に、関連する steering ドキュメントと structure.md を確認してください。

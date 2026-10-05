# CLAUDE.md

## プロジェクト概要

このリポジトリはタスクボードアプリケーションのプロジェクトです。実装前に既存のコード、設定、ドキュメントを確認し、採用済みの技術スタックや設計方針があればそれに従ってください。まだ決まっていない事項を既定の事実として扱わないでください。

## 技術スタック

| 分類 | 採用技術 |
| --- | --- |
| UI | React 19（関数コンポーネント + Hooks） |
| 言語 | TypeScript 6 |
| ビルド・開発サーバー | Vite 8（`@vitejs/plugin-react`） |
| lint | oxlint（`.oxlintrc.json`、react / typescript / oxc プラグイン） |
| スタイル | プレーン CSS（コンポーネントごとの CSS ファイル + `src/index.css` の CSS 変数） |
| 状態管理・永続化 | `useState` + `localStorage`（キー: `task-board:tasks`） |
| ホスティング | GitHub Pages（GitHub Actions でデプロイ） |

- 外部の UI ライブラリ、状態管理ライブラリ、テストフレームワークは現時点で未導入です。導入する場合は事前に確認してください。
- `tsconfig.app.json` で `verbatimModuleSyntax` が有効なため、型のみの import は `import type` を使ってください。

### コマンド

- `npm run dev`: 開発サーバーの起動（http://localhost:5173/task-board/）
- `npm run lint`: lint
- `npm run build`: 型チェック（`tsc -b`）+ 本番ビルド（出力先: `dist/`）
- `npm run preview`: ビルド結果のプレビュー

## コンポーネントの命名規約

現在のコード（`src/App.tsx`）に合わせ、以下に従ってください。

- **コンポーネント**: PascalCase の関数宣言で定義し（例: `function App()`）、ファイル名もコンポーネント名と同じ PascalCase の `.tsx` にする（例: `App.tsx`）。1 ファイル 1 コンポーネントを基本とし、`export default` でエクスポートする。
- **スタイル**: コンポーネントと同名の CSS ファイルを隣に置き（例: `App.css`）、コンポーネントから import する。
- **CSS クラス名**: kebab-case（例: `task-form`, `task-list`）。状態は修飾クラスで表す（例: `task completed`）。
- **型**: PascalCase の `type` エイリアスで定義する（例: `type Task`）。
- **イベントハンドラー・関数**: 動詞から始まる camelCase（例: `addTask`, `toggleTask`, `deleteTask`, `loadTasks`）。
- **型ガード**: `is` + 型名（例: `isTask`）。
- **モジュールレベルの定数**: UPPER_SNAKE_CASE（例: `STORAGE_KEY`）。
- **コードスタイル**: シングルクォート、セミコロンなし、インデントはスペース 2 つ。
- **UI テキスト**: 画面上の文言とアクセシビリティ用ラベル（`aria-label`）は日本語で記述する。

## デプロイ先

- **GitHub Pages**: https://ark-kenta-miyazato.github.io/task-board/
- リポジトリ: https://github.com/ark-kenta-miyazato/task-board
- `main` ブランチへの push で GitHub Actions（`.github/workflows/deploy.yml`）が lint・ビルドを行い、`dist/` を GitHub Pages へデプロイします。
- リポジトリ名のサブパスで配信されるため、`vite.config.ts` の `base` は `'/task-board/'` です。リポジトリ名や公開パスを変える場合は `base` も合わせて変更してください。
- GitHub のリポジトリ設定で Pages の Source を **GitHub Actions** にしています。

## 開発方針

- 依頼された範囲に絞って変更し、既存の構成や命名規則を尊重してください。
- 変更前に関連する実装とテストを確認し、原因に対する最小限の修正を行ってください。
- 既存のテスト、lint、型チェックなど、プロジェクトで定義されている検証を実行してください。実行できない場合は理由を報告してください。
- 秘密情報、認証情報、個人情報をコードやコミットに含めないでください。
- 無関係なユーザー変更を上書き、削除、巻き戻ししないでください。
- 必要に応じて、動作や設定に影響する変更に合わせてドキュメントを更新してください。

## Git・GitHub 運用ルール

- **コードを変更するたびに、その変更をコミットし、GitHub の現在の作業ブランチへプッシュしてください。** 作業の最後まで push を保留しないでください。
- push 前に差分を確認し、可能な範囲で関連するテストやチェックを実行してください。
- コミットメッセージには変更内容が分かる簡潔な説明を記載してください。
- 既存の作業ブランチを使用し、明示的な依頼なしにブランチを作成・切り替えたり、履歴を書き換えたりしないでください。
- ユーザーの未コミット変更を含めたり、上書きしたりしないよう、コミット対象を確認してください。
- リモート未設定、認証失敗、競合などで push できない場合は、変更を失わない形で状況を伝え、push が完了したと報告しないでください。
- force push や破壊的な Git 操作は、明示的な依頼がない限り行わないでください。

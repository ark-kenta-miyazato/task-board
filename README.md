# タスクボード

React で作成したシンプルなタスク管理アプリです。

## 機能

- テキスト入力でタスクを追加
- チェックボックスで完了・未完了を切り替え
- タスクを削除
- 完了済みのタスクはグレー（取り消し線付き）で表示

タスクはブラウザの localStorage（キー: `task-board:tasks`）に保存されるため、ページを再読み込みしても残ります。

## 技術スタック

- React 19 + TypeScript
- Vite
- oxlint

## 使い方

```sh
npm install      # 依存関係のインストール
npm run dev      # 開発サーバーの起動
npm run lint     # lint
npm run build    # 型チェック + 本番ビルド
npm run preview  # ビルド結果のプレビュー
```

`vite.config.ts` で `base: '/task-board/'` を指定しているため、開発サーバーは http://localhost:5173/task-board/ で開きます。

## GitHub Pages への公開

`main` ブランチへの push をきっかけに、GitHub Actions（`.github/workflows/deploy.yml`）が lint・ビルドを行い、GitHub Pages へデプロイします。

初回のみ、GitHub のリポジトリ画面で **Settings → Pages → Build and deployment → Source** を **GitHub Actions** に設定してください。

公開 URL: https://ark-kenta-miyazato.github.io/task-board/

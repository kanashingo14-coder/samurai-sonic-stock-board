# SAMURAI SONIC 在庫ボード

物販ブース用のリアルタイム在庫ステータス表示サイトです。GitHub Pages で公開し、在庫データと更新権限は Supabase（Postgres + Auth）で管理しています。

## 構成

- `index.html` — お客様用／スタッフ用の両画面。単一の静的ファイルで、JS 内で画面を出し分けています。
- `images/` — 商品画像（17点）。

## データと認証

- 在庫データは Supabase の `stock_items` テーブルに保存されており、お客様画面はこれを読み取り専用（anon）で表示します。在庫の変更は Supabase Realtime で即座に全画面へ反映されます。
- スタッフが在庫を編集するには、ページ下部の注意書きを**3秒間長押し**（スマホ向け）または**10回連続クリック**（PC向け）すると、ログイン用のフォームが開きます。ここでの認証は Supabase Auth（メールアドレス＋パスワード）で行われ、サーバー側の Row Level Security により、ログインしていない人は在庫を更新できません。
- スタッフ用アカウントは Supabase ダッシュボードの「Authentication → Users」から作成・管理してください。

## 公開方法

このリポジトリを GitHub Pages で公開すると、`index.html` がそのままサイトとして表示されます（リポジトリの Settings → Pages → Source を「main ブランチ / ルート」に設定）。

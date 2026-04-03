# コントリビューションガイド

## ブランチ運用

- 執筆・修正はセクション単位または担当者単位でブランチを切る
- ブランチ名の例: `feature/chapter-2`, `fix/typo-intro`, `update/v2-research`
- PRを立ててmainにマージする（カジュアルな運用 — 承認必須ルールなし）
- mainは常にクリーンな状態を保つ

## タグ運用ルール

**重要: 一度打ったタグは絶対に削除しない。**
過去バージョンへの参照URL（`blob/vN/report/main.md`）や、調査資料からのリンクが壊れるため。

### タグの打ち方

リリース準備が完了した時点で打つ。

```bash
git tag v1
git push origin v1
```

タグは単純連番: `v1`, `v2`, `v3`, ...

### リリースフロー

1. `report/main.md` を更新していく（PRベース）
2. 内容が固まったら `changelog/vX-to-vY.md` を書く
3. `README.md` のバージョン・発行日・更新履歴テーブルを更新する
4. `report/main.md` のフロントマター（version, date）を更新する
5. Gitタグ `vY` を打つ → GitHub Actionsが走りPDFが生成される
6. GitHub Releasesにタグが紐づき、PDFが添付される

## ファイル運用ルール

- `report/main.md` は**常に1つのファイルを上書き更新**する。バージョン別にファイルを分けない
- 過去バージョンはGitタグ経由で参照する
- 調査資料 `research/` はバージョンごとにフォルダを分けて蓄積する（例: `research/v1/`, `research/v2/`）

## バージョン情報の更新箇所

バージョンアップ時は以下の**2箇所**を必ず同時に更新する。

1. `README.md` の冒頭（最新版表記）と更新履歴テーブル
2. `report/main.md` のYAMLフロントマター（version, date）

# Issue Label Design

GitHub Issueで学習課題を分類するためのラベル設計です。
フォーク後にラベルを作成・更新する場合は、`config/labels.json` をもとに `npm run sync-labels` を実行します。

## 教科

- `subject:math`: 数学
- `subject:english`: 英語
- `subject:japanese`: 国語
- `subject:science`: 理科
- `subject:social`: 社会
- `subject:programming`: プログラミング

## 学習タイプ

- `type:concept`: 概念理解
- `type:practice`: 演習
- `type:mistake`: 間違いレビュー
- `type:review`: 復習
- `type:test-prep`: テスト準備
- `type:writing`: 記述、作文、小論文
- `type:question`: 会話中の問題提起、仮説、確認したい論点

## 状態

- `status:ready`: 着手可能
- `status:blocked`: 何がわからないか整理が必要
- `status:reviewing`: 添削、振り返り中
- `status:done`: 完了済み

## ポートフォリオ

- `portfolio:show`: 学習ポートフォリオに掲載する
- `portfolio:hide`: 学習ポートフォリオには掲載しない

## 必要な支援

- `needs:hint`: ヒントが必要
- `needs:explanation`: 解説が必要
- `needs:practice`: 類題が必要
- `needs:review`: 添削が必要
- `needs:memorization`: 暗記、定着が必要
- `needs:teacher-check`: 人間の先生や保護者の確認が必要

## 難易度

- `difficulty:easy`: 基礎
- `difficulty:medium`: 標準
- `difficulty:hard`: 応用

## 注意

- `risk:answer-spoiler`: すぐに答えを見ると学習効果が下がる
- `risk:exam`: テスト、受験、成績に関係する重要テーマ
- `risk:needs-human-teacher`: AIだけで判断しない方がよい内容

## Close方針

- `close:on-understood`: 自分の言葉で説明できたらClose
- `close:on-reviewed`: 添削と振り返りが済んだらClose
- `close:on-practice`: 類題で確認できたらClose

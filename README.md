# Codex Study Harness

Codexを学校の勉強に使うための学習ハーネスです。

このプロジェクトでは、GitHub Issueを「学習課題」として使い、Codex / Copilotとの会話を通じて、目標、理解、間違い、演習、振り返り、復習計画を残します。

このリポジトリは、個別の学習成果物を入れていない初期状態のハーネスとして使えます。フォークした人は、自分の学習Issueと `learning-log/` の記録を追加して使います。

## 何をするためのものか

AIに答えだけを出してもらうのではなく、次のことを管理します。

- 何を理解したいのか
- 今どこまでわかっているのか
- どこで詰まっているのか
- どのように考えたのか
- どこを間違えたのか
- どう解き直したのか
- 次に何を復習するのか

## 基本の使い方

1. このリポジトリをフォークする。
2. ローカルで `npm install` と `npm run check` を実行し、ハーネスが壊れていないことを確認する。
3. GitHub CLIを使う場合は `npm run sync-labels` で学習用ラベルを作成・更新する。
4. 学習者がCodexに疑問、問題提起、間違い、レポートテーマを書く。
5. Codexが既存Issueに続けるか、新しいIssueを作るかを判断する。
6. CodexがIssueに、学習テーマ、目的、現在の理解、わからないこと、自分で考えたことを記録する。
7. Codexと会話しながら、ヒント、添削、解説、類題を進める。
8. 重要な気づき、仮説、誤解、根拠確認、確認問題の結果をIssueコメントに追記する。
9. 学習後、`learning-log/` に振り返りを残す。
10. 類題または確認問題で理解を確認する。
11. 次回復習日や次のIssue候補を書く。
12. 完了条件を満たしたら、学習ブランチを `main` へ合流してからIssueをCloseする。

## 自動記録の考え方

このハーネスでは、学習者が「これがわからない」「この視点を入れたい」「この説明で合っているか」などと問題提起したら、Codexがその内容をIssueに記録します。

記録先は次のように決めます。

- 進行中の同じテーマがある場合: 既存Issueにコメントを追加する。
- 新しいテーマの場合: 新しいIssueを作成する。
- 間違いの原因分析が中心の場合: 間違いレビューIssueにする。
- まだテーマが曖昧な場合: Codexが短く確認してからIssue化する。

詳しい運用は `docs/auto-recording-workflow.md` を確認します。

記録するときは、単に「何を聞いたか」だけでなく、次の変化を残します。

- 最初はどう考えていたか
- 何を確認して見方が変わったか
- どの知見を得たか
- 次に似た問題で使える判断基準は何か

目標は、あとから読んだときに「この学習者はここで見方が変わったのか」とわかる学習履歴にすることです。
詳しい確認観点は `docs/insight-capture-checklist.md` にあります。

## Issueの種類

- 学習課題: 新しく理解したいテーマ。
- 間違いレビュー: 間違えた問題を分析して、再発防止する。
- 復習: 以前学んだ内容を確認する。
- テスト準備: 定期テストや模試に向けた確認。

## Codexの使い方

Codexに依頼するときは、モードを指定すると進めやすくなります。

学習を始める合図として、次のように入力できます。

```text
ハーネススタート
```

`ハーネス開始`、`学習ハーネスを始めて`、`このテーマでハーネスを使いたい` のように、開始したいニュアンスがわかる表現でも始められます。
この合図を出すと、Codexは学習ハーネスを開始し、教科、テーマ、現在の理解、わからないこと、自分で考えたこと、希望する学習モードを確認します。
すでに問題文やテーマを書いている場合は、不足している項目だけ確認し、Issue化や学習ログ化を前提に進めます。
開始時には、最初のIssueまたは最初のIssueコメントに `問題提起`、`学習者の仮説・考え`、`次の確認問題` を必ず残します。
これは、思考ループの1周目を開始直後から記録するためです。
まだ自分の考えが出ていない場合は、仮説を勝手に作らず「未確認」と記録し、最初の確認問題で自分の予想を書いてもらいます。
テーマまたはIssue番号が決まったら、Codexは日付と内容がわかる学習用ブランチを作成します。

```text
study/YYYYMMDD-topic-slug
study/YYYYMMDD-issue-N-topic-slug
```

例:

```text
study/20260512-linear-function
study/20260512-issue-12-english-reading
```

ブランチ作成前に未コミット変更がある場合は、勝手に巻き戻さず、どう扱うかを確認します。

学習を終えるときは、次のように入力できます。

```text
ハーネス終了
```

`ハーネス完了`、`この学習を終わりにしたい`、`Issueを閉じて次に進みたい` のように、終了したいニュアンスがわかる表現でも終了処理に入ります。
この合図を出すと、Codexは現在の学習について、確認問題の結果、思考の変化、得た知見、次回復習がそろっているか確認します。
条件を満たしていれば、Issueに終了コメントを追記し、必要に応じて `learning-log/` を更新し、変更をコミットまたはPR化します。
その後、学習ブランチを `main` へ合流してからIssueをCloseし、Codexは `main` に戻って次の課題候補を出します。
PR本文に `Closes #<Issue番号>` を入れる場合は、PRがmergeされた時点でIssueが自動Closeされ、そのCloseイベントでGitHub Pagesのデプロイが始まります。
不足がある場合はIssueを閉じず、Close前に必要な最小アクションを提示します。

終了条件を満たした学習では、Codexはあわせて思考深化HTMLを生成します。
これは全Issueを集計する `index.html` ではなく、その回の学習だけを中学生にも読みやすくまとめる終了時レポートです。
「問い」「予想」「考え直し」「気づき」「次に使うこと」を、点数ではなく思考の道すじとして表示します。

Issueから作る場合:

```powershell
npm run harness:end-report -- --issue <Issue番号>
```

学習ログやレポートMarkdownから作る場合:

```powershell
npm run harness:end-report -- --source learning-log/YYYY-MM-DD-topic.md
```

出力先は既定で `public/thinking-depth.html` です。
`public/` は `.gitignore` に入っているため、通常は表示確認用の生成物として扱います。

GitHub Pagesで見られるようにする場合は、`Portfolio` workflowへIssue番号を渡します。
通常は、ハーネス終了時に学習ブランチを `main` へ合流してからIssueをCloseすると、`Portfolio` workflow が自動で起動し、Pagesへ反映されます。
Issue closeイベントのワークフローは `main` の内容を使うため、学習ログやレポート生成コードがブランチに残ったままIssueをCloseしないでください。
終了時の順序は「main合流後にIssueをClose」です。
手動で再生成したい場合だけ、次を実行します。

```powershell
gh workflow run portfolio.yml -f issue_number=<Issue番号>
gh run watch
```

ワークフローは `public/index.html` の全体ダッシュボードに加えて、次の2つをPages artifactに含めます。

- `thinking-depth.html`: 最新の終了時レポート
- `thinking-depth/issue-<Issue番号>.html`: Issue別に残る固定レポート

公開URLの例:

```text
https://<owner>.github.io/<repo>/thinking-depth.html
https://<owner>.github.io/<repo>/thinking-depth/issue-<Issue番号>.html
```

```text
ヒントモードでお願いします。
まだ答えは出さずに、考える順番だけ教えてください。
```

```text
添削モードでお願いします。
この解答のどこが間違っているか、理由も含めて見てください。
```

```text
振り返りモードでお願いします。
今日の学習ログに残す内容を整理してください。
```

Issueへの記録を明示したいときは、次のように依頼します。

```text
この疑問をIssueに記録して、学習履歴として残してください。
```

```text
今の仮説と確認結果を、進行中のIssueに追記してください。
```

この用途のプロンプトは `prompts/auto-issue-recorder.md` にあります。

## 最初に試すおすすめテーマ

まずは1教科、1テーマだけで試すのがおすすめです。

例:

- 数学: 一次関数の文章題
- 英語: 長文読解で設問の根拠を探す
- 国語: 説明文の要旨をまとめる
- 理科: 電流と電圧の関係
- 社会: 歴史の出来事を因果関係で説明する

## 完了の目安

Issueを閉じる前に、以下を確認します。

- 自分の言葉で説明できる。
- 間違えた理由がわかっている。
- 類題を1問以上解いた。
- 次に復習する内容が決まっている。

## 品質チェック

このリポジトリには、学習履歴の品質を守るための軽量CIがあります。

```powershell
npm install
npm run check
```

CIでは、主に次を確認します。

- GitHub IssueテンプレートとワークフローのYAML構文が壊れていないか。
- 必須ドキュメントやプロンプトが存在するか。
- 学習ログに、問題提起、思考の変化、なるほどポイント、得た知見、次に使える判断基準などの必須見出しがあるか。
- 学習ログの確認問題が未実施のまま残っていないか。
- PRテンプレートや振り返りテンプレートに、知見を残す欄があるか。

GitHub Actionsでは、pull request と main への push で同じチェックを実行します。

GitHubラベルを初期化する場合は、GitHub CLIでログインしたうえで実行します。

```powershell
gh auth login
npm run sync-labels
```

## 思考の軌跡ダッシュボード

GitHub Issueの蓄積から、`public/index.html` にAI時代の学習評価ページを生成できます。
これは作品集としてのポートフォリオではなく、学習者がどのように思考の深さに至ったかを、中学生にも読める形でたどるための「思考の道すじ」ダッシュボードです。
生成されるHTMLのUI、評価ラベル、説明文は日本語で表示します。
Issue本文や学習者本人の言葉は、証拠性を保つため原文のまま表示します。
現在の公開HTMLは、難しい理論名や点数ではなく、問い、予想、確認、考え直し、気づき、次に使うことの順番で表示します。
掲載したいIssueには `portfolio:show` ラベルを付けます。
公開したくないIssueには `portfolio:hide` ラベルを付けます。

このリポジトリでは、GitHub Pagesの公開元を `GitHub Actions` にする前提です。
`public/index.html` はワークフロー実行時に生成される公開用成果物であり、通常はcommitしません。

初回設定:

1. GitHubの `Settings → Pages → Build and deployment → Source` を `GitHub Actions` にする。
2. ラベルを同期する。
3. 公開したいIssueに `portfolio:show` ラベルを付ける。
4. `Actions → Portfolio → Run workflow` を実行する。
5. ワークフロー完了後、PagesのURLを確認する。

ラベルを同期する場合:

```powershell
npm run sync-labels
```

ローカルで生成する場合:

```powershell
npm run build:portfolio
```

ローカル生成は表示確認用です。
生成された `public/` は `.gitignore` に入っているため、通常のcommit対象にはなりません。

生成される内容:

- ページ全体の読み方
- 掲載された学習数、完了した学習数、道すじがはっきり読める学習数
- 最新Issueの思考の道すじ
- Issueごとの「問い」
- Issueごとの「予想」
- Issueごとの「確認」
- Issueごとの「考え直し」
- Issueごとの「気づき」
- Issueごとの「次に使うこと」
- Issue原文へのリンク

ここで見るのは点数ではありません。
対象者が「何を疑問に思ったか」「自分ではどう予想したか」「何で確かめたか」「どこで考え直したか」「何に気づいたか」「次にどう使える形にしたか」を、順番に読めるようにすることが目的です。

GitHub Actionsから手動生成する場合:

1. GitHubの `Actions` タブを開く。
2. `Portfolio` ワークフローを選ぶ。
3. `Run workflow` を押す。
4. Actions内で `public/index.html` が生成される。
5. `public/` がPages artifactとしてアップロードされる。
6. GitHub Pagesにデプロイされる。

GitHub Pagesで公開する場合は、GitHubの設定で次を選びます。

```text
Settings
→ Pages
→ Build and deployment
→ Source: GitHub Actions
```

PublicリポジトリでPages公開する場合、掲載された学習内容は外部から見える状態になります。
個人情報、学校名、成績、課題本文などを含むIssueには `portfolio:show` を付けないでください。

## ディレクトリ

```text
.
├─ AGENTS.md
├─ README.md
├─ .github/ISSUE_TEMPLATE/
├─ docs/
├─ goals/
├─ learning-log/
├─ prompts/
├─ scripts/
└─ config/
```

## 注意

このプロジェクトは、AIに宿題を代行させるためのものではありません。
学習者自身の思考、途中式、説明、振り返りを残すことを目的にします。

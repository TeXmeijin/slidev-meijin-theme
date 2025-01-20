---
theme: './theme'
title: 2年間開発を続けているテストメーカー立ち上げ時の技術選定と振り返り
info: |
  ## Slidev Starter Template
highlighter: shiki
drawings:
  persist: false
transition: slide-left
mdc: true
layout: cover
colorSchema: light
fonts:
  # basically the text
  sans: M PLUS 2
  # use with `font-serif` css class from UnoCSS
  serif: Robot Slab
  # for code blocks, inline code, etc.
  mono: Fira Code
  weights: 200, 400, 700
---

# 2年間開発を続けている<br>テストメーカー立ち上げ時の<br>技術選定と振り返り

## 株式会社NoSchool CTO meijin

---

# アジェンダ

- 自己紹介
- テストメーカーの紹介
- テストメーカーの技術選定
  - Great or Normal or Not-Great
- 個人開発の技術選定Tips

---
layout: section
---

# 自己紹介

---

- 職種・SNS
  - 株式会社NoSchool CTO
    - 2016年〜株式会社LIFULL Webエンジニア
    - 2019年〜株式会社NoSchool CTO
  - Twitter(X): [名人｜マナリンクCTO](https://twitter.com/meijin_garden) 🔍
  - Zenn: https://zenn.dev/meijin 🔍
  - 好きな言語はTypeScript、好きなCSSプロパティはobject-fit
- 趣味
  - 将棋☗、カメラ📸、個人開発💻、ラム酒🥃、筋トレ💪、高校野球観戦⚾、麻雀🀄

<div class="absolute top-12 right-8">
<img class="w-48 h-48 rounded-full" src="https://github.com/TeXmeijin/vite-react-ts-tailwind-firebase-starter/assets/7464929/09bd0b32-0bcc-4f0d-849a-ccfdd46713ba" alt="">
</div>

---
layout: section
---

# テストメーカーの紹介

---

## テストメーカーとは

- 概要
  - 「穴埋めテストを簡単に作れるWebアプリケーション」
  - 「穴埋めテスト」でGoogle1位（多分）🔍🌐
  - https://www.test-maker.app
- 沿革
  - 2022年6月リリース
  - リリースツイートが2,000RT以上、IT Media Newsに掲載📣
  - 2025年1月現在、2万人以上の会員登録。有料版も提供💰
- 主なユーザーは学校の先生、資格受験、企業研修など

---

# マウスやタッチ操作で簡単穴埋めテスト作成＆編集
![画面収録 2025年1月14日 18時46分20秒](https://github.com/user-attachments/assets/4c86b59d-884b-4ec3-964d-88d48ba44336)

---

# 回答URLを配布して、簡単共有

<figure>
<img src="https://github.com/user-attachments/assets/0cab2b65-0ddb-4f63-8356-7b55dc7a63ce" alt="" width="500">
</figure>

<figure class="mt-4">
<img src="https://github.com/user-attachments/assets/96f0b15e-9f89-4af5-98cf-b013db92b93d" alt="" width="500">
</figure>

---
layout: section
---

# テストメーカーの技術選定

---

# 技術選定一覧

※⭐をつけているものをこのあと解説します

- フロントエンド
  - Next.js / Tailwind CSS / ⭐daisyUI / ⭐Slate.js (リッチテキストエディタ) / Vercel
- バックエンド
  - ⭐frourio (Node.jsフレームワーク) / Prisma / PostgresQL / Firebase Auth / ⭐Railway
- その他
  - Sentry / ⭐Posthog / Stripe

---

# daisyUI(https://daisyui.com/)【Great】

Tailwind CSSのコンポーネントライブラリ

```jsx
<details class="dropdown">
  <summary class="btn m-1">open or close</summary>
  <ul class="menu dropdown-content bg-base-100 rounded-box z-[1] w-52 p-2 shadow">
    <li><a>Item 1</a></li>
    <li><a>Item 2</a></li>
  </ul>
</details>
```

<video controls>
  <source src="https://github.com/user-attachments/assets/edca20fa-70c4-4b27-bc3b-ffc0f8390c6c" type="video/mp4">
</video>

---

# daisyUI | 解説

- Dropdownを作るのに、JavaScriptは不要！
  - `<details>`と`<summary>`で実装できる
  - そこにCSSでスタイルを当てれば、見た目はDropdownになる
- 純粋にHTMLとCSSの勉強になるので、GitHub Repoを読むと楽しい
  - CSSしかないので、CSS筋が鍛えられる
- 技術的なメリット
  - Server ComponentsのままでUIが実装できる

---

# Slate.js(https://docs.slatejs.org/)【Not-Great】

- Slate.jsについて
  - 競合としてTiptap、Quill、Editor.js、Lexicalなどがある
  - 長所
    - フルカスタマイズ可能。機能ごとに提供されている
  - 短所
    - バージョンが未だに0系。実態として破壊的変更が多い
    - 実質Plateというラッパーライブラリが必須だが、こちらも破壊的変更が多い

→今から始めるなら、Tiptapをおすすめします

✅「リッチテキストエディタ 基礎」でGoogle1位のこの記事をぜひ！
https://zenn.dev/meijin/articles/rich-text-editor-basis-knowledge

---

# テストメーカーでWYSIWYGエディタを使った理由

- テストメーカーの「マウスで選択したところが穴埋めになる」体験
  - 抽象化すると **「ユーザーの操作をフックに、特定のDOMを別のDOMへ変換する」** が必要
  - WYSIWYGエディタの **「Command+Bでspanをstrongへ変換する」** と一緒！
  - カスタマイズ性の高いWYSIWYGエディタライブラリを利用し、当該機能を実現

![画面収録 2025年1月14日 18時46分20秒](https://github.com/user-attachments/assets/4c86b59d-884b-4ec3-964d-88d48ba44336)

---

# frourio(https://frourio.io/)【Normal】

- Node.jsフルスタックフレームワーク
- 2025年現在もNode.js製FWは乱立
  - 個人的に最有力）Hono, frourio, Nest.js
  - 個人的に有力視）FoalTS, Blitz.js, RedwoodJS
- frourioの特長
  - 関数を中心とした設計。ClassやDecoratorは使わない！

→ただ、テストメーカーのようなWebのみ＆シンプルCRUDなサービスを今から始めるなら、Next.js+Supabaseのみでやります

---

# Railway(https://railway.app/)【Not-Great】

- 概要と長所
  - めっっっちゃ簡単に使えるPaaS。管理画面がイケてる。開発自体は盛ん
  - 料金｜バックエンドサーバーとPostgresQLで月額$20程度
- 欠点：不安定...というか信頼度が微妙というか...
  - 一番酷かったときで深夜3時に落ちて翌日14時頃まで復旧しなかった
  - Discordでサポートがあるが、英語なので正直しんどい
  - 割としばしば大きめのmigrationをやっているようで、DBの再起動したら<br>ストレージがアメリカからシンガポールに勝手に移動＆途中でCancelしたらDBごと落ちたことがある

---

# Posthog(https://posthog.com/)【Great】

- Google Analyticsの代替
  - 価格：有料版もあるが、無料枠も（個人開発なら）十分な量
- 特長
  - とにかくエンジニアフレンドリー
  - トラッキングの実装が簡単＆そこそこモダン
  - データ分析が、SQLライクな独自言語でできる。BIツールがオールインされているイメージ

---

# Posthog | スクショ

- SQLライクにイベントを分析することができる
  - 新機能リリース後、何人がUI上で反応したか？といった、「欲しいデータだけどGAいじりたくないなぁ」みたいなものが分かる

<img src="https://github.com/user-attachments/assets/18c9d7a9-25c4-4896-af76-159bc619d85f" width="510">

---
layout: section
---

# 個人開発の技術選定Tips

---

# 個人開発の技術選定Tips

- 極論、simpleなもの選んでおけば大後悔はしない
  - 例：`Railway`についてNot-Greatと評したが、元々がSimpleですぐ使えるツールなので、個人開発のスピード感には大いに貢献している
- 【そのサービスの勝負どころ】に集中できる選定
  - 例：テストメーカーの最大の勝負どころはカスタマイズされたWYSIWYGエディタ。そのため、Slate.jsは破壊的変更が多いが採用の価値があった
  - 例：daisyUIは、「WYSIWYGエディタ以外を爆速でUI開発しつつ、エディタはページのPerformanceを落としがちなのでUIをできるだけ軽いバンドルサイズで実装したい」を叶えられる

---
layout: cover
---

# ご清聴ありがとうございました！

こちらの記事にプロダクトマネジメントのTipsなども書いています。
<br>
<br>
【テストメーカー 支える技術】で検索🔍
<br>
https://zenn.dev/meijin/articles/personal-development-release-and-paid-story

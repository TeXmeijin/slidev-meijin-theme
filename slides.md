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
- Good技術選定と、他も検討したい技術選定
- 個人開発の技術選定Tips
- まとめ

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

- フロントエンド
  - Next.js / Tailwind CSS with daisyUI / Slate.js (リッチテキストエディタ) / Vercel
- バックエンド
  - frourio (Node.jsフレームワーク) / Prisma / PostgresQL / Firebase Auth / Railway
- その他
  - Sentry / Posthog / Stripe

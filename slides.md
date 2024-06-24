---
theme: './theme'
title: toCスタートアップにおけるDDD・クリーンアーキテクチャ取捨選択集
info: |
  DDDのリアルを話します。 Twitter: @meijin_garden
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

# toCスタートアップにおける<br />DDDの取捨選択

## 株式会社NoSchool CTO / meijin

---

# 目次

1. TL; DR
1. 自己紹介・事業紹介
1. DDDやクリーンアーキテクチャに対するスタンス
1. 実際の取捨選択事例集
1. まとめ

---
layout: section
---

# TL; DR

---

# TL; DR

- DDDやクリーンアーキテクチャに関する議論は「要はバランス」に落ち着きがち
- toCサービスで3年以上設計と向き合ってきた私が「具体的に何を考えてアーキテクチャのバランスを取ってきたか」という事例をまとめる
- よくある取り組みや設計ルールに対して「弊社では無視している」「逆にめっちゃ力を入れている」＆「その理由を事業・プロダクト・組織等々の観点から説明」
- 『DDDやクリーンアーキテクチャ原理主義に従わないことを恐れるな！』

---
layout: section
---

# 自己紹介・事業紹介

---

# 自己紹介

- 職種・SNS
  - 株式会社NoSchool CTO: マナリンク(https://manalink.jp/)の開発
  - Twitter(X): [名人｜マナリンクCTO](https://twitter.com/meijin_garden)
  - Zenn: https://zenn.dev/meijin
  - 好きな言語はTypeScript、好きなHTTPヘッダーはCache-Control
- 趣味
  - 将棋☗、カメラ📸、ラム酒🥃、個人開発💻、筋トレ💪、高校野球観戦⚾
  - 個人開発：テストメーカー(https://test-maker.app/)

<div class="absolute top-12 right-8">
<img class="w-48 h-48 rounded-full" src="https://github.com/TeXmeijin/vite-react-ts-tailwind-firebase-starter/assets/7464929/09bd0b32-0bcc-4f0d-849a-ccfdd46713ba" alt="">
</div>

---

# 事業紹介

- 株式会社NoSchoolについて
  - 2018年創業・2020年にマナリンクをリリース
  - 2024年現在、社員10名超、エンジニア5名
- マナリンクについて
  - オンライン家庭教師が探せるメディア（先生600人超）
  - 授業・売上・宿題等の管理ができるSaaS
  - **『メディア的な機能とSaaS的な機能の両方が大事』**
  - Web（Next.js×Laravel）、アプリ（React Native）

<div class="absolute top-8 right-8">
<img class="w-64" alt="Manalink iPhone 12 Pro.png (1.0 MB)" src="https://img.esa.io/uploads/production/attachments/17780/2024/06/24/104467/8d5243bd-6c9e-4ab5-950d-f7d0d89c50de.png">
</div>

---
layout: section
---

# DDDやクリーンアーキテクチャに対するスタンス

---

# DDDやクリーンアーキテクチャに対するスタンス

1. <span>「オンライン家庭教師」という過去に存在しない＆法的にも固まっていないドメインで事業をやるので **『ドメイン駆動開発』というより『ドメイン作りながら開発』**</span>
2. メディア機能はパフォーマンス重視、SaaS機能はドメインロジック重視
3. 組織が4〜5人と小規模なので、強いルールを決めるより個人が自律的に意思決定できることを重視
4. 創業時からPHP＆Laravelを使っているので、PHPの限界やLaravelのルールとの競合を意識

- 以上から
  - 機能群ごとに、設計で何を求めるかが変わる
  - ある程度以上の「完璧」を求めることのコスパがかなり悪い
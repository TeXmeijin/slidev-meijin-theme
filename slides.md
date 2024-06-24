---
theme: './theme'
title: Welcome to Slidev
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

# スライドタイトル

## スライドサブタイトル

---
layout: section
---

# セクションタイトル

---

# 箇条書きサンプル（ドット）
- 弊チームでもさっそくアーキテクチャの徹底と、外部ライブラリの利用制限で用いた
- あるとき、メンバーが`react.Suspense`のラッパーを作ってくれた
- なので、`Suspense`を直接呼ぶのではなく作ったラッパーを使うように徹底したい

---

# 箇条書きサンプル（数値）

1. あるとき、メンバーが`react.Suspense`のラッパーを作ってくれた
2. なので、`Suspense`を直接呼ぶのではなく作ったラッパーを使うように徹底したい
3. そのため、`react`の中の`Suspense`のみ利用範囲を制限したい

---

# 箇条書き＆コードサンプル

- 「`react`の中の`Suspense`のみ利用範囲を制限したい」ケースには対応できない
- これまで通り設定すると、`react`からのimportが全部NGになってしまう

```js
        {
          "module": "react",
          "allowReferenceFrom": ["src/libs/suspense.ts"],
          "allowSameModule": false
        },
```

---

# ネストした箇条書きサンプル

- あるモジュールから別のモジュールをimportできる・できないのルールを規定する
  - `.eslintrc.js`に設定を書き、破られていたらエラー扱いとする
  - husky/lint-stagedやCIで強制できる
- 利用例1：プロダクトで決めたアーキテクチャの徹底
  - `src/components/page`は`src/pages`から
  - `src/components/features`は`src/pages`から呼べる
  - `src/components/ui`は`src/components/page`、`src/components/features`から呼べる
---
theme: './theme'
title: 弊社の「意識ﾁｮｯﾄ低いアーキテクチャ」10選
info: |
  弊社の「意識ﾁｮｯﾄ低いアーキテクチャ」10選
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

# 弊社の<br>「意識ﾁｮｯﾄ低いアーキテクチャ」<br>10選

## 株式会社NoSchool CTO / meijin

---
layout: section
---

# アジェンダ

---

# アジェンダ

- 自己紹介・事業紹介
- 意識低いアーキテクチャ10選
- まとめ

---
layout: section
---

# 自己紹介

---

- 職種・SNS
  - 株式会社NoSchool CTO
  - 新卒4年目でスタートアップのCTOになって5年経ちました
  - Twitter(X): [名人｜マナリンクCTO](https://twitter.com/meijin_garden)
  - Zenn: https://zenn.dev/meijin
  - 好きな言語はTypeScript、好きなHTTPヘッダーはCache-Control
- 趣味
  - 将棋☗、カメラ📸、ラム酒🥃、個人開発💻、筋トレ💪、高校野球観戦⚾

<div class="absolute top-12 right-8">
<img class="w-48 h-48 rounded-full" src="https://github.com/TeXmeijin/vite-react-ts-tailwind-firebase-starter/assets/7464929/09bd0b32-0bcc-4f0d-849a-ccfdd46713ba" alt="">
</div>

---

# 自己紹介2

- ZennでReact記事が人気
  - Zenn記事で唯一2,000Likes超え！（登壇時点）
- 個人開発
  - テストメーカー（ユーザー数1万5千人以上）
- エンジニア向け教材執筆
  - 「LaravelでFat Controllerをリファクタしよう」
  - 本教材をきっかけに入社した社員有り

<div class="absolute top-4 right-6">
<img  class="w-[380px] border" alt="CleanShot 2024-07-15 at 21.45.36@2x.png (72.4 kB)" src="https://img.esa.io/uploads/production/attachments/17780/2024/07/15/104467/82093c0c-b23d-42f6-a7ed-773b9da30868.png">
</div>
<div class="absolute top-48 right-6">
<img class="w-[380px] border" alt="CleanShot 2024-07-15 at 21.44.59@2x.png (202.4 kB)" src="https://img.esa.io/uploads/production/attachments/17780/2024/07/15/104467/da2af37d-a587-4f11-bbb2-0e0452bf336e.png">
</div>
<div class="absolute top-84 right-6">
<img class="w-[380px] border" alt="CleanShot 2024-07-15 at 21.35.39@2x.png (428.1 kB)" src="https://img.esa.io/uploads/production/attachments/17780/2024/07/15/104467/29c9bd52-0779-4c9e-ac2e-41f0e0990187.png">
</div>

---
layout: section
---

# 本日の内容

---

# 弊社の「意識ﾁｮｯﾄ低いアーキテクチャ」を発表

- **意識低い**のニュアンス例
  - データorサービス規模が膨大になると耐えられないアーキテクチャだが、<br>要件を鑑みると**現実的に膨大にならない**ので採用
  - その道のハイスキルなエンジニアには辛い選定だが、<br>**現メンバーのスキルセットを鑑みる**とこのラインが適切と判断
  - 流行っている技術だけどまだ人柱が世の中的に必要そうなので、<br>**様子見として追従していない**

🍻ほどよいオーバーエンジニアリングを探求していきましょう〜みたいなことを言いたい発表です

---
layout: section
---

# 前提知識

軽めに弊社のサービス概要や状況を説明して、アーキテクチャの話が腹落ちしやすいようにします。

---

# 前提知識

- 弊社のサービス
  - オンライン家庭教師マナリンク（https://manalink.jp）
  - 特性の異なるWebサイトを**マナリンクが包含**しており、アーキテクチャ上の工夫が必要
    - 家庭教師を探せる検索サイト（**toC向けメディアっぽい**）
    - 家庭教師が授業の予定、結果、売上などを管理できるサイト（**toB向けSaaSっぽい**）
- 組織・会社
  - サービス提供開始4年のスタートアップ
  - エンジニアは5名（CTO含む）、全員正社員、出社制
  - 全員フルスタック（**内、弊社からフルスタックになったメンバー3名**）

---

# マナリンクの先生一覧

- 普通の家庭教師会社と違って、先生を指名できちゃうのが特長です！

<div class="flex gap-x-4">
<div class="flex-2">
<img width="600" alt="CleanShot 2024-10-23 at 18.02.47.png (515.8 kB)" src="https://img.esa.io/uploads/production/attachments/17780/2024/10/23/104467/490de198-2687-4d76-bfaa-3edbeef67459.png">
</div>
<div class="flex-1">
<img width="226" alt="CleanShot 2024-10-23 at 18.04.59.png (199.3 kB)" src="https://img.esa.io/uploads/production/attachments/17780/2024/10/23/104467/583b3f1a-a6ca-4bae-9849-6a668d57da1f.png">
</div>
</div>

---
layout: section
---

# さっそく10選を紹介！

## ※バックエンドは【BE】、フロントエンドは【FE】と表記

---

1. **【BE】** 定期バッチや遅延実行はFargateのコンテナをStep Functionsから呼んで済まそう
2. **【BE】** とりあえずControllerからUseCaseは最悪切ろうね
3. **【BE】** PHPだけどPHP Stanのレベルを10段階の6までにしてるよ
4.  **【BE】** Laravelの機能のうち、ORMにあまりにベタベタな機能はそもそも使わないでね
5. **【FE】** Next.jsだけどApp Routerじゃないよ
6. **【FE】** デザインシステムなんて整っていないけどTailwind CSSだよ
7.  **【FE】** WebもアプリもReactだけど、言うほどコード共通化してないよ
8. **【BE/FE】** OpenAPI書かなくていいよ。aspidaでサクッと型付けしちゃおう
9. **【BE/FE】** 高速化がどうしてもしたいページはCloudFrontのSWRキャッシュで済ませるよ
10. **【BE/FE】** 腐敗防止層は適当でもめっちゃ価値あるから積極的に切ろう

---
layout: cover
---

# ①【BE】<br> 定期バッチや遅延実行は<br>Fargateのコンテナを<br>Step Functionsから呼んで済まそう

---

# 前提知識

- マナリンクでは、バックエンド（Laravel）アプリケーションをAWS Fargateで運用

```plantuml
@startuml AWS Architecture

!define AWSPuml https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v18.0/dist
!include AWSPuml/AWSCommon.puml
!include AWSPuml/NetworkingContentDelivery/CloudFront.puml
!include AWSPuml/Containers/Fargate.puml
!include AWSPuml/Containers/ElasticContainerService.puml
!include AWSPuml/General/User.puml
!include AWSPuml/ApplicationIntegration/StepFunctions.puml

!procedure $AWSIcon($service, $line1, $line2="")
rectangle "$AWSImg($service)\n<b>$line1</b>\n$line2"
!endprocedure

skinparam linetype ortho
left to right direction
$AWSIcon(User, " ", "User") as user

CloudFront(cloudfrontAlias, "CloudFront", "api.manalink.jp")
Fargate(fargateAlias, "AWS Fargate", "Laravel Server")

user --> cloudfrontAlias
cloudfrontAlias --> fargateAlias

' ECS TaskをFargate内部に追加
ElasticContainerService(ecsTaskAlias, "ECS Task", "Running Laravel App")

fargateAlias --> ecsTaskAlias

@enduml
```

<div class="mt-4"></div>

- 定期バッチ処理
  - Userへの各種通知や、統計データの生成など
  - バッチ処理のためだけに別Repositoryを切ったり、別言語を使ったり、ドメインロジックを再実装したくない

---

# AWS Step Functionsからアプリケーションと同じECS Taskを起動


```plantuml
@startuml AWS Architecture

!define AWSPuml https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v18.0/dist
!include AWSPuml/AWSCommon.puml
!include AWSPuml/NetworkingContentDelivery/CloudFront.puml
!include AWSPuml/Containers/Fargate.puml
!include AWSPuml/Containers/ElasticContainerService.puml
!include AWSPuml/General/User.puml
!include AWSPuml/ApplicationIntegration/StepFunctions.puml
!include AWSPuml/ApplicationIntegration/EventBridge.puml

!procedure $AWSIcon($service, $line1, $line2="")
rectangle "$AWSImg($service)\n<b>$line1</b>\n$line2"
!endprocedure

skinparam linetype ortho
left to right direction
$AWSIcon(User, " ", "User") as user

CloudFront(cloudfrontAlias, "CloudFront", "api.manalink.jp")
Fargate(fargateAlias, "AWS Fargate", "Laravel Server")
StepFunctions(stepFunctionsAlias, "AWS Step Functions", "Batch Runner")
EventBridge(eventBridgeAlias, "Amazon EventBridge", "Batch Scheduler")

user --> cloudfrontAlias
cloudfrontAlias --> fargateAlias

' ECS TaskをFargate内部に追加
ElasticContainerService(ecsTaskAlias, "ECS Task", "Running Laravel App")

fargateAlias --> ecsTaskAlias
eventBridgeAlias --> stepFunctionsAlias
stepFunctionsAlias --> ecsTaskAlias

@enduml
```

---

# 軽く解説

- AWS Step Functions(Sfn)は多くのAWSサービスをフローチャートの要領で連携できるサービス
- トリガーにEventBridgeを設定でき、Cron式で定期実行が可能。タイムアウトやリトライも設定可
- SfnはECS Task起動時にStdInを指定できるので、定期バッチ名や引数も渡すことができる

以下の例ではJST17時に`php artisan command:introduce-trial-support`を<br>**アプリケーションと同じDockerベースのインスタンス**で実行する

```yaml
        IntroduceTrialSupport:
          Type: Schedule
          Properties:
            Input: '{"commands": ["php", "artisan", "command:introduce-trial-support"]}'
            Schedule: 'cron(0 8 * * ? *)'
```

---

# メリット・意識ﾁｮｯﾄ低いポイント

- メリット
  - アプリケーションと同じドメインロジック・CI・ロギング等が再利用でき、効率的
  - アプリケーションと同じインスタンスでは実行されないため、負荷の高い処理も割と安全
  - AWS SAMを使いYamlベースで実行時刻の設定ができるため、Git管理しやすい
- **意識ﾁｮｯﾄ低いポイント**
  - バッチの同時実行制御など、処理間をまたいだ制御がやりにくい
  - 言語＆FWがLaravel＆PHP縛りになる
  - 起動条件がCronで表現できないくらい複雑だと対応できない
  - 1時間以上といった長時間実行/同時に数十台バッチが立ち上がることなどは想定していない

---
layout: section
---

## ここまで書いて気がついたのですが、このペースで10個解説するとボリュームがヤバそうなのでここから駆け足でいきます！🏃🏃🏃🏃🏃🏃

---
layout: cover
---

# ②【BE】<br> とりあえずControllerから<br>UseCaseは最悪切ろうね

---

# ControllerからUseCaseは最悪切る

- 急に意識が低くなりますが
  - ControllerからUseCaseは最悪切る
  - UseCase(以上)の単位の結合テストは必ず書く
  - DDDで設計していたり、CQRSを採用する機能群もあるが、サービス全体を通して絶対従うべき原則は多くない
- 最悪のラインがそこな理由（**意識が低いポイント！**）
  - Fat Controllerを許容すると、LaravelのORMベッタリ機能の大半が利用可能になる...
  - バックエンド処理が**Web Front、ネイティブアプリ、社内向け管理画面、定期バッチ経由等から呼ばれる**ため、再利用性の担保を考慮するとPresentation層の1つ奥は必須

---
layout: cover
---

# ③【BE】<br> PHPだけどPHP Stanの<br>レベルを10段階の6までにしてるよ

---

# PHPだけどPHP Stanのレベルを6までにしてるよ

- PHPStanとは
  - JavaScriptでいうESLintのような静的解析ツール
  - ASTをベースに所定のルールに沿ったコードかをCLIベースで検証可
  - PHP Docsの内容も考慮し、PHP自身よりリッチな型チェックが可能
  - IDE連携、CI連携
- レベル6とは
  - PHPStanの特異な点として、大まかに10段階のレベルがプリセットで用意
  - 導入時、1から順に上げていったが、5のあたりで厳しすぎて開発効率が落ちてきた
  - 現在は6にカスタム設定を多少加えて運用している（**意識が低いポイント！**）

---
layout: cover
---

# ④【BE】<br> Laravelの機能のうち、<br>ORMにあまりにベタベタな機能は<br>そもそも使わないでね

---

# ちょっと古めなFWのご多分に漏れず、LaravelにもORMベタベタ機能がある

- ORMベタベタ機能例
  - Policy（認可処理。ORMベースで書き込み制御などを行う）
  - Route Model Binding（Controllerの引数に操作対象のORMインスタンスが注入）
  - API Resource（完全にベタベタではないが、ORM依存させると超便利になる）

```php
// 引数にORMが渡ってくるのがRoute Model Binding、返り値がAPI Resource
public function edit(\App\Models\User $user, string $email)
{
    $user->email = $email;
    $user->save();
    $user->refresh();
    return new UserResource($user);
}
```

---

# ORMベタベタ機能を使わない理由

- 一言でいうと
  - テーブル構造が依存する範囲が無駄に広がるから
  - かつ、弊社のアプリケーション特性上、それが辛いことが多いから
- テーブル構造の依存が広がると困ること
  - 同じデータを、機能ごとに別のものとして解釈することが困難になる
    - たとえば「先生の指導コース」は生徒にとっては授業内容の明示、先生にとっては収入源、マナリンクにとってはCtoCのトラブルを防ぐための契約条件明示
    - 機能群によって欲しいデータ、紐づくデータ、Mutationする内容などが異なる
    - これが往々にして**あとから発覚する**のがアプリ開発あるある

---
layout: cover
---

# ⑤【FE】<br> Next.jsだけどApp Routerじゃないよ

---

# Next.jsだけどApp Routerじゃないよ

- Pages Routerを使ってます
  - 2024年10月現在、弊社ではまだPages Routerを利用
- なぜ？
  - 個人開発でApp Routerを入れて軽く検証済み
    - CC限定でよければ気合で移行できるアーキテクチャにはしてある...つもり
  - 細かいところで`revalidateTag`がまだバグったままリリースされているなど、**まだまだ不安定な部分がある**
  - toC向けメディアと授業向け管理画面の両方を単一サービスで運営しており、**複数特性のアプリにおけるベストプラクティスが固まるまで待ちたい**（**意識が低いポイント！**）

---
layout: cover
---

# ⑥【FE】<br> デザインシステムなんて整っていないけど<br>Tailwind CSSだよ

---

# デザインシステムなんて整っていないけどTailwind CSSだよ

- デザインシステムが整っていなくてもTailwind CSSを使って嬉しい場面はある
- たとえばz-indexの管理を**意識低い感じで**できる

```js
// tailwind.config.js
      zIndex: {
        modal: 'var(--z-index-modal)',
        header: 'var(--z-index-header)',
        menu: 'var(--z-index-menu)',
      },
// src/index.css
    --z-index-modal: 110;
    --z-index-header: 105;
    --z-index-menu: 100;
```

---
layout: cover
---

# ⑦【FE】<br> WebもアプリもReactだけど、<br>言うほどコード共通化してないよ

---

# WebもアプリもReactだけど、言うほどコード共通化してないよ

- ReactとReact Nativeは、別物
  - そもそもDOMが異なる
  - 純粋にロジックのみ持っているフックなら共通できるが・・・
  - 要件レイヤーで見ても、Webとアプリが常に一致とは限らない
- ”何”が共通化できている？
  - aspida(次節)/SWRを使ったAPI型定義や状態管理など、基底となる考え方
  - CompositionやHooksの切り方といった設計パターンの共通化
  - （失敗談）同機能をWeb/Appでアサイン割りして事故った。機能ごとにアサインがベスト

---
layout: cover
---

# ⑧【BE/FE】<br> OpenAPI書かなくていいよ。<br>aspidaでサクッと型付けしちゃおう

---

# OpenAPI書かなくていいよ。aspidaでサクッと型付けしちゃおう

- aspidaは、APIの型定義をTSで書くと、APIクライアントが生成されるツール

```ts
export interface Methods {
  get: {
    resBody: {
      is_available: boolean;
    };
  };
}
```

```ts
  // SWRラッパーも提供していて、型安全にAPIを叩ける
  const { data, error, isValidating, mutate: revalidate } = useAspidaSWR(apiClient.available);
  console.log(data.is_available); // boolean type safe
```

---

# OpenAPIを書かない理由

- 工数がかかる上にメリットが小さい
  - 全メンバーがフルスタックのため、FE/BE境界のドキュメント化必須度が低い
  - Mutate寄りのAPIが多く、表面上のDocsよりDomain層のコード読むほうが速い
  - BEがモノリシックなこともあって、エラーハンドリング周りもシンプルな実装でOK
- 欲しい理由があるとしたら
  - APIの設計レビューの統一Formatとして扱うのは魅力的かも

※aspida自体はOpenAPIとのCodegen対応しています。弊社がサボっているだけです

---
layout: cover
---

# ⑨【BE/FE】<br> 高速化がどうしてもしたいページは<br>CloudFrontのSWRキャッシュで済ませるよ

---

# 高速化がどうしてもしたいページはCloudFrontのSWRキャッシュで済ませるよ

- 再掲）マナリンクでは前段にCloudFrontを置いていて、かつAWS CDKで設定を管理している

```plantuml
@startuml AWS Architecture

!define AWSPuml https://raw.githubusercontent.com/awslabs/aws-icons-for-plantuml/v18.0/dist
!include AWSPuml/AWSCommon.puml
!include AWSPuml/NetworkingContentDelivery/CloudFront.puml
!include AWSPuml/Containers/Fargate.puml
!include AWSPuml/Containers/ElasticContainerService.puml
!include AWSPuml/General/User.puml
!include AWSPuml/ApplicationIntegration/StepFunctions.puml

!procedure $AWSIcon($service, $line1, $line2="")
rectangle "$AWSImg($service)\n<b>$line1</b>\n$line2"
!endprocedure

skinparam linetype ortho
left to right direction
$AWSIcon(User, " ", "User") as user

CloudFront(cloudfrontAlias, "CloudFront", "api.manalink.jp")
Fargate(fargateAlias, "AWS Fargate", "Laravel Server")

user --> cloudfrontAlias
cloudfrontAlias --> fargateAlias

' ECS TaskをFargate内部に追加
ElasticContainerService(ecsTaskAlias, "ECS Task", "Running Laravel App")

fargateAlias --> ecsTaskAlias

@enduml
```

---

# 高速化に関しての基本的なスタンス

- 私（CTO）は割とパフォーマンス頑張りたい人
  - FEではLighthouseを見て凡ミスは全部倒す、CLSできるだけ0、画像最適化もimgixを使うなどして低コストで実現（imgixで画像最適化を済ますのも**意識ﾁｮｯﾄ低い**かも）
  - BEでも、DDDは好きとはいえSQLを叩きまくる富豪的なスタンスは爆弾負債を残しそうなので好きではなく、基本はN+1も許容しないし、クエリ回数をCIで監視している
  - キャッシュはBiz・Dev共に認知の外に置きがちで思わぬエンバグのリスクが高いのでできるだけ避けたい
- とはいえどうしても高速化したい＆Mutationの頻度が少ないページは
  - CloudFront×stale-while-revalidateヘッダーでキャッシュする
  - 動的ページでも、古いキャッシュが割とすぐ揮発するので苦情になりにくい👍

---

# CloudFrontのSWRキャッシュの設定例

- Next.js（Pages Router）では以下のように設定する
- 正直、Next.js内部のキャッシュに頼るより一般的なProtocolに則るのでわかりやすい（と思ってる

```ts
export function setCacheControlForSSRPage(
  context: GetServerSidePropsContext<ParsedUrlQuery, string | false | object | undefined>,
) {
  context.res.setHeader('Cache-Control', 'public, s-maxage=10, stale-while-revalidate=86400');
}
```

- キャッシュであまり苦労したくないから、あらゆるキャッシュの中でも基本CloudFrontキャッシュだけで頑張るよ！が**意識ﾁｮｯﾄ低い**ポイント

---
layout: cover
---

# ⑩【BE/FE】<br> 腐敗防止層は適当でもめっちゃ価値あるから積極的に切ろう

---

# 腐敗防止層は適当でもめっちゃ価値あるから積極的に切ろう

- 腐敗防止層とは
  - あるモジュールがN箇所に依存していると、シグネチャの変更時にN箇所に影響が伝播するが、間にシグネチャを吸収するモジュールを挟むことで、変更時の影響を1箇所のみに絞る
  - ただ切るだけじゃなくて、引数の型やモジュール名を一段階抽象的にすることが望ましい

---

# 史上最強に意識が低い腐敗防止層

```tsx
import { Tab as LibTab } from '@headlessui/react';

export const Tab = LibTab;
export const TabPanel = LibTab.Panel;
export const TabList = LibTab.List;
export const TabPanels = LibTab.Panels;
export const TabGroups = LibTab.Group;
```

- こんなただLibraryからImportしてExportするだけのコンポーネント、意味があると思いますか？

---

# あります！

```tsx
import { Tab as LibTab } from '@headlessui/react';

export const Tab = LibTab;
export const TabPanel = LibTab.Panel;
export const TabList = LibTab.List;
export const TabPanels = LibTab.Panels;
export const TabGroups = LibTab.Group;
```

- 背景知識
  - Headless UIは、特定バージョンから`Tab.Panels`コンポーネントを`TabPanels`に変更した
  - 現バージョンのHeadless UIから直接TabをImportしていると、ライブラリアプデ時に、<br>**N箇所のコンポーネントを`Tab.Panels`から`TabPanels`に変更する必要がある**
  - あらかじめ内製Wrapperで`Tab.Panels`を`TabPanels`に変換しておくことで、アプデ時の影響範囲を1箇所に絞ることができる

---
layout: cover
---

# 【まとめ】<br>意識が低いアーキテクチャに<br>価値はあるか？

---

# 【まとめ】意識が低いアーキテクチャに価値はあるか？

- 小さなアーキテクチャなくして、大きなアーキテクチャなし
  - よく”大規模サービスやりたい”といった志向を見聞きしますが、個人的には<br>小さなアーキテクチャをしっかり作りきれることがまず大事
  - 大きなアーキテクチャは、小さなアーキテクチャをN回積み重ねることで作られる
- 小さな改善でも、やらないよりはマシ！
  - 「単にTabのWrapperを作るよりもっとDOM構造ごとWrapperにできないかな」など、<br>つい欲張ってしまうが、欲張りすぎて何もできなかったら本末転倒
  - **意識低い改善で終わらせるには意外と勇気がいる**が、やりきろう

---
layout: section
---

## ご清聴ありがとうございました！

follow me🐦: @meijin_garden
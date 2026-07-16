# 要件定義書 v4.2
## 戦略コンサルシステム：コアシステム基盤 & B2Bドッグフーディング編

作成日：2026-07-15
ステータス：Final v4.2
担当：壮輝 / MONJU

---

## 1. ビジョンとミッション

ユーザーの「野望」を入力として受け取り、
本質的な問いの発見から仮説検証・意思決定まで、
戦略コンサルのプロセスを自動化するシステムを構築する。

### ファーストユースケース（ドッグフーディング戦略）

開発者自身が第一のユーザーとなり、
Web制作×自動化事業のB2B営業に本システムを適用する。

現場の一次情報（ヒアリングデータ・失注理由）を
システムに蓄積し続けることで、
他のAIラッパーには模倣不可能な
「データモート（強力な参入障壁）」を構築し、
最終的にバーティカルAI SaaSとして外部展開する。

### 重要原則

**全ての施策の採否・優先順位は
意思決定システム（Level 0〜3）の出力に従って決定する。**

人間（壮輝）が直感や経験で施策を決定することはしない。
現時点で挙げられている施策（職業図鑑・三田市・LinkedIn等）は
全て「検証待ちの仮説」として保持する。

---

## 2. システムの本質（MBBスタンダード準拠・5フェーズ構成）

### 設計原則

戦略コンサルのデファクト（McKinsey・BCG・Bain）を忠実に再現する。
机上の空論を吐き出すLLMラッパーからの脱却を図り、
「Human-in-the-loop」による仮説検証サイクルを回す。

### Phase 0：問題定義エンジン

```
入力：野望・現状・制約（自然言語）
処理：
  ・「クライアントが言う問題 ≠ 本当の問題」原則で深掘り
  ・SCQAフレームワークで構造化
    Situation（現状）→ Complication（問題）
    → Question（問い）→ Answer（仮答え）
  ・問題ステートメントを明文化（具体的・有界に）
出力：
  ・問題ステートメント
  ・SCQAの4要素
```

### Phase 1：イシュー特定エンジン（新設）

```
入力：問題ステートメント
処理：
  ・「今、本当に解くべき問いか？」をスクリーニング
    （安宅『イシューからはじめよ』の「犬の道」回避）
  ・Issue TreeでMECEに問題空間を分解
  ・2×2マトリクスでイシュー優先度を評価
    軸①：重要度（解いたときのインパクト）
    軸②：実行可能性（答えを出せるか）
出力：
  ・本当に解くべきイシュー（1つに絞る）
  ・棄却したイシューと理由
  ・Issue Tree（MECE構造）
```

### Phase 2：仮説構築エンジン（Day-One Answer）

```
入力：イシュー
処理：
  ・限られた情報でまず答えを仮定する（Day-One Answer）
  ・Hypothesis TreeでMECEに仮説を展開
  ・Ghost Deck（アウトプットの骨格）を先に設計する
    ※分析の前にアウトプットを設計するのがMBBのデファクト
  ・良い仮説の条件を確認
    ①反証可能か
    ②アクションにつながるか
    ③自明でないか
出力：
  ・Day-One Answer（初期仮説）
  ・Hypothesis Tree（MECE構造）
  ・Ghost Deck（アウトプットの骨格）
  ・検証すべき仮説リスト（優先順位付き）
```

### Phase 3：検証設計・データ収集エンジン

```
入力：仮説リスト
処理（順序が重要）：
  Step 1：Desk Research（机上・二次情報）を先行
    ・外部API（市場データ・競合データ・統計）
    ・過去の類似プロジェクトのナレッジを参照
    ・「車輪の再発明をしない」原則
  Step 2：Fieldリサーチで隙間を埋める
    ・「誰に・どうヒアリングすべきか」の行動指示を生成
    ・現場の一次情報を管理画面から手動でフィード
    ・非言語のリアクション・生の愚痴も構造化して記録
    ※フィールドリサーチは「机上で答えが出ない」部分にのみ投入
  Step 3：80/20で分析を打ち切る
    ・完璧な分析を目指さない
    ・80%の正確さで意思決定を前に進める
  仮説が反証されたら：
    ・更新ログを記録（何のデータで・どう修正したか）
    ・Phase 2に戻って仮説を修正する（イテレーティブ）
出力：
  ・仮説の検証結果（支持/反証/不明）
  ・仮説更新ログ
  ・Fieldリサーチが必要な領域の特定と行動指示
```

### Phase 4：示唆抽出・意思決定エンジン（So What?）

```
入力：検証結果
処理：
  ・Pyramid Principleで統合する
    思考：ボトムアップ（データ→パターン→示唆→結論）
    出力：トップダウン（結論→根拠→データ）
  ・全アウトプットにSo What?を明示する
    NG：「売上が下がっている」
    OK：「Q3売上12%減。APAC拡大で挽回可能」
  ・Action Title形式で結論を書く
出力：
  ・Pyramid構造の意思決定レポート
  ・採択施策リスト（根拠・So What?付き）
  ・棄却施策リスト（根拠付き）
  ・実行ロードマップ
  ・KPI設計
  ・次のイテレーションへの入力（学習ループ）
```

### フェーズ間の関係

```
Phase 0：問題定義
  ↓ SCQAで構造化
Phase 1：イシュー特定
  ↓ Issue Tree・MECEで絞り込む
Phase 2：仮説構築
  ↓ Day-One Answer・Ghost Deck
Phase 3：検証（Desk→Field→80/20）
  ↓ 反証されたらPhase 2に戻る（イテレーティブ）
Phase 4：示唆抽出（So What?・Pyramid）
  ↓ 実行する
  ↓ 結果をフィードする
  ↓ Phase 0に戻る（学習ループ）
```

---

## 3. 学習ループの設計

```
野望を入力する
  ↓
Level 0 問いを発見する
  ↓
Level 1 仮説を立てる
  ↓
Level 2 検証する（机上＋フィールド）
  ↓
Level 3 施策を採択・棄却する
  ↓
実行する
  ↓
結果をフィードバックする
  ↓
仮説を更新する（精度が上がる）
  ↓
また問いを発見する
```

このループが速く・正確に回るほど
システムの価値とデータモートが強くなる。

---

## 4. 現在の検証状態（仮説ログ）

### 確定した結論（Level 3通過済み）

```
結論①：収益手段はWeb制作に決定
根拠：
  ・収益まで1〜6ヶ月（スキル・営業次第）
  ・単価10〜50万円/件
  ・将来性高・SaaS接続可能
  ・アフィリエイト（85%が月1万円未満）は除外
  ・補助金申請支援は法改正リスクがあり単体採用しない
    ただし営業の切り口として活用する

結論②：警戒心突破の構造が判明
根拠（飲食店オーナーの外注障壁データより）：
  ・代替プラットフォームへの依存
  ・ITリテラシー不足による心理的障壁
  ・ROIへの不信感
  ・キャッシュフロー制約
  ・「死んだサイト」になる恐怖
対応設計：
  ・デモサイトを先に作って見せる
  ・原稿取材・LINEだけのやり取り
  ・Notionで自己更新できるCMS込み
  ・補助金活用で実質負担を下げる
```

### 検証待ちの仮説（Level 2未通過）

```
仮説A：職業図鑑シリーズが技術デモとして有効か
仮説B：三田市が最適なターゲットエリアか
仮説C：LinkedInがB2B発信の主戦場として最適か
仮説D：Spark Baseが営業拠点として有効か
仮説E：「研究という大義名分」が警戒心突破に有効か
仮説F：30万＋30万の補助金パッケージが刺さるか
```

---

## 5. システムアーキテクチャ

### リポジトリ構成

```
kassamassa/monju-strategy（戦略・設計）
  ├── requirements_v4.md（本ドキュメント）
  ├── DESIGN_SYSTEM.md
  ├── market-analysis/
  └── admin-design/

kassamassa/web-page（コンテンツ実装）
  ├── app/vol/[slug]/（職業図鑑）
  └── app/admin/（管理者画面）

kassamassa/monju-core（システム実装・将来）
  ├── apps/admin-dashboard/
  ├── apps/saas-web/
  └── packages/strategy-engine/
```

### 技術スタック

```
フロントエンド：Next.js 14（App Router）+ TypeScript
スタイル：CSS Modules
モノレポ：Turborepo（Phase 2〜）
DB：Supabase（PostgreSQL）
認証：NextAuth.js
AI推論：Claude API
ホスティング：Vercel
```

### セキュリティ・マルチテナント要件

```
・全テーブルにtenant_idを必須（Not Null）
・Phase 1はtenant_id = 1（MONJU単独）で稼働
・SupabaseのRLSでDBレベルのデータ分離
・AIエージェントのSQL生成時は人間による監査必須
```

---

## 6. データモデル（Supabase）

```sql
-- 問いの発見
issues (
  id, tenant_id, input_text,
  issues_json, selected_issue, created_at
)

-- 仮説
hypotheses (
  id, tenant_id, issue_id,
  hypothesis_text, priority, status, created_at
)

-- フィールドインタビュー（最重要・モートの源泉）
field_interviews (
  id, tenant_id, company_name,
  interview_date, raw_notes,
  structured_pain_points, nonverbal_reactions,
  created_at
)

-- 提案・受注記録
proposals (
  id, tenant_id, company_name,
  proposed_package, proposed_price,
  result, rejection_reason, created_at
)

-- 学習ログ
learnings (
  id, tenant_id, hypothesis_id,
  action_taken, result,
  next_hypothesis, insight_text, created_at
)
```

---

## 7. 実装ロードマップ

### Phase 1（1ヶ月目）：基盤構築と行動開始

```
システム：
  ・Supabaseテーブル設計・構築
  ・admin-dashboardの最小UI実装
  ・Level 0のプロトタイプ（Claude API）

フィールド：
  ・仮説B〜Fの検証開始
  ・ヒアリング実施・結果をDBに記録
```

### Phase 2（2〜3ヶ月目）：検証ループ稼働と初受注

```
システム：
  ・Level 1〜3の実装
  ・補助金提案ロジックの完成

ビジネス：
  ・Web制作×自動化の初案件受注
  ・失注データの蓄積開始
```

### Phase 3（4〜6ヶ月目）：モートの深化と発信

```
システム：
  ・蓄積データによる推論精度向上
  ・プロンプトバージョン管理実装

発信：
  ・採択された発信チャネルでの継続投稿
  ・「地域小規模事業者の課題レポート」公開
```

### Phase 4（1年後）：SaaS化

```
システム：
  ・monju-coreのTurborepo化
  ・saas-webのローンチ
  ・マルチテナント対応をオン

ビジネス：
  ・外部ユーザー獲得
  ・料金プラン稼働
```

---

## 8. 成功指標

```
システム：
  ・Phase 1末：Level 0が稼働
  ・Phase 2末：学習ループが稼働
  ・Phase 4末：外部ユーザー獲得

ビジネス：
  ・Phase 2末：初受注1件
  ・Phase 3末：月収10万円
  ・Phase 4末：SaaS月次収益発生
```

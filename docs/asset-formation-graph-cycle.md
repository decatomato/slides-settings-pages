# 資産形成グラフサイクル 設計資料

作成日: 2026-09-17
目的: 国内外の資産形成に関する一次情報・フレームワークを取得し、個人が回し続けられる「情報取得 → グラフ化 → 判断 → 実行 → 見直し」のサイクルを設計する。

## 変更点サマリ(初版)

- 参照 X 投稿の取得結果と代替確認内容を記載。
- 国内外の情報源を役割別に要素表で整理。
- 国内外の「サイクル」フレームワークを比較し、共通構造を抽出。
- 5層(日次/週次/月次/四半期/年次)+ライフイベントの多層サイクルを Mermaid 図で提案。
- 各層で描くグラフ(KPI)と、AI 自動化の分担案を記載。

---

## 0. 参照 X 投稿について(未確認)

| 項目 | 内容 |
| --- | --- |
| URL | https://x.com/beku_ai/status/2100079333952086211 |
| 取得可否 | **未確認**。この実行環境から x.com / 各種ミラー(fxtwitter, nitter, syndication)への通信が遮断されており本文を取得できなかった。 |
| 投稿日時(ID から算出) | 2026-09-16 13:28 JST(Snowflake ID の時刻部を復号) |
| アカウント | ベク(@beku_AI)。検索結果によれば「AI 収益化」「Claude Code で株式自動売買システム構築」(2026-07-07 投稿、閲覧 79 万超)などを発信。 |
| 扱い | 本資料では投稿本文は引用せず、同アカウントの公開テーマ(AI エージェントによる投資情報収集・自動化)を「AI 活用サイクル」の観点として反映した。本文を貼っていただければ差分を統合する。 |

---

## 1. 情報源マップ(国内外)

### 1.1 国内(一次情報)

| 要素名 | 役割 | 依存関係 | 出典 |
| --- | --- | --- | --- |
| 金融庁 NISA 特設サイト「資産形成の基本」 | 長期・積立・分散、家計管理、ライフプランの公式原則 | サイクルの「原則」層 | https://www.fsa.go.jp/policy/nisa2/invest/ |
| 金融庁「家計の安定的な資産形成に関する有識者会議」 | 預貯金偏重からのリバランス論、政策背景 | 年次見直しの根拠 | https://www.fsa.go.jp/singi/kakei/index.html |
| 資産運用立国/基本方針(閣議決定 2024-03-15) | 制度変更の方向性(NISA 恒久化等) | 年次の制度チェック | https://www.fsa.go.jp/news/r5/sonota/letterbody.pdf |
| J-FLEC(金融経済教育推進機構)教材 | 「生活設計・家計管理・資産形成」の三本柱、中立の無料相談 | 月次家計・年次ライフプラン | https://www.j-flec.go.jp/materials/shisankeisei/ |
| 知るぽると(金融広報中央委員会) | 金融リテラシー教材、家計簿・ライフプラン表 | 月次家計 | https://www.shiruporuto.jp/ |
| 全国銀行協会「資産形成」 | 備えとしての資産形成の考え方 | 原則層 | https://www.zenginkyo.or.jp/asset-building/ |
| GPIF 基本ポートフォリオ | 4 資産 25% ずつ、乖離許容幅 ±5〜6%、株式/債券全体 ±9%(第 5 期 2025-04〜) | 四半期リバランス判定の閾値参考 | https://www.gpif.go.jp/gpif/15324685gpif/5th_policy_asset_mix_details_jp.pdf |
| 日本銀行 資金循環統計 / 時系列データ検索 | 家計金融資産の構成推移(現預金/株式/投信/保険年金) | 年次のベンチマーク | https://www.boj.or.jp/statistics/sj/index.htm , https://www.stat-search.boj.or.jp/ |
| 総務省統計局 e-Stat 家計調査 | 年代別の収支・貯蓄の平均像 | 年次の自己位置確認 | https://www.stat.go.jp/library/faq/faq04/faq04b01.html |
| 野村證券 大庭「資産運用のライフサイクル理論」 | 人的資本と金融資産の合算でリスク資産比率を決める考え方 | 年次のアロケーション見直し | https://www.toushin.or.jp/files/statistics/80/T_14.pdf |
| 第一ライフ資産運用経済研究所 レポート | AI を個人の資産運用にどこまで使えるか、詐欺リスク | AI 活用時のガードレール | https://www.dlri.co.jp/report/ld/592997.html |
| All About「家計の PDCA サイクル」 | 現状把握→計画→実行→評価→見直し、年 1 回 | サイクル構造の国内例 | https://allabout.co.jp/gm/gc/466916/ |

### 1.2 海外(一次情報・定番フレームワーク)

| 要素名 | 役割 | 依存関係 | 出典 |
| --- | --- | --- | --- |
| Vanguard "Principles for Investing Success" | Goals / Balance / Cost / Discipline の 4 原則、定期レビュー日を決める | 原則層、年次レビュー | https://corporate.vanguard.com/content/dam/corp/research/pdf/vanguards_principles_for_investing_success.pdf |
| Vanguard "Best practices for portfolio rebalancing" | 年 1〜2 回の監視+5% 閾値が費用対効果の均衡点。新規入金・分配金でのリバランスが低コスト | 四半期/年次リバランス規則 | https://corporate.vanguard.com/content/dam/corp/research/pdf/rational_rebalancing_analytical_approach_to_multiasset_portfolio_rebalancing.pdf |
| Bogleheads 投資哲学(10 原則) | 計画策定、早く頻繁に投資、リスク過不足回避、分散、タイミング回避、インデックス、低コスト、税最小化、単純化、Stay the course | 原則層 | https://www.bogleheads.org/wiki/Bogleheads%C2%AE_investment_philosophy |
| Bogleheads Investment Policy Statement (IPS) | 目標・リスク許容度・配分・リバランス規則を文書化 | サイクル全体の「憲法」 | https://www.bogleheads.org/wiki/Bogleheads%C2%AE_investing_start-up_kit |
| CFP Board 7-Step Financial Planning Process | 理解→情報収集→分析→提案→合意→実行→**モニタリング**(年 1 回+ライフイベント時) | 年次サイクルの骨格 | https://www.kitces.com/blog/definition-financial-planning-practice-standards-conduct-required-cfp-board/ |
| Money Guy "Financial Order of Operations"(9 段階) | 次の 1 円をどこに置くかの優先順位(免責額→会社拠出マッチ→高金利債務→生活防衛資金→税優遇口座→…→貯蓄率 25%) | 月次キャッシュフロー配分 | https://moneyguy.com/guide/foo/ |
| Trinity Study / Bengen 4% ルールと 2026 年の更新 | 取り崩し率の目安。Morningstar 3.9%(2026)、Bengen 4.7%、Vanguard 3.5〜4.5% と見解が分かれる | 年次のゴール達成度(FI 比率) | https://thepoorswiss.com/updated-trinity-study/ , https://en.wikipedia.org/wiki/4%25_rule |
| Merrill Lynch Investment Clock | 成長×インフレで景気を 4 局面に分け、優位資産(株/商品/現金/債券)を示す | 四半期のマクロ観測(配分は変えず理解用) | https://macro-ops.com/the-investment-clock/ |
| Ray Dalio All Weather / All Seasons | 4 つの経済環境に耐えるリスクパリティ配分 | 年次のアロケーション設計参考 | https://portfoliocharts.com/portfolios/all-seasons-portfolio/ |
| FRED(米セントルイス連銀) | 金利・CPI・失業率などマクロ系列の API 取得 | 四半期グラフのデータ源 | https://fred.stlouisfed.org/ |

### 1.3 AI 活用(参照投稿のテーマ)

| 要素名 | 役割 | 依存関係 | 出典 |
| --- | --- | --- | --- |
| Claude Code による株式自動売買・スクリーニング事例 | AI エージェントで情報取得・分析・執行を自動化する国内事例 | 日次/週次の自動収集 | https://x.com/beku_AI/article/2074417887050375361 , https://qiita.com/okikusan-public/items/27d9b0f0177293db8b1a |
| J-Quants(JPX)API | 国内株の株価・財務データ取得 | 日次/週次データ源 | https://jpx-jquants.com/ |
| Bloomberg「AI 任せで老後資産形成は大丈夫か」(2026-06-06) | AI 一任の限界と検証 | AI ガードレール | https://www.bloomberg.com/jp/news/articles/2026-06-06/TFOS2SKK3NY800 |

---

## 2. 国内外サイクルの比較と共通構造

| フレームワーク | 起点 | 実行 | 監視・見直し頻度 | 特徴 |
| --- | --- | --- | --- | --- |
| 家計 PDCA(国内) | 現状把握 | 計画→実行 | 年 1 回 | 家計中心、投資は一部 |
| J-FLEC 三本柱(国内) | 生活設計 | 家計管理→資産形成 | 教材ベース(頻度規定なし) | 長期・積立・分散 |
| CFP 7 ステップ(米) | 目標理解 | 提案→実行 | 年 1 回+ライフイベント | 専門家プロセス |
| Vanguard 4 原則(米) | Goals | Balance/Cost | 定期レビュー日+5% 閾値 | 低コスト・規律 |
| Bogleheads IPS(米) | 計画文書 | インデックス積立 | IPS に規定 | 「Stay the course」 |
| Money Guy FOO(米) | 免責額確保 | 9 段階に配分 | 給与ごと | キャッシュフロー配分 |
| Investment Clock / All Weather | マクロ 4 局面 | 配分設計 | 四半期 | 市場サイクル理解 |

**共通構造**: すべて「目標(ゴール)→現状把握(データ)→配分ルール(IPS)→実行(積立・配分)→監視(グラフ)→閾値超過時のみ見直し」という閉ループで、頻度は「毎月の実行」「年 1 回の総点検」「ライフイベント時の臨時見直し」の 3 段構え。国内は家計管理に強く、海外は配分ルールと閾値の定量化に強いので、両者を組み合わせる。

---

## 3. 提案: 資産形成グラフサイクル(多層)

設計方針
- **原則層は変えない**: 長期・積立・分散(金融庁)+低コスト・規律(Vanguard/Bogleheads)。
- **層ごとに「取得する情報」「描くグラフ」「許される行動」を固定**し、短周期ほど行動を制限する(短周期の情報で売買しない)。
- **閾値でのみ発動**: 配分乖離 5%(Vanguard)〜GPIF 許容幅(±5〜6%)を超えたときだけリバランス。
- **AI は取得・整形・可視化・異常検知まで**。売買判断・IPS 変更は人が行う。

```mermaid
flowchart TB
    subgraph L0[原則層(固定)]
        P[ゴール/IPS<br/>長期・積立・分散・低コスト・規律]
    end

    subgraph L1[日次(自動)]
        D1[取得: 保有資産の評価額・為替・主要指数] --> D2[グラフ: 純資産推移(折れ線)] --> D3[行動: なし(記録のみ)]
    end

    subgraph L2[週次(自動+5分レビュー)]
        W1[取得: 決算・適時開示・経済指標カレンダー] --> W2[グラフ: 配分ドリフト(積み上げ棒)] --> W3[行動: 異常アラート確認のみ]
    end

    subgraph L3[月次(人 30 分)]
        M1[取得: 収入・支出・積立実績] --> M2[グラフ: 貯蓄率・FOO 段階(ウォーターフォール)] --> M3[行動: 積立の入金配分をドリフト縮小方向へ]
    end

    subgraph L4[四半期(人 1 時間)]
        Q1[取得: マクロ 4 局面(成長×インフレ)、FRED/日銀] --> Q2[グラフ: Investment Clock 位置、乖離幅ゲージ] --> Q3{乖離 5% 超?}
        Q3 -- Yes --> Q4[リバランス実行]
        Q3 -- No --> Q5[何もしない]
    end

    subgraph L5[年次(人 半日)]
        Y1[取得: 制度改正(NISA/税)、ライフサイクル理論、資金循環統計との比較] --> Y2[グラフ: ゴール到達度(FI 比率=資産×取り崩し率/年間支出)、年代別ベンチマーク] --> Y3[行動: IPS 改訂・目標配分の更新]
    end

    E[ライフイベント<br/>結婚/出産/転職/相続/退職] -. 臨時 .-> L5

    P --> L1 --> L2 --> L3 --> L4 --> L5
    Y3 --> P
```

### 3.1 各層のグラフ定義(KPI)

| 層 | グラフ | 指標定義 | データ源 | 判断閾値 |
| --- | --- | --- | --- | --- |
| 日次 | 純資産推移(折れ線) | Σ評価額 − 負債 | 証券会社 CSV / API、為替 | なし(記録) |
| 週次 | 配分ドリフト(積み上げ棒) | 各資産の現在比率 − 目標比率 | 保有明細 | ±5% で黄色、GPIF 許容幅超で赤 |
| 月次 | 貯蓄率・FOO 段階(ウォーターフォール) | (収入 − 支出) / 収入、FOO の到達段階 | 家計簿 | 目標貯蓄率(例 20〜25%)未達で見直し |
| 月次 | 積立実行率 | 実績積立額 / 計画積立額 | 証券口座 | 100% 未満で原因確認 |
| 四半期 | Investment Clock 位置 | 成長(GDP ギャップ/PMI)×インフレ(CPI)の 2 軸散布 | FRED、日銀、内閣府 | 配分は変えない(理解用) |
| 四半期 | 乖離幅ゲージ | 株式全体・債券全体の乖離 | 保有明細 | ±9%(GPIF 準拠)で必ずリバランス |
| 年次 | FI 比率 | 金融資産 × 取り崩し率(3.5〜4.7%)/ 年間支出 | 全データ | 1.0 で経済的自立 |
| 年次 | 年代別ベンチマーク | 自分の資産構成 vs 資金循環統計・家計調査 | 日銀、e-Stat | 差分の理由を説明できるか |
| 年次 | 人的資本+金融資産のリスク比率 | ライフサイクル理論に基づく株式比率 | 年収・残存勤続年数 | 目標配分の改訂根拠 |

### 3.2 行動制限ルール(IPS に転記する項目)

1. 日次・週次の情報で売買しない(記録とアラートのみ)。
2. 新規入金・分配金は常にドリフトを縮小する資産へ配分する(低コストなリバランス)。
3. 乖離 5% 超は四半期レビューで、株式/債券全体 9% 超は即時にリバランスする。
4. 目標配分・取り崩し率・ゴールの変更は年次レビューかライフイベント時のみ。
5. AI 出力は「情報整理と判断支援」に限定し、執行は人が承認する(第一ライフ研レポートの詐欺・過信リスクを踏まえる)。

---

## 4. AI 自動化の分担案

| 層 | 自動化内容 | 実装(Codex 側) | 運用・検証(Claude 側) |
| --- | --- | --- | --- |
| 日次 | 評価額・為替・指数の取得、純資産 CSV 追記、折れ線更新 | 取得スクリプト+CSV/SQLite | 定期実行(Routine)、欠損検知 |
| 週次 | 決算・適時開示・指標カレンダー収集、ドリフト計算、アラート | J-Quants/FRED クライアント、閾値ロジック | 要約レポート md 生成 |
| 月次 | 家計簿集計、貯蓄率・FOO 判定、入金配分の提案 | 集計ジョブ | 提案の妥当性レビュー |
| 四半期 | マクロ 2 軸プロット、乖離ゲージ、リバランス案 | プロット生成 | 案の検証・文書化 |
| 年次 | 制度改正の差分要約、ベンチマーク比較、IPS 改訂ドラフト | 統計取得 | 一次ソース確認、改訂案レビュー |

注: 参照投稿(@beku_AI)のテーマである「Claude Code による自動売買」は、本サイクルでは**執行を含めない**設計とした。売買執行を自動化する場合は、上記 IPS ルール 1・3・5 をコード側のガードとして先に実装することを推奨する。

---

## 5. 限界・未確認事項

- 参照 X 投稿の本文は未取得(通信遮断)。本文提供後に統合する。
- 金融庁・Vanguard・Bogleheads・野村の各ページは本環境から直接閲覧できず、検索結果の要約に基づく。数値(5% 閾値、GPIF 許容幅、取り崩し率)は複数ソースで一致を確認したが、一次ページでの再確認を推奨。
- 取り崩し率は 2024〜2026 年で見解が分かれるため、幅(3.5〜4.7%)で扱う。

## 6. 出典一覧

- 金融庁 NISA 特設「資産形成の基本」 https://www.fsa.go.jp/policy/nisa2/invest/
- 金融庁 家計の安定的な資産形成に関する有識者会議 https://www.fsa.go.jp/singi/kakei/index.html
- 金融庁 基本方針(2024-03-15 閣議決定) https://www.fsa.go.jp/news/r5/sonota/letterbody.pdf
- J-FLEC 資産形成ハンドブック https://www.j-flec.go.jp/materials/shisankeisei/
- J-FLEC 講義資料(資産形成) https://www.j-flec.go.jp/wpimages/uploads/60min_model_3.pdf
- 全国銀行協会 https://www.zenginkyo.or.jp/asset-building/
- GPIF 第 5 期基本ポートフォリオ詳細 https://www.gpif.go.jp/gpif/15324685gpif/5th_policy_asset_mix_details_jp.pdf
- 日本銀行 資金循環統計 https://www.boj.or.jp/statistics/sj/index.htm
- 総務省統計局 FAQ(家計部門の金融資産) https://www.stat.go.jp/library/faq/faq04/faq04b01.html
- 大庭昭彦(野村證券)資産運用のライフサイクル理論 https://www.toushin.or.jp/files/statistics/80/T_14.pdf
- 柏村祐(第一ライフ資産運用経済研究所)AI は個人の資産運用にどこまで活用できるのか https://www.dlri.co.jp/report/ld/592997.html
- All About 家計の PDCA サイクル https://allabout.co.jp/gm/gc/466916/
- Vanguard, Principles for Investing Success https://corporate.vanguard.com/content/dam/corp/research/pdf/vanguards_principles_for_investing_success.pdf
- Vanguard, Rational rebalancing (2022) https://corporate.vanguard.com/content/dam/corp/research/pdf/rational_rebalancing_analytical_approach_to_multiasset_portfolio_rebalancing.pdf
- AAII, Best Practices for Portfolio Rebalancing(Vanguard 2010 研究の紹介) https://www.aaii.com/journal/article/best-practices-for-portfolio-rebalancing
- Bogleheads investment philosophy https://www.bogleheads.org/wiki/Bogleheads%C2%AE_investment_philosophy
- Bogleheads investing start-up kit https://www.bogleheads.org/wiki/Bogleheads%C2%AE_investing_start-up_kit
- Kitces, CFP Board Practice Standards https://www.kitces.com/blog/definition-financial-planning-practice-standards-conduct-required-cfp-board/
- Money Guy, Financial Order of Operations https://moneyguy.com/guide/foo/
- The Poor Swiss, Updated Trinity Study 2026 https://thepoorswiss.com/updated-trinity-study/
- Wikipedia, 4% rule https://en.wikipedia.org/wiki/4%25_rule
- Macro Ops, The Investment Clock https://macro-ops.com/the-investment-clock/
- Portfolio Charts, All Seasons Portfolio https://portfoliocharts.com/portfolios/all-seasons-portfolio/
- ベク(@beku_AI)Claude Code を使った株式自動売買システムの構築方法(2026-07-07) https://x.com/beku_AI/article/2074417887050375361
- Bloomberg(2026-06-06)AI 任せで老後資産形成は大丈夫か https://www.bloomberg.com/jp/news/articles/2026-06-06/TFOS2SKK3NY800

# 議事録: Code with Claude 2026 | Tokyo 基調講演

- **日時**: 2026-06-10（ライブ配信）
- **主催**: Anthropic（日本初開催・2日間イベントの初日基調講演）
- **動画**: https://www.youtube.com/watch?v=GiqyYQdYoIY
- **出典**: YouTube ライブ自動字幕（英語）より作成。固有名詞は文脈から推定補正。タイムスタンプは配信開始からの経過時間（講演本編は 1:02:50 開始）。

---

## 登壇者

| 時刻 | 登壇者 | 役職 | テーマ |
|---|---|---|---|
| [1:02:50](https://youtu.be/GiqyYQdYoIY?t=3770) | Caitlin（Less） | Head of Engineering, Claude Platform | オープニング・プラットフォーム戦略 |
| [1:09:35](https://youtu.be/GiqyYQdYoIY?t=4175) | Diane Penn | Head of Product Management, Research | 新モデル発表 |
| [1:21:15](https://youtu.be/GiqyYQdYoIY?t=4875) | Angela Jen | Head of Product, Claude Platform | Claude Managed Agents |
| [1:26:10](https://youtu.be/GiqyYQdYoIY?t=5170) | Caitlin（再登壇） | 同上 | Managed Agents デモ |
| [1:30:36](https://youtu.be/GiqyYQdYoIY?t=5436) | Cat Wu | Head of Product, Claude Code | Claude Code 最新機能 |

---

## 主要発表（サマリー）

1. **Claude Fable 5 / Claude Mythos 5 リリース**（第5世代・当日朝公開）
2. **Claude Managed Agents 新機能**: Scheduled Deployments・Vaults（環境変数保管）・Outcomes・Memory・Dreaming
3. **Claude Code 新機能**: Dynamic Workflows・Agents View（CLI）・Claude Security 等。Fable 5 は全 Claude Code ユーザーに提供開始

---

## 1. オープニング — Caitlin（1:02:50〜）

- 日本初の Code with Claude 開催。数時間前に第5世代モデル **Fable 5 / Mythos 5** をリリースしたと冒頭で発表
- Anthropic は「プラットフォーム企業」：開発者が生み出す価値が自社単独を上回る
- **顧客事例（APAC）**:
  - **楽天**: Claude Code から Claude Managed Agents へ拡大。エンジニアリング・プロダクト・営業・財務の社内エージェント運用。リリース頻度が四半期1回 → **2週間ごと**に
  - **Canva**: Claude によりデザイン内に対話型ミニアプリ（地図・計算機・ウィジェット）を生成可能に
- モデル進化の振り返り: 1年前 Opus 4（機能単位の自律実装）→ 6ヶ月前（夜間長時間タスク）→ 2ヶ月前 Mythos が OpenBSD ソースツリーから **27年間見逃された脆弱性を発見**
- プラットフォームの **API 量は前年比約17倍**

## 2. 新モデル発表 — Diane Penn（1:09:35〜）

### Claude Fable 5
- 一般提供される中で**過去最高性能のモデル**。ほぼ全ベンチマークで SOTA（SWE-bench Pro 最高スコア）
- 強みの2軸:
  - **シングルショット正確性**: 複雑で仕様が明確な問題を一発で解決
  - **自律性**: 単一ゴールで数日間動作可能。数百万トークン規模でも仕様を記憶、サブエージェントの分配・コスト管理も改善
- コードの「読み」にも強い: 障害トリアージ、リポジトリ履歴調査、能動的な改善提案
- コーディング以外: 財務分析・文書・スライド・表計算をエンドツーエンドで処理。曖昧で混在した依頼の整理も得意。ビジョン性能は歴代 Claude 最高
- **セーフガード**: サイバーセキュリティ・生物・化学領域のリクエストは **Opus 4.8 へ自動ルーティング**（明示ラベル付き・Opus 料金課金）。正当な研究がブロックされる場合がある点は改善継続中

### Claude Mythos 5
- Fable 5 と同一基盤、サイバー・バイオのセーフガードを解除した研究者向けモデル
- **Project Glasswing** パートナーに当日から提供。今月中にライフサイエンス研究者の登録を拡大

### サードパーティ評価
- **Cognition**: 自社評価 Frontier Bench で歴代最高スコア（長期推論・未知ツールへの汎化を評価）
- **GenSpark**: 全モデル比較で1位。UI設計・ゲームコーディング等の最難関タスクで最強

### 開発者への提言
1. 現行ではなく**次のバージョンの Claude を想定して設計**する
2. モデルが賢くなるほど、複雑なハーネスよりも**ファイルシステムやサンドボックス等の基本プリミティブ**が有効
3. **より難しい評価・まだ動かないプロトタイプ**を作る — 動き始めた時が出荷の合図
4. **モデルアップグレードを容易に**（自動評価・テストプロセス整備）

## 3. Claude Managed Agents — Angela Jen（1:21:15〜）

- AIネイティブ企業の要件は **ハーネス・コンテキスト・インフラ** の3要素。これを統合提供するのが Claude Managed Agents
- **ハーネス**: 「頭脳（判断）」と「手（サンドボックス実行）」を分離。Outcomes 指定で達成まで反復
- **コンテキスト**: **100万トークンウィンドウ**、メモリ、スキルの自己読み書き、過去トラジェクトリを省察して自己改善する **Dreaming**
- **インフラ**: サンドボックスの自動スケール、複数エージェントフリート生成
- 導入事例: **Notion**（プロダクト内エージェントオーケストレーション）、**Asana**（AI チームメイト）

### デモ — Caitlin（1:26:10〜）
- 架空の F1 チーム「Shankira Racing」の研究ダッシュボード（空力・タイヤ温度・パワーユニット・ドライバー安全の4エージェント）
- **本日リリース**: オンデマンド実行に加え **Scheduled Deployments**（例: 夜間の安全チェック定期実行）、Developer Console での観測性、**Memory / Dreaming** ボタン
- ※会場 Wi-Fi 不調により一部は口頭説明で代替

## 4. Claude Code — Cat Wu（1:30:36〜）

- 平均的な開発者は**週20時間**を Claude Code と共に作業。Anthropic 社内ではエンジニア1人あたりのコード出荷量が **8倍**に
- **4つのインターフェース**: CLI（パワーユーザー向け）/ IDE 拡張 / Claude Desktop（全セッション横断ビュー・プレビュー内蔵）/ **Agents View in CLI**（ターミナルを離れず全セッション管理）
- ユーザーフィードバック起点の新プロダクト群:

| 要望 | プロダクト |
|---|---|
| コードレビュー時間の削減 | **Code Review**（エージェントチームが PR の重大バグを検出・数千社利用） |
| 外出先でのコーディング | **Remote Control + iOS/Android アプリ** |
| チケット起点の自動実行 | **Routines**（スケジュール / Webhook / API トリガー） |
| セキュリティチームの負荷 | **Claude Security**（コードベースを夜間スキャン・重要度判定・修正セッション起動） |
| 大規模リファクタ/移行 | **Dynamic Workflows**（数十〜数百エージェントを決定的構造で並列実行） |

- **Dynamic Workflows デモ**: マーケサイトの12言語ローカライズ。逐次なら約1時間 → 並列実行＋検証エージェント12体で1プロンプト完結。ワークフローは JavaScript として保存・再利用可能
- 導入事例: **Spotify**（Agent SDK 製の移行エージェントで月1,000超の PR をマージ、移行期間 **90%短縮**）、**メルカリ**（全エンジニアが利用、アウトプット前年比 **+90%**）
- **Fable 5 は本日から全 Claude Code ユーザーに提供**

## 5. クロージング（1:42:12〜）

- モデル（Diane）・エージェント基盤（Angela/Caitlin）・開発者ツール（Cat）の3層は一つのストーリー
- 当日の後続セッション案内: 研究トーク / Claude Platform トラック / Claude Code ワークショップ

---

## 特記事項

- 自動字幕由来のため、人名・固有名詞（Caitlin の姓、"Shankira Racing" 等）は要確認
- 配信冒頭 0:00〜1:02 は開演前の待機映像（議事内容なし）
- アーカイブ公開後に YouTube の処理済み字幕で精度を再検証可能

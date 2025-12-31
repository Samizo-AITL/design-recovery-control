---
title: Design Recovery Control – Current Status & Next Steps
author: Samizo-AITL
date: 2025-12-31
version: 0.1
---

# Design Recovery Control  
## Current Status & Next Steps

本ドキュメントは、`design-recovery-control` リポジトリ立ち上げ時点での  
**思想確定点・到達状態・今後の展開方針**を整理したメモである。  
次回作業は、本 md を起点として再開する。

---

## 1. 現在地（Where We Are）

### 1.1 リポジトリ状態

- Repository: `design-recovery-control`
- 公開設定：Public
- 初期コミット：
  - README.md 作成
  - Description / Topics 設定済み
- GitHub Pages：
  - `samizo-aitl.github.io/design-recovery-control/` に接続済み

---

### 1.2 コンセプト確定事項（FIX）

**Design Recovery Control (DRC)** を以下のように定義する。

> Design Recovery Control is a control architecture that recovers  
> *control design assumptions* under system degradation,  
> using layered supervision of PID, FSM, and LLM.

#### 明確に「やらないこと」
- LLMによるリアルタイム制御 ❌
- 操作量 $u(t)$ への直接介入 ❌
- Reliability Control の代替 ❌

#### 明確に「やること」
- 劣化によって破綻した **制御設計前提の回復**
- PIDゲイン・FSM遷移条件・運転モード定義の再設計
- LLMは **設計監督層** に限定

---

## 2. 位置づけ整理（Conceptual Positioning）

### 2.1 Controlカテゴリ比較

| Category | 対象 | 主眼 |
|---|---|---|
| Reliability Control | 物理ストレス | 劣化予防 |
| Recovery Control | 出力・機能 | 機能復旧 |
| **Design Recovery Control** | 制御設計前提 | 設計回復 |

---

### 2.2 AITLとの関係

- **AITL**：アーキテクチャパターン（PID × FSM × LLM）
- **DRC**：AITLにおける *LLM設計監督層* を一般化した工学概念

```
AITL Architecture
 ├─ PID : Real-time Control
 ├─ FSM : Safety & State Supervision
 └─ LLM : Design Recovery Control（← 本リポジトリ）
```

---

## 3. 今回は「やらない」と決めたこと

意図的に、以下は次フェーズに回す。

- 数学的厳密性（安定証明・収束証明）
- ドメイン特化モデル（Inkjet / MEMS / Semiconductor）
- 大規模PoC・長期ログ評価
- 論文化フォーマット整備

👉 今フェーズの目的は **概念の固定**。

---

## 4. 次フェーズ候補（What to Do Next）

### Phase 1：Concept Completion（最優先）

- [ ] README に **比較図（Reliability vs Recovery vs DRC）** を追加
- [ ] DRC の **Design Principles** を箇条書きで明文化
- [ ] 「LLMが触れてはいけない境界」を図示

---

### Phase 2：Minimal PoC

- [ ] 劣化モデル（1次遅れ系の $\tau$ 変化）
- [ ] FSM：NORMAL / DEGRADED / RECOVERY
- [ ] LLM：
  - 入力：FSMログ＋性能指標
  - 出力：PID再設計案（テキスト）
- [ ] Before / After 応答グラフ 1枚

👉 **「Design Recovery が起きた瞬間」を可視化**

---

### Phase 3：AITL統合

- [ ] `aitl-controller-A-type` との差分整理
- [ ] DRC を「AITLの設計監督層」として再定義
- [ ] Samizo-AITL Portal への概念ページ追加

---

## 5. このリポジトリの最終ゴール

- 「LLM制御」という誤解を回避した  
  **AI × Control の正しい設計分業モデル**を提示する
- 教材・PoC・論文の **共通語彙**として機能させる
- 長期的にドメイン非依存な「設計回復」という概念を残す

---

## 6. 次回の開始点（Start Here Next Time）

次回は以下のどれかから開始する：

1. README 拡張（Conceptual Diagram 追加）
2. Minimal PoC の Python 1ファイル作成
3. 「Design Recovery Control 定義文」の最終確定

---

*This document freezes the current design intent.*  
*Further work should extend, not redefine, this foundation.*

---
version: 1.4
type: functional-requirements
---

# 01. 機能要件
## Epic: 拾得物の登録 (Item Registration)
### FR-01-01: AIによる自動入力とインテリジェントな分類・提案
- As a 施設担当者,
- I want to 拾得物の情報が、物品の特性や法的要件に応じて賢く分類・提案され、簡単に入力できるようにしてほしい,
- so that 手入力の手間を省き、遺失物法に則った適切な管理を、一貫性を持って実現したい。
- Acceptance Criteria:
    - [ ] 写真をアップロードすると、AIが解析を開始する。
    - [ ] 分類提案: AIは、"eac_05_item_classification.json"を知識ベースとして、拾得物の大分類・中分類を提案する。
    - [ ] 解析結果（品名、特徴など）が登録フォームの各項目に自動で入力される。
    - [ ] AIの提案には確信度(Confidence Score)がパーセンテージで併記される。
    - [ ] 権利情報の入力:
        - [ ] 「拾得者の属性」を「第三者」「施設占有者」から選択できる。
        - [ ] 「所有権の主張」の有無をチェックボックス等で選択できる。
        - [ ] 「報労金の請求権」の有無をチェックボックス等で選択できる。
    - [ ] 保管場所の提案ロジック (優先度順):
        1. [最優先] 「所有権の主張」が「有り」の場合、保管場所に「yy-mm-dd-所有権主張」を自動で提案する。
        2. [ ] AIが品名を「傘」と判断した場合、保管場所に「yy-mm-dd-umb」を自動で提案する。
        3. [ ] AIが特徴に「食品」が含まれると判断した場合、保管場所に「yy-mm-dd-冷蔵庫」または「yy-mm-dd-冷凍庫」を自動で提案する。
        4. [ ] 上記以外の場合は、デフォルトの保管場所命名規則「yy-mm-dd-nn」に従って提案する。
    - [ ] 手動入力のサポート:
    - [ ] 分類や保管場所の入力フィールドは、ドロップダウンリスト形式になっている。
    - [ ] 分類のドロップダウンリストには"eac_05_item_classification.json"に基づいた選択肢が表示される。
    - [ ] 担当者はAIの提案内容や権利情報を修正できる。
    - [ ] 画像を登録せずに、テキスト情報のみで登録することも可能である。

## Epic: 拾得物の検索 (Item Search)
### FR-02-01: 高度な検索機能 (Advanced Search)
- As a 施設担当者,
- I want to 品名、特徴などのキーワードや、拾得場所・日付で、登録された拾得物を柔軟かつ正確に検索したい,
- so that 遺失者からの「黒っぽい上着」のような曖昧な情報からでも迅速に対応できる。
- Acceptance Criteria:
    - [ ] セマンティック検索: 「ジャケット」で検索した場合、「上着」や「ジャンパー」など、意味的に関連する物品も検索結果に含まれる。AIがテキストの特徴量をベクトル化し、検索クエリとの類似度に基づいて結果をランキングする。
    - [ ] キーワード検索: 複数のキーワードを組み合わせてAND検索ができる。
    - [ ] 絞り込み: 検索結果を拾得場所（テキスト入力）や拾得日の期間（開始日・終了日）で絞り込める。
    - [ ] 結果表示: 検索結果は一覧で表示され、写真のサムネイルも確認できる。

### FR-02-02: 音声検索 (v1.1)
- As a 施設担当者,
- I want to マイクに向かって話すだけで、拾得物を検索したい,
- so that キーボード操作が苦手でも、素早く検索できる。

## Epic: 拾得物の管理 (Item Management)
### FR-03-01: ステータス更新
- As a 施設担当者,
- I want to 拾得物の状態を「保管中」「返還済」「警察届出済」などに簡単に更新したい,
- so that 物品の状況を正確に管理できる。

### FR-03-02: 保管期限管理
- As a 施設担当者,
- I want to 保管期限が近い、または切れた物品を一覧で確認したい,
- so that 廃棄や警察への届出といった次のアクションを漏れなく行える。

## Epic: システム利用 (System Access & Audit)
### FR-04-01: 施設認証と自動ログイン
- As a 施設担当者,
- I want to 初回だけ認証すれば、次回から自動でログインしてほしい,
- so that 毎回のログイン操作を省略できる。
- Acceptance Criteria:
    - [ ] 初回起動時に施設コードとパスワードを要求する。
    - [ ] 認証成功後、認証情報をセキュアに保存する。
    - [ ] 次回以降の起動時は、保存した情報を使って自動的にログインする。
    - [ ] 管理者は、紛失した端末などの認証を強制的に無効化できる。

### FR-05-01: 監査ログ
- As a システム管理者,
- I want to 「いつ」「誰が」「どの拾得物データを」「どのように操作したか」の履歴を記録・閲覧したい,
- so that 不正な操作がないかを確認し、システムのセキュリティと信頼性を担保できる。
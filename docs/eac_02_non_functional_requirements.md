---
version: 1.0
type: non-functional-requirements
---

# 02. 非機能要件
## NFR-PERF: 性能・スケーラビリティ
- NFR-PERF-01: 検索応答時間は、95パーセンタイルのリクエストにおいて2秒以内に完了すること。
- NFR-PERF-02: 通常時10名、ピーク時30名の同時接続ユーザーの負荷に耐えること。
- NFR-PERF-03: データ件数が100万件規模になっても、検索応答時間（2秒以内）を維持すること。
- NFR-PERF-04: 1施設あたり年間2万件の登録（画像含む）を想定し、5年間の運用に耐える容量設計であること。

## NFR-SEC: セキュリティ
- NFR-SEC-01: 認証パスワードは、ソルト付きハッシュ化方式(Bcrypt)を用いて保存すること。
- NFR-SEC-02: 自動ログイン用のリフレッシュトークンはクライアントPCのセキュアな領域に保存し、有効期限は90日とすること。
- NFR-SEC-03: 管理者は、特定の施設の認証トークンをサーバー側から強制的に失効させられること。
- NFR-SEC-04: SQLインジェクションを防ぐため、全てのDBクエリでパラメータ化クエリを使用すること。
- NFR-SEC-05: アップロードされた画像ファイルは、サーバーサイドでマルウェアスキャンを実施すること。
- NFR-SEC-06: OWASP Top 10の主要な脆弱性に対応すること。

## NFR-REL: 信頼性・災害対策
- NFR-REL-01: RPO (目標復旧時点) は24時間とする。DBは日次でバックアップを取得する。
- NFR-REL-02: RTO (目標復旧時間) は4時間とする。障害発生後、4時間以内にシステムを復旧させる手順を確立する。
- NFR-REL-03: バックアップデータは、地理的に離れた場所（例: クラウドの別リージョン）に保管すること。
- NFR-REL-04: AIエンジンへの接続が10秒以内に完了しない場合、タイムアウトとしてエラー処理を行うこと。タイムアウト発生時は最大2回まで再接続を試み、それでも失敗する場合は手動入力モードに切り替えること。

## NFR-A11Y: アクセシビリティ
- NFR-A11Y-01: WCAG 2.1 レベルAAの主要な基準を満たすこと。
- NFR-A11Y-02: キーボードのみでの主要な操作が可能であること。
- NFR-A11Y-03: スクリーンリーダー（NVDA等）での読み上げに対応すること。

## NFR-OPS: 運用・保守
- NFR-OPS-01: アプリケーションログはレベル（INFO, WARN, ERROR）を定義し、30日間保持すること。
- NFR-OPS-02: 監査ログは1年間オンラインで検索可能とし、その後3年間はアーカイブ保管すること。
- NFR-OPS-03: CPU使用率、メモリ使用率、API応答時間等を監視し、閾値を超えた場合に管理者に通知すること。
- NFR-OPS-04: AIモデルの精度(F1スコア)が0.85を下回った場合、または3ヶ月に一度、再学習パイプラインを実行すること。
- NFR-OPS-05: 拾得物が「現金」「貴金属」の場合、システムは「金庫保管」を推奨し、その記録を残すこと。
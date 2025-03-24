# OctoBot-Services ドキュメント

## 概要
OctoBot-Servicesは、OctoBotのコア取引機能と様々な外部サービス、通信チャネル、ユーザーインターフェースを統合するPythonパッケージです。取引ボットと外部世界の橋渡しとして機能します。

このパッケージは、OctoBotユーザーに以下の機能を提供します：
- 取引、注文、市場状況に関する通知の受信
- コマンドベースのインターフェース（例：Telegram）を通じた取引システムとの対話
- 取引システムの管理と監視のためのWebインターフェースの使用
- 外部データソースやプラットフォームへの接続
- 機能強化のための様々なサービスの設定

## コアアーキテクチャ
OctoBot-Servicesのアーキテクチャは、いくつかの重要な抽象化に基づいています：

### サービスシステム
- `AbstractService`：インターフェースと共通の動作を定義するすべてのサービスの基本クラス
- `ServiceFactory`：サービスインスタンスを作成・管理し、シングルトンインスタンスを確保
- `AbstractServiceUser`：サービスを必要とするコンポーネントの基本クラス

### 通知システム
- `AbstractNotifier`：通知を送信するための基本クラス
- 様々なイベント（注文、取引など）に対応する通知タイプ
- `NotificationChannel`：購読者に通知を配信するためのチャネル

### インターフェースシステム
- `AbstractInterface`：すべてのインターフェースの基本クラス
- `AbstractBotInterface`：コマンドベースの対話のためのインターフェース
- `AbstractWebInterface`：Webベースの対話のためのインターフェース

### サービスフィードシステム
- `AbstractServiceFeed`：外部ソースからデータを受信するサービスフィードの基本クラス
- `ServiceFeedFactory`：サービスフィードインスタンスを作成
- `ServiceFeedManager`：サービスフィードのライフサイクルを管理

## ディレクトリ構造
```
octobot_services/
├── api/                  # 外部連携用のAPI関数
├── channel/              # 通信チャネル
├── interfaces/           # インターフェース実装
│   ├── bots/             # ボットインターフェース
│   ├── web/              # Webインターフェース
│   └── util/             # インターフェースユーティリティ
├── managers/             # コンポーネントマネージャー
├── notifier/             # 通知システム
├── notification/         # 通知実装
├── services/             # サービス実装
├── service_feeds/        # サービスフィード実装
└── util/                 # ユーティリティ関数
```

## 主要コンポーネント

### サービス
サービスは標準インターフェースを通じて特定の機能を提供します。例えば：
- 通信用のTelegramサービス
- ブラウザベースのダッシュボード用のWebサービス
- 外部シグナル用のWebhookサービス

### 通知機能
通知機能は様々なチャネルを通じてユーザーに情報を送信します：
- Eメール通知
- Telegramメッセージ
- Discordアラート
- カスタム通知チャネル

### インターフェース
インターフェースはユーザーがOctoBotシステムと対話することを可能にします：
- コマンドラインインターフェース
- ボットベースのインターフェース（Telegram、Discord）
- Webインターフェース

### サービスフィード
サービスフィードは外部データをOctoBot環境に取り込みます：
- TradingViewシグナル
- ソーシャルメディアフィード
- カスタムデータソース

## 使用例

### サービスの作成
```python
class MyCustomService(AbstractService):
    def get_type(self):
        return "my_service"
        
    def get_endpoint(self):
        return "https://my-service-endpoint.com"
        
    async def prepare(self):
        # サービス初期化コード
        pass
        
    def has_required_configuration(self):
        return all(key in self.config for key in self.get_required_config())
        
    def get_successful_startup_message(self):
        return "カスタムサービスが正常に起動しました！", True
```

### サービスの使用
```python
class MyServiceUser(AbstractServiceUser):
    REQUIRED_SERVICES = [MyCustomService]
    
    def __init__(self, config):
        super().__init__(config)
        # 初期化コード
```

## 設定
サービスはOctoBot設定システムを通じて設定されます。各サービスは以下を指定できます：
- 必須設定フィールド
- デフォルト値
- フィールドの説明
- 読み取り専用情報
```
services:
  my_service:
    enabled: true
    api_key: "あなたのAPIキー"
    secret: "あなたのシークレット"
```

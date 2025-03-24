# OctoBot-Services モジュール

## サービス
`services`モジュールはコアサービスシステムを提供します：
- `AbstractService`：すべてのサービスの基本クラス
- `ServiceFactory`：サービスインスタンスの作成と管理

## 通知
`notification`モジュールは通知システムを処理します：
- `AbstractNotifier`：通知送信の基本クラス
- 様々なイベント用の通知実装

## インターフェース
`interfaces`モジュールはユーザーインターフェースを管理します：
- `AbstractInterface`：すべてのインターフェースの基本クラス
- `AbstractBotInterface`：コマンドベースの対話用
- `AbstractWebInterface`：Webベースの対話用

## サービスフィード
`service_feeds`モジュールは外部データソースを処理します：
- `AbstractServiceFeed`：サービスフィードの基本クラス
- `ServiceFeedFactory`：サービスフィードインスタンスの作成

## マネージャー
`managers`モジュールはコンポーネントのライフサイクル管理を提供します：
- `ServiceManager`：サービスのライフサイクル管理
- `InterfaceManager`：インターフェースのライフサイクル管理
- `ServiceFeedManager`：サービスフィードのライフサイクル管理

## チャネル
`channel`モジュールは通信システムを実装します：
- `UserCommandsChannel`：ユーザーコマンド配信用
- `NotificationChannel`：通知配信用

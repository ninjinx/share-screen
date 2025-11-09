# uxplayを活用したWindows向けAirPlay戦略

## 1. uxplayの特徴
- OSS（GPLv3）、クロスプラットフォーム（Linux/WSL/Windows/FreeBSD）
- AirPlay1/2対応、低遅延映像・音声ミラーリング
- ハードウェアアクセラレーション対応
- Bonjour/mDNSによるデバイス検出
- コマンドライン操作・自動起動対応

## 2. 技術的優位性
- OSSで無償利用可能
- AirPlay2対応（OSSでは希少）
- WSL2環境で安定動作
- 高速デコード・低遅延通信

## 3. 既存OSS/商用資産との比較

| 製品/OSS         | AirPlay2 | Windows対応 | ライセンス | 低遅延 | サポート      |
|------------------|----------|-------------|------------|--------|--------------|
| uxplay           | ○        | WSL2経由    | GPLv3      | ○      | コミュニティ  |
| shairplay        | ×        | △           | GPL        | △      | コミュニティ  |
| OpenAirplay      | ×        | △           | GPL        | △      | コミュニティ  |
| AirServer        | ○        | ○           | 商用       | ○      | 商用サポート  |
| Reflector        | ○        | ○           | 商用       | ○      | 商用サポート  |

## 4. Windows環境での活用方法
- WSL2（Ubuntu）上でuxplayをビルド・運用
- Bonjour/mDNSサービスをWindows側で有効化
- 同一ネットワークセグメントでiOSデバイスと接続
- GPUアクセラレーション設定（必要に応じて）

## 5. 導入/運用フロー
1. WSL2（Ubuntu）をセットアップ
2. 必要パッケージ（libavcodec, libavformat等）をインストール
3. uxplayをビルド・インストール
4. Bonjour/mDNSサービスを有効化
5. uxplayを起動し、iOSデバイスから接続
6. 映像・音声ミラーリングを確認
7. トラブル時はログ・ネットワーク設定を確認

## 6. 推奨構成
- WSL2 + Ubuntu 20.04以降
- Windows 10/11
- Bonjour/mDNSサービス有効
- 同一LANセグメント
- GPUアクセラレーション有効化（推奨）

## 7. 注意点
- WSL/Windows間のネットワーク設定に注意
- AirPlay2の一部機能は未対応の場合あり
- 法的配慮（Appleプロトコル利用時のライセンス）
- OSSのためサポートはコミュニティベース
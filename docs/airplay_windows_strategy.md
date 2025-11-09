# AirPlayを利用したiOS画面ミラーリングWindowsアプリ 技術選定・戦略策定

## 1. AirPlayプロトコル概要とWindowsでの実装課題
- AirPlayはApple独自のワイヤレスストリーミング技術で、Bonjour（mDNS）によるデバイス検出、RTSP/HTTP/UDP/TCP通信、暗号化・認証が特徴です。
- Windowsでの実装課題は、非公開仕様・認証/暗号化対応・リアルタイム映像デコード・Bonjourサービス再現・法的配慮などが挙げられます。

## 2. 利用可能な言語・フレームワーク比較
| 言語/フレームワーク | パフォーマンス | 開発効率 | GUI対応 | OSS資産 | 備考 |
|--------------------|---------------|----------|---------|---------|------|
| C++                | 高            | 低       | WinAPI/Qt | 多い    | ネイティブ実装向き |
| Rust               | 高            | 中       | egui/GTK | 一部    | 安全性・高速性 |
| Python             | 低            | 高       | PyQt/Tkinter | 少ない | プロトタイプ向き |
| Electron           | 中            | 高       | HTML/CSS/JS | 少ない | GUI重視・パフォーマンス課題 |
| .NET (C#)          | 中            | 高       | WPF/WinForms | 一部   | Windows親和性 |

## 3. 既存OSSやライブラリの調査
- AirServer, Reflector（商用）
- OSS: [OpenAirplay](https://github.com/OpenAirplay/OpenAirplay), [airplay-protocol](https://github.com/philippe44/airplay-protocol), [Mirage](https://github.com/PhantomInsights/Mirage), [shairplay](https://github.com/juhovh/shairplay), [node-airplay-js](https://github.com/benvanik/node-airplay-js)
- Bonjour/mDNS: [Bonjour SDK](https://developer.apple.com/bonjour/), [zeroconf](https://github.com/jstasiak/python-zeroconf), [mdns](https://github.com/agnat/node_mdns)

## 4. 推奨技術スタックの選定理由
- コア実装はC++またはRust（パフォーマンス・低レベル制御・OSS資産活用）
- GUIは.NET (C#) またはElectron（Windows親和性・開発効率）
- mDNS/Bonjourは公式SDKまたはOSS（言語に応じて選択）
- C++/Rustは暗号化・認証・リアルタイム通信に最適、GUIはユーザビリティ重視

## 5. 開発戦略（段階的な実装方針、テスト・デバッグ方法）
1. プロトコル調査・PoC（OSSベースで最低限動作確認）
2. mDNS/Bonjour対応（デバイス検出・接続）
3. 映像・音声デコード（ハードウェアアクセラレーション検討）
4. 認証・暗号化対応（FairPlay/Device Verification）
5. GUI統合（Windows向け操作画面）
6. テスト・デバッグ（iOS複数台検証、パケットキャプチャ、ログ解析、ユーザーテスト）

### テスト・デバッグ方法
- Wireshark等でプロトコル解析
- 仮想デバイス・エミュレータ利用
- 単体/統合テスト自動化
- ログ出力・エラー通知強化

```mermaid
flowchart TD
    A[AirPlayプロトコル調査]
    B[mDNS/Bonjour対応]
    C[映像・音声デコード]
    D[認証・暗号化]
    E[GUI統合]
    F[テスト・デバッグ]
    A --> B --> C --> D --> E --> F
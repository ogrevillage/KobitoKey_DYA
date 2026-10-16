# 小人キー（KobitoKey_DYA）Compact5移植前の復元用バックアップ

## このバックアップの意味
- **日時：2026-10-16**。元のmainコミット：`7db66a39478356aae98c665da55d95ab6a03cd2a`。
- さらに丸ごと保存したブランチ：`backup/pre-compact5-20261016`（元のmainコミットと同一の状態を指す）。
- このディレクトリの `KobitoKey.keymap` は2026-10-16に稼働していた設計の**完全なコピー**。書き換え前のGit Blob SHA：`1fd95193e97696a55512a9b8bbb1cb9c11bf55e4`。
- `firmware/` 内の左右`.uf2`は、変更前のmainに実際に保存されていた既存ファームウェアの**完全なGit blob再利用**（ビルドを今から再実行したものではない）。各UF2が現在実機に入っているものと完全一致するかは別途確認が必要。
- **`settings_reset`は復元目的に含めない**：ペアリング情報を消すおそれがあるので、設定初期化を安易に実行しない。

## GitHub上のキーマップを戻す
1. このディレクトリの`KobitoKey.keymap`を`config/KobitoKey.keymap`に戻す。
2. 通常のビルドWorkflowの成功と左右UF2生成を確認する。
3. `keymap-drawer`内の図も必要なら通常のDraw Workflowで更新する。
4. 戻す際は小人キーL1 NUMBER・L3 MOUSE・L4 BTを含め、保管済みの全レイヤー・コンボが元どおりか確認する。

## 実機を元の動作に戻す
- 左右各キーボードに**対応する側の元のUF2**を、既に確認済みの安全な書き込み手順で使う。左右を混同しない。
- デバイスのブートローダー起動やドライブ名は機種・搭載ボードで異なるため、未確認の操作を行わない。
- このチャットから実機への直接書き込みは行っていない。
- Bluetoothのペアリングが消えることを避けるため、初期化UF2は利用しない（必要性が後で判明した場合のみ別途判断）。

## 元UF2のGitオブジェクト
- `KobitoKey_left rgbled_adapter-seeeduino_xiao_ble-zmk.uf2` : Git blob `c6df7c6b590bc0bcb20f6a8b8cf188b2a80320ac` (685568 bytes)
- `KobitoKey_right rgbled_adapter-seeeduino_xiao_ble-zmk.uf2` : Git blob `d508e1196594c2ac6532b13d796c4b86c5999f70` (459264 bytes)

安全のため、**保存フォルダは後続のキーマップ調整で上書きしない**。

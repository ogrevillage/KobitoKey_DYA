# KobitoKey_DYAへのCompact 5移植案（未適用・レビュー用）

**重要**：このフォルダの `KobitoKey.keymap` は実際のビルド対象ではありません。既存の `config/KobitoKey.keymap`、`keymap-drawer/`、ビルド／配布済みUF2は一切変更しません。

## 実リポジトリに基づくレイヤー対照

| Geonix Compact 5 | KobitoKey_DYA 実レイヤー | この案 |
|---|---|---|
| L0 BASE | L0 BASE | 移植（左Z長押しShift、右:長押しShift、右/長押しCtrlなど） |
| L1 NUM/SYMBOL | L5 NUMBER2 | 移植（数値・記号の位置、L5専用ShiftとEsc/Ctrl） |
| L2 FUNC | **L2 FUNCTION** | 移植候補。小人キー実L3はマウスにつき、L3には絶対に上書きしない |
| L3 BT/RGB | L4 BT | **変更なし**（元の5 Bluetoothプロファイルとペアリング操作を保持） |
| L4 MOUSE | L3 MOUSE | **変更なし**（元のクリック、L0戻りキーを保持） |
| -- | L1 NUMBER | **変更なし** |

**ユーザー指定の矛盾**：Geonix L2→小人キーL3と同時に、小人キーL3(MOUSE)を現状維持することは不可能です。そのためマウスを保護し、移植案では右Backspaceの`&lt 2 BACKSPACE`で起動する小人キーL2 FUNCTIONを試用候補として更新しています。小人キーL3/L4とL1は原文のバイト列を保持しています。これは**mainに未適用**であり、先にレイヤー番号を確認するためのドラフトです。

## 移植詳細とソース

- 比較対象：`ogrevillage/GeonixR2-QMK/variants/compact5/design.json`（L0・L1・L2・コンボ）。
- 元の小人キー：`ogrevillage/KobitoKey_DYA/config/KobitoKey.keymap`（ZMK構文）。
- **40キーのキー位置**：小人キーは10+10+10+10でGeonix Compact5と同じため、ZMKの`key-positions`を用いてコンボ位置を正しく調整。GeonixのVIA matrix値を流用しない。
- L0：`&kp LCTRL`、`&mt LSHIFT Z`、`&mt RSHIFT APOS`、`&mt RCTRL SLASH`。元の専用右Shiftは試しやすいよう維持。Enterは**元の単押しのまま**、マウスレイヤー起動に変更しない。
- **L0のレイヤータップ入替（2026-10-16 ユーザー指定）**：左Delは`&lt 5 DEL`（短押しDelete／長押しL5 NUMBER2）、右BSは`&lt 2 BACKSPACE`（短押しBackspace／長押しL2 FUNCTION）。Pの`&lt 4 P`（短押しP／長押しL4 BT）は維持。
- L5：右端上段テンキー割算、G=`LS(MINUS)`、H=`APOS`(JISコロン想定)、B=`INT3`、N=`COMMA`。Z物理位置はShift、左下は`&mt LCTRL ESCAPE`。
- L2：F1〜F10最上段、右HJKL=←↓↑→、右端中段F11、左A=Tab、Z=Shift、最下段左Ctrl位置=短Esc/長Ctrl。F12は未配置。
- **コンボ**：Q+W→Esc、A+S→Tab、D+F→英数、J+K→かな、括弧ペアは元のZMKコンボ維持。Z+X→Shiftは廃止。**O+P→長音はL0のみ**（L5は既存の`KP_MINUS`を使うためコンボ不要）。F+J→@をL0限定で追加（位置13+16、JISホスト向け`LEFT_BRACKET`）。
- 元のL1 NUMBERもそのまま残し、D+F／J+K／括弧ペアのL1コンボ有効状態は保持。
- **操作上の注意**：L2 FUNCには右BS長押し、L5 NUM2には左Del長押しで入ります。Geonixでの元の長押し担当と違うため、長押しキー自身の入力やコンボの競合を実機で確認してください。
- **注意**：ZMKのMod-Tap (`&mt`) への変更と物理`.`+`:`の括弧コンボ競合、`O+P`長音とPレイヤー切替、JISコード実出力は実機未確認。QMKをZMKに直訳して機械的に安全とは限らない。
- **キーマップ表現のみの試作**。ZMKのビルド・UF2生成・書き込みは行っていません。ビルドする際は必要な権限・環境で別途安全に検証。

## 変更対象と保護対象

レビュー承認後に初めて`config/KobitoKey.keymap`へコピー／修正し、`.github/workflows/build.yml`・`draw-keymap.yml`の結果を確認する。**現時点でビルド用`config/`や既存ファームウェアを更新しない**。Bluetooth、マウス、L1 NUMBERに影響があれば移植を中断する。

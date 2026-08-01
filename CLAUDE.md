# ogu_scan

## Project Type
web-app（静的 HTML/CSS/Vanilla JS、ビルドステップなし）

## Quality Standard
- iOS Safari 実機でカメラ起動・台形補正・PDF生成・Web Share が正常動作すること
- `index.html` 単体で完結する設計を維持すること（外部ビルドツール・バンドラー不要）

## Verification Criteria
- ロジック変更後は必ず iOS Safari 実機（または BrowserStack）で確認
- ローカル確認: `npx serve .` → http://localhost:3000
- HTTPS 必須機能（カメラ）のテストは Vercel デプロイ URL か localhost で行う

## Architecture Notes
- **単一ファイル構成**: すべてのロジック・スタイルは `index.html` に集約
- **ライブラリ（編集禁止）**:
  - `jspdf.min.js` — PDF 生成（jsPDF v2.5.1）。更新時は公式から再取得
  - `opencv.js` — 画像処理（OpenCV.js）。更新時は公式ビルドから再取得
- **外部送信なし**: 画像・PDF データはブラウザ内で完結。クラウド送信ロジックを追加しない

## Key APIs
- `MediaDevices.getUserMedia` — カメラ映像取得（HTTPS または localhost のみ動作）
- `Canvas 2D API` — フレーム取得・フィルター処理・台形補正
- `Web Share API` — iOS ネイティブ共有シート（iOS 15+ / Safari のみ）
- `jsPDF` — PDF バイナリ生成

## Project-Specific Overrides
- `jspdf.min.js` / `opencv.js` は直接編集禁止。変更が必要な場合はユーザーに確認を取ること
- 機能追加時も「サーバーレス・外部送信なし」の原則を維持する

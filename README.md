# ⚠️ このリポジトリは廃止されました（2026-07-20）

**株価分析ツールは kessan-tool（決算分析ツール）に統合されました。**
今後の利用・修正は、すべて kessan-tool 側で行ってください。

---

## 統合後の場所

| 項目 | 内容 |
|---|---|
| 統合先 | `kessan-tool` リポジトリ |
| 開き方 | kessan-tool を開き、上部タブの **「📉 株価分析」** を選択 |
| 正となるファイル | **`kessan-tool/stock-analysis.html`** |
| 実装方式 | kessan-tool の `index.html` に3つ目のタブを追加し、`stock-analysis.html` を iframe で表示（初回表示時に遅延ロード） |

## なぜコードを1ファイルに統合しなかったか

kessan-tool と本ツールは、同名で中身の違う関数・定数を多数持っており、
単純にコードを1つにまとめると **JS が停止するか、チャート描画が壊れます**。

- `const GROUNDING_RULE` が両方に存在 → 重複宣言で **SyntaxError（JS全停止）**
- `drawChart` が**引数の異なる別物**
  - kessan-tool: `drawChart(containerId, canvasId, dataStr)`
  - 株価分析: `drawChart(canvas, lines)`
- 他に `autoModelChain` / `callGeminiAnalyze` / `setGemStatus` / `tokenNote` /
  `trimChartByMonths` / `copyFactCheck` / `openKabutan` / `openIR` が衝突
- CSS 変数（`--accent` など）も相互に干渉

そのため「既存を壊さない」ことを最優先し、**iframe による分離読み込み**を採用しました。
既存2タブ（決算分析・個別銘柄分析）の CSS / JS / DOM は無改変です。

## このリポジトリの扱い

- **更新されません。** 参照用の残置です。
- Cloudflare Pages のデプロイは残っていますが、開くと廃止バナーが表示されます。
- 機能の履歴を追いたい場合のみ、本リポジトリのコミット履歴を参照してください。

## 補足（統合時のメモ）

- `functions/api/fetch-stock.js` は kessan-tool 側にも同等品があります。
  統合時、kessan-tool 版に `low`（取得範囲内の安値）を追加して上位互換にしました。
- API（`/api/analyze`・`/api/fetch-stock`）は kessan-tool と同一オリジンで動作します。
- `GEMINI_API_KEY` は Cloudflare Pages の**プロジェクトごと**に設定が必要です。

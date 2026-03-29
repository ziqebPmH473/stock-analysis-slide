# スライドCSS調整ガイド

`index.html` の `<style>` タグ内にあるCSSクラスを直接編集することで、余白・文字サイズ・列幅などを調整できます。

---

## 共通：全スライドの外側余白とフォント基準

```css
/* 例：スライド2の外側余白（上下・左右） */
.s2-wrap { padding: 44px 72px 40px; }
/*                  ↑上下  ↑左右  ↑下 */
```

| クラス名 | 対象スライド |
|---|---|
| `.s1-wrap` | スライド1 |
| `.s2-wrap` | スライド2 |
| `.s3-wrap` | スライド3 |
| `.s4-wrap` | スライド4 |
| `.s5-wrap` | スライド5 |

---

## スライド1：現状の整理

### 上段（現在値カード・指標カード・チャート）の高さ
```css
.s1-upper { height: 185px; }  /* 数値を大きくすると上段が高くなる */
```

### 現在値カードの幅
```css
.s1-price-card { width: 210px; }  /* 広くすると株価がゆったり表示される */
```

### 指標カードの幅
```css
.s1-metrics-card { width: 290px; }
```

### 現在値の文字サイズ
```css
.s1-price { font-size: 56px; }
.s1-change { font-size: 16px; }
```

### 指標ラベル・値の文字サイズ
```css
.s1-ml { font-size: 13px; }  /* ラベル（PER, PBRなど） */
.s1-mv { font-size: 20px; }  /* 値 */
```

### 下段：変動要因・強み・弱みの文字サイズ
```css
.s1-ftitle  { font-size: 14px; }  /* 各カードの小見出し */
.s1-factor  { font-size: 18px; }  /* 変動要因の各行 */
.s1-sw-title{ font-size: 14px; }  /* 強み・弱みの小見出し */
.s1-sw-item { font-size: 17px; }  /* 強み・弱みの各行 */
```

---

## スライド2：短期シナリオ

### 上段の参照指標（大きな数字）

```css
.s2-mb-num { font-size: 60px; }  /* 大きな数値（597円など） */
.s2-mb-lbl { font-size: 19px; }  /* ラベル（現在の基準株価など） */
.s2-mb-sub { font-size: 15px; }  /* 補足テキスト */
```

### 下段のシナリオ行：列幅の配分

```css
.s2-scen-row {
  grid-template-columns: 180px 230px 140px 1fr;
  /*                     ↑名前  ↑値域  ↑騰落率 ↑説明（残り全部） */
}
```

- `180px` = 「🔴 弱気シナリオ」の列
- `230px` = 「¥430〜500」の列
- `140px` = 「▼-28%〜-16%」の列
- `1fr`   = シナリオ説明文の列（自動で残りを埋める）

### シナリオ行の文字サイズ
```css
.s2-sr-name  { font-size: 20px; }  /* シナリオ名 */
.s2-sr-range { font-size: 28px; }  /* 想定レンジ（大きな数字） */
.s2-sr-pct   { font-size: 18px; }  /* 騰落率 */
.s2-sr-cond  { font-size: 16px; }  /* 説明文 */
```

---

## スライド3：12か月後シナリオ

### テーブルの列幅
```html
<!-- buildS3 関数内のHTMLを直接編集 -->
<th style="width:10%">シナリオ</th>
<th style="width:24%">目標レンジ</th>
<th style="width:20%">現在値比</th>
<th>前提条件</th>
```

### テーブルのフォントサイズ
```css
.s3-table th { font-size: 14px; }
.s3-table td { font-size: 17px; }
.s3-sc  { font-size: 17px; }  /* シナリオ名列 */
.s3-pc  { font-size: 24px; }  /* 価格列（大きめ） */
.s3-pct { font-size: 17px; }  /* 騰落率列 */
.s3-cd  { font-size: 16px; }  /* 条件文列 */
```

---

## スライド4：転換点のモノサシ

### インジケーター行のフォントサイズ
```css
.s4-iname { font-size: 20px; }  /* 指標名 */
.s4-ivals { font-size: 17px; }  /* 現在値→目安値 */
.s4-inote { font-size: 14px; }  /* 注記 */
```

### 行の縦方向の分散
```css
.s4-items { justify-content: space-evenly; }
/* space-between（端に寄せる）や center（中央に集める）も可 */
```

---

## スライド5：リスク

### リスクの小見出し（囲いの外）
```css
.s5-rtitle { font-size: 24px; }
```

### リスク内容の文字サイズ
```css
.s5-rlist li { font-size: 18px; }
```

---

## チートシート：よく使うpaddingの書き方

```css
padding: 上 右 下 左;        /* 4値 */
padding: 上下 左右;           /* 2値 */
padding: 40px 72px 40px;     /* 上・左右・下 */
```

## チートシート：grid-template-columns の書き方

```css
grid-template-columns: 180px 230px 140px 1fr;
/* 固定px幅を3列指定し、残りを1fr（自動）で埋める */

grid-template-columns: 1fr 1fr 1fr;
/* 3等分 */

grid-template-columns: 2fr 1fr 1fr;
/* 左を広めにした3列 */
```

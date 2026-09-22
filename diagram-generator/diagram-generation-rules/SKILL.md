---
name: diagram-generation-rules
description: Use when generating or reviewing explanatory diagram images that should convey an idea intuitively as AI-generated raster art.
---

# Diagram Generation Rules

## 適用範囲

説明用の図解画像を生成またはレビューするとき、表現と画像の仕様に以下の規則を適用する。段落との対応、文書への配置、個別の視覚スタイルは対象外である。

## 不変条件

- 画像は `$imagegen` で生成されたラスター画像である。SVG、HTML/CSS、canvas、その他のコードやベクター形式で描画された画像は該当しない。
- アスペクト比は正確に 16:9 である。
- 描画領域はフレームの外周まで使われ、外周の空白、余白、パディングは 0 である。主要な図と文字は、構図が許す限り大きく表示されている。
- 伝える主題とその関係を、画像だけを見ても大まかに理解できる。
- 正確性や完全性より直感的な理解を優先し、その理解に不要な説明や冗長な情報を含まない。
- 要旨を伝えるために必要な要素だけで構成され、文字と図は少なく大きい。

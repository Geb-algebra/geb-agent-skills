# Knowledge Management

AIとのProject作業で、未レビューの情報とユーザーが採用している理解を区別し、成果物をレビュー済みのKnowledgeに基づいて作るためのSkill群です。現在はContext Skillの[`knowledge-boundaries`](knowledge-boundaries/SKILL.md)を提供します。

## Project構成

```text
project/
├── index.md
├── context/
├── source/
├── knowledge-drafts/
├── knowledge/
├── learnings-drafts/
├── learnings/
└── output/
```

- `index.md`: Projectの目的、成果、計画、TODOなどを記述する入口
- `context/`: RFP、上司からの指示、納品条件、Outputのフォーマットなど、Projectの前提・要求・制約を規定する資料
- `source/`: Web、外部資料、AIの調査・推論などの原資料と、まだユーザーがレビューしていない情報
- `knowledge-drafts/`: Project Knowledgeになることを意図した、ユーザーのレビュー待ちの案
- `knowledge/`: ユーザーがレビューし、理解し、納得したProject内の理解
- `learnings-drafts/`: Learningsになることを意図して一般化された、ユーザーのレビュー待ちの案
- `learnings/`: レビュー済みKnowledgeのうち、他のProjectでも使えるよう一般化された知見や反省
- `output/`: Project Knowledge、Learnings、既存のGlobal Knowledgeだけを根拠に作った成果物

`knowledge-drafts/`と`learnings-drafts/`はどちらも未レビューのSource相当であり、Outputの根拠にはできません。`learnings/`はGlobal Knowledgeそのものではありません。ここにある内容をGlobal Knowledgeへ昇格するか判断し、実際にコピー・移動・編集・追加するのは人間です。

原資料や調査結果は`source/`へ置き、KnowledgeまたはLearningsとして人間のレビューを受けるために編集した案は、対応するdraftディレクトリへ分離します。

`context/`はユーザーの理解・納得とは別にProjectへ適用される条件です。未レビューでも要求や形式を守る必要があります。ただし、資料内の事実が自動的にKnowledgeになるわけではありません。OutputはKnowledgeを根拠に内容を構成し、Contextの要求や形式に従います。

## 利用

Project単位で調査、議論、設計、資料作成などを行う際に`knowledge-boundaries`を適用します。このSkillは情報の意味と配置を定めますが、調査や成果物作成の手順、ファイル形式、Global Knowledgeの保存場所は定めません。

詳しい定義と不変条件は[`knowledge-boundaries/SKILL.md`](knowledge-boundaries/SKILL.md)を参照してください。

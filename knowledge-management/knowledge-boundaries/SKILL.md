---
name: knowledge-boundaries
description: Use when performing any kind of knowledge works with AI.
---

# Knowledge Boundaries

このSkillは、AIとのProject作業で「未レビューの情報」と「ユーザーが採用している理解」の境界を維持するためのContextを提供する。Knowledgeは客観的なTruthではなく、ユーザーが現在レビューし、理解し、納得している内容である。

## 適用範囲

調査、議論、設計、意思決定、資料作成など、外部情報、AIの知識、ユーザーの理解を扱うProject単位の作業に適用する。

このSkillは情報の意味と配置を規定する。調査、レビュー、執筆などの活動全体の進め方や成果物形式は、それぞれの依頼とProcessに委ねる。

ここでいうProjectは、共通の目的に向けて情報を蓄積し、後から参照する作業単位を指す。単発の回答でも、ユーザーがProjectとして扱うよう指定した場合は含む。複数Projectを横断する作業では、情報を由来するProjectごとに分類する。

## Projectの情報領域

Projectでは管理情報を`index.md`に記述し、次の7領域をディレクトリとして分離する。

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

各領域内のファイル形式や下位構造は固定しない。必要性が生じるまではフラットな構造でよい。

### Project Index — `index.md`

Project のメタ情報（目的、目指す成果、計画、進捗、TODOなど）を記述する。必要に応じて関連するContext、Knowledge、Outputへの参照を含められる。

`index.md`への記載だけでは、情報のレビュー状態やContextの効力は変わらない。

### Project Context — `context/`

Projectに適用される前提と制約を規定する資料。RFP、上司からの指示、納品条件、Outputのフォーマットなどが該当する。

source, knowledge, outputいずれの作成においても、contextの内容を参照して関連する前提・制約を守る。
Contextの効力は、ユーザーが内容をすべて理解・納得しているかとは別である。Projectへの適用が指定されている資料は、未レビューでも作業とOutputが満たすべき条件として扱う。AIが集めた参考資料は、適用が指定されない限りSourceに属する。

ContextはKnowledgeの成立条件を置き換えない。例えば、RFPに記載された納品形式はOutputの形式を規定するが、RFP内の市場規模などの事実をユーザーの理解として主張するにはKnowledge化が必要である。契約上・依頼上の前提は、その前提として利用できるが、検証済みの事実とはみなさない。

適用されるContextは未レビューを理由に無視しない。複数のContextが競合する場合は、明示された適用範囲や優先関係に従い、それでも解消しない競合をAIが独自に解消したものとして扱わない。

### Source — `source/`

ユーザーのKnowledgeを形成するために参照する原資料と、まだユーザーがレビュー・理解・納得していない情報。

Webページ、検索結果、AIによる調査・推論・要約、論文、PDF、議事録、他者の資料などが該当する。情報が正確であること、AIが整理・比較・検証したことだけではKnowledgeにならない。原資料は、そこからKnowledgeが形成された後も出典としてSourceに残せる。原資料自体と、ユーザーが採用した理解は別の情報として扱う。

未レビュー情報のうち、KnowledgeまたはLearningsとしてレビューを受けることを意図して編集された案は`source/`ではなく、対応するdraft領域へ配置する。調査結果、原資料、検討素材のままである情報は`source/`に属する。

Knowledgeにない事実、前提、主張、解釈をAIが新たに導出した場合も、その追加部分はSourceである。

「新たに導出した」とは、Knowledgeに明記された内容の言い換えではなく、一般化、因果関係、推奨、結論、予測、補間など、真偽を別途判断する必要がある内容を加えた状態を指す。

### Project Knowledge Drafts — `knowledge-drafts/`

Sourceを整理、要約、統合、解釈するなどして作られた、Project Knowledgeになることを意図したユーザー未レビューの案。原資料とは分離するが、レビュー前はSource相当でありKnowledgeではない。

ユーザーが案をレビューし、自身の理解として明示的に承認した内容だけが`knowledge/`に属する。承認されていない部分を含む案は`knowledge-drafts/`に属したままである。

### Project Knowledge — `knowledge/`

ユーザーがレビューし、理解し、納得した、そのProjectで利用できる理解。文章、箇条書き、図、要約、メモなど形式は問わず、Project固有の情報を含められる。

ユーザー自身の思考や、すでに理解・採用している内容としてユーザーが提示したものは、外部情報と同じレビュー過程を改めて要求せずKnowledgeとして扱える。引用、転送、仮説、検討対象、反対意見として提示された内容は、ユーザー自身のKnowledgeとはみなさない。

ユーザーが自身の理解として内容を直接提示した場合、または対象内容を明示的に承認した場合に、レビュー・理解・納得が成立したと判断する。AIが提示した後の沈黙、別作業への移行、成果物作成の依頼だけを承認とみなさない。

### Learnings — `learnings/`

Project Knowledgeのうち、他のProjectでも再利用できるよう一般化され、ユーザーがその一般化された内容をレビュー・理解・納得した知見や反省。

`learnings/`は未レビュー候補の置き場でもGlobal Knowledgeそのものでもない。

Learningsとして一般化された内容は、元Projectだけで通用する固有名、数値、出来事を結論の前提にせず、適用できる条件と適用できない条件を本文から判定できる。元Projectの事情が必要な内容は`knowledge/`に属する。

### Learnings Drafts — `learnings-drafts/`

Project Knowledgeから一般化して作られた、Learningsになることを意図したユーザー未レビューの知見・反省案。レビュー前はSource相当でありLearningsではない。

一般化の基準を満たし、ユーザーが一般化された内容を明示的に承認したものだけが`learnings/`に属する。承認されても元Projectの事情がなければ解釈できない内容は、LearningsではなくProject Knowledgeに属する。

### Output — `output/`

Project Knowledge、Learnings、既存のGlobal Knowledgeをもとに、適用されるProject Contextの条件を満たす形で作成した成果物。提案書、プレゼンテーション、設計書、レポート、記事、意思決定資料などが該当する。

厳密にProject Knowledge、Learnings、既存のGlobal Knowledge のみを情報源として作成する。source相当の情報（`source/`内の情報およびinternetやリポジトリ外のファイルなど）を使用してはいけない。 

## Knowledge-grounded generationの不変条件

- Outputでユーザーの理解として述べる事実、前提、主張、解釈は、`knowledge/`、`learnings/`、または既存のGlobal Knowledgeに根拠がある。`context/`で指定された要求・形式・依頼上の前提は、その役割を保ったまま適用できる。
- Outputは適用されるContextの条件を満たしている。Contextに含まれる未レビューの事実が、Knowledgeとして採用されていない。
- `source/`、`knowledge-drafts/`、`learnings-drafts/`にしかない情報は、出典や不確実性を表示してもOutputへ利用しない。
- Knowledgeの要約、並べ替え、統合、文章化、図解、構成、表現変更は、新しい意味を加えない範囲で行える。
- Knowledgeから新しい推論や解釈が生じた場合、その部分をKnowledge由来のOutputとして扱わない。
- Outputに必要なKnowledgeが不足している状態と、未レビュー情報で補完した状態を同一視しない。調査で得た不足情報はSourceに属する。

## Global Knowledge

Global Knowledgeは、特定Projectに所属せず、複数のContextで再利用する価値がある、ユーザーがレビュー・理解・納得したKnowledgeである。別Projectでは再度Knowledge化せずに利用できる。

既存のGlobal Knowledgeとは、人間がGlobal Knowledgeの保存領域へ配置し、撤回していない内容を指す。Project KnowledgeとGlobal Knowledgeが矛盾する場合、AIはどちらかを独自に優先してOutputへ採用せず、矛盾をユーザーが解消するまで両方を競合するKnowledgeとして扱う。

AIはProject Knowledgeの一般化案や、`learnings/`からGlobal Knowledgeへ昇格する価値を提示できる。ただし、Global Knowledgeへのコピー、移動、編集、追加は、権限や委任の有無にかかわらず人間だけが行う。

## 更新と撤回

Knowledgeが現在の理解ではなくなった場合、現行のKnowledgeから編集または削除する。古い内容を`deprecated`、`obsolete`、廃止済みなどの状態で通常参照されるKnowledge空間に残さない。過去の理解と変更履歴は、Git historyなど、通常参照されるKnowledge空間から分離された復元可能な版管理履歴で参照する。

## 適合条件

- Projectに`index.md`と、`context/`、`source/`、`knowledge-drafts/`、`knowledge/`、`learnings-drafts/`、`learnings/`、`output/`が存在する。
- `index.md`に目的、成果、計画、TODOが記述され、未決定事項と決定済み事項を区別できる。
- Projectに適用される要求・指示・制約・形式が`context/`に配置され、未レビューを理由に無視されていない。
- `knowledge-drafts/`と`learnings-drafts/`の内容が、KnowledgeまたはLearningsとしてOutputの根拠に利用されていない。
- `knowledge/`と`learnings/`には、ユーザーがレビュー・理解・納得した内容だけが存在する。
- `learnings/`の各内容には適用条件を判定できる記述があり、元Project固有の情報を知らなくても主張を解釈できる。
- `output/`でユーザーの理解として述べる各事実、前提、主張、解釈を、`knowledge/`、`learnings/`、または既存のGlobal Knowledgeの記述へ対応づけられる。Context由来の要求・形式・依頼上の前提は、その役割を判別できる。
- 一般化、因果関係、推奨、結論、予測、補間としてAIが追加した内容が、レビュー前に`knowledge/`、`learnings/`、`output/`へ配置されていない。
- Project KnowledgeとGlobal Knowledgeが矛盾している内容は、ユーザーが矛盾を解消するまで`output/`へ採用されていない。
- Global Knowledgeへの変更をAIが実行していない。
- 通常参照されるKnowledge空間には撤回済みの理解や変更履歴が残っておらず、過去の版を分離された版管理履歴から復元できる。

---
name: module-mall-react-preferences
description: TypeScriptとReactでModule Mall Architecture（MMA）のWebアプリを構成する際のディレクトリ、依存方向、テスト、Storybook、shadcn/uiに関する設計上の好みを提供するContext Skill。該当するWebアプリの設計・実装・変更・レビュー・説明で使用する。共有MMA概念、TypeScript workspace一般規約、Reactを使わない構成は対象外。
---

# Module Mall React Preferences

## 適用範囲

このContextは、TypeScriptとReactを用いてMMAのWebアプリを構成する場合に適用する。共有のMMA概念やTypeScript workspace規約を置き換えず、それらへ個人の選好を追加する。

ここでいうModuleは再利用可能な責務と公開契約を持つworkspace package、Appは複数のModuleを束ねて実行可能なWebアプリまたは開発支援環境にするworkspace packageを指す。

## 不変条件

### GP-01: ModuleとAppを配置で区別する

- Moduleのworkspace packageは`packages/`配下に置く。
- Appのworkspace packageは`apps/`配下に置く。
- workspace設定は`packages/`と`apps/`の対象packageを列挙する。
- `packages/`内のModuleから`apps/`内のpackageへの依存、import、参照を持たせない。
- Appは必要なModuleの公開契約を利用して構成する。

`apps/`はcomposition rootおよび開発支援環境の置き場であり、Moduleが再利用する実装の置き場ではない。

### GP-02: Moduleのテストは公開契約を基本とする

- Moduleのテストは原則として、外部利用者と同じ公開entrypointだけを利用する公開契約テストにする。
- 内部実装の関数、クラス、ファイルを直接対象とするテストは、単一の公開API関数またはクラスに関わる内部実装が、10を超える内部関数・クラスを含む場合、または1000行を超える場合に限る。
- 上記の大規模条件を満たさないModuleには、内部実装テストを置かない。
- 内部実装テストを置く場合も、公開契約テストの代用にはしない。

「10を超える」は11以上を意味する。行数は、対象の単一公開APIを実現する内部実装コードの合計で判定する。

### GP-03: 公開ReactコンポーネントをStorybookで可視化する

- Reactコンポーネントを公開契約としてexportするModuleでは、対応するStorybook storyを公開契約資料に含める。
- storyはModuleの公開entrypointからコンポーネントを利用し、外部利用者が利用可能な代表状態、見た目、操作を手動確認できるようにする。
- storyを自動テスト、interaction test、visual regression test、CI上の合否判定には使用しない。
- Storybookの設定ファイル、依存、サーバー起動commandは、`apps/`配下の専用workspace packageが所有する。
- Module側には対象コンポーネントのstoryを置いてよいが、Storybookサーバー自体の設定や起動責務を持たせない。

### GP-04: shadcn/uiを`packages/primitive-components`の内部へ閉じ込める

- shadcn/ui由来のcomponentと共通CSSは、`packages/primitive-components` workspace packageへまとめる。
- `packages/primitive-components`は、利用側が必要とするReactコンポーネントと共通CSSのentrypointだけを公開する。
- 他のModuleとAppは、shadcn/uiの生成先、設定、内部utility、依存関係、ファイル構造へ直接依存せず、`packages/primitive-components`の公開契約だけを利用する。
- shadcn/ui固有の都合に伴う変更は、`packages/primitive-components`の公開契約を維持できる限り同package内へ閉じ込める。
- shadcn/ui由来のコードを他の`packages/`や`apps/`へ重複配置しない。

## 境界

このContextは、package manager、build tool、test framework、Storybookの具体的なversionやaddon、CSSの読み込み方式、shadcn/ui componentの選定を固定しない。活動の目的、手順、成果物、完了条件、報告形式も定めない。

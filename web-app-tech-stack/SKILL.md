---
name: web-app-tech-stack
description: React Router Framework Mode と Vite を中心に、Bun、shadcn/ui、Tailwind CSS、Base UI、oxlint、oxfmt、Vitest、Storybook、Zod、および Cloudflare Workers・D1・R2 を組み合わせる Web アプリの技術選択規則を提供する。React Web アプリの設計、実装、変更、レビュー、依存関係選定でこの標準スタックを適用するときに使用する。ブラウザへのデータ保存には localforage、サーバー DB への保存には Drizzle ORM と D1 を適用する。
---

# Web App Tech Stack

## 分類と適用範囲

この Skill を Context Skill として扱う。対象は、この標準スタックを採用する React Web アプリの設計、実装、変更、レビュー、説明とする。

技術の役割、選択条件、実行環境の境界、準拠状態だけを規定する。活動の目的、成果物、完了条件、作業順序、ディレクトリ構成、Route Module や UI コンポーネントの詳細な設計パターンは規定しない。それらはユーザーの依頼または併用する Process Skill と Context Skill に委ねる。

## 技術の役割

| 関心事 | 採用技術 | 役割と境界 |
|---|---|---|
| アプリケーション | React Router Framework Mode | ルーティング、レンダリング、データの読み書きに関するフレームワーク境界 |
| 開発・ビルド | Vite | React Router と統合する開発サーバーおよびビルド基盤 |
| パッケージとタスク | Bun | 依存関係、ロックファイル、スクリプト実行 |
| UI | shadcn/ui | アプリが所有して変更できる UI コンポーネントの第一選択 |
| UI プリミティブ | Base UI | shadcn/ui の下位層、および不足する振る舞いを補うヘッドレス UI |
| スタイル | Tailwind CSS | UI のスタイリングに使うユーティリティ CSS 基盤 |
| 入力境界 | Zod | 実行時バリデーションと、その契約からの型推論 |
| 静的品質 | oxlint / oxfmt | lint とフォーマットの標準実装 |
| 自動テスト | Vitest | ロジックとコンポーネントの振る舞いの検証 |
| UI 契約資料 | Storybook | 公開 React コンポーネントの利用可能な API、状態、振る舞いの記述 |
| ブラウザ保存 | localforage | 特定ブラウザ・端末に属する永続データまたは破棄可能なキャッシュ |
| サーバー実行 | Cloudflare Workers | サーバーコードの実行環境とリソース binding の境界 |
| 構造化データ | Drizzle ORM + D1 | サーバーが所有する照会可能な永続データ |
| オブジェクト | R2 | ファイル、画像、生成物などのバイナリまたは大容量データ |

「公開 React コンポーネント」とは、アプリまたはパッケージが利用者向けの公開エントリーポイントから export する再利用可能なコンポーネントを指す。その公開契約には props、variant、意味の異なる状態、利用者が観測できる振る舞いを含む。

## 判断知識

- localforage のデータは一つのブラウザ・端末に属し、オフライン利用やクライアント専用設定に適する。複数端末・複数利用者で共有する正本には適さない。
- D1 は関係、制約、検索、トランザクションを必要とする構造化データに適する。Drizzle はアプリコードと D1 の間のスキーマおよびクエリ境界になる。
- R2 はオブジェクト本体に適する。検索可能な属性、所有者、状態、R2 object key などの関係データが必要なら D1 に保持する。
- Storybook はコンポーネント利用者向けの契約資料であり、Vitest は振る舞いの正しさを検証する。どちらか一方で他方を代替しない。
- shadcn/ui は外部のブラックボックスなコンポーネントライブラリではなく、生成したソースをアプリが所有する。Base UI はアクセシブルな振る舞いを担い、Tailwind CSS は見た目を担う。

## 不変条件

- **T-01 アプリ基盤**: React アプリは React Router Framework Mode を Vite と統合して構成する。Library Mode、独立した SPA router、別のビルド基盤を同じ役割の代替として導入しない。
- **T-02 Workers 対応**: サーバーコードとサーバー依存関係は Cloudflare Workers 上で動作可能にする。Web 標準 API を基本とし、Node.js compatibility に依存する場合は Workers 設定にその依存を明示する。
- **T-03 Bun に統一**: パッケージの追加、lockfile、タスク実行を Bun に統一する。npm、pnpm、Yarn の lockfile や同じ役割の実行手順を併存させない。
- **T-04 UI の優先関係**: UI は Base UI をプリミティブ層とする shadcn/ui コンポーネントを第一選択にする。必要な契約を shadcn/ui が提供しない場合だけ Base UI を直接構成し、それでも不足する部分だけを独自実装する。
- **T-05 UI 基盤の一貫性**: 新たな UI プリミティブとして Radix UI などの競合する基盤を追加せず、Base UI に統一する。Tailwind CSS と競合する別のユーティリティ CSS 基盤を追加しない。
- **T-06 アクセシビリティの保持**: shadcn/ui または Base UI をラップ、変更、合成しても、keyboard 操作、focus 管理、ARIA の関係、disabled 状態など、元のアクセシブルな振る舞いを失わせない。
- **T-07 公開 UI 契約**: 公開 React コンポーネントには Storybook story を用意する。story は利用者と同じ公開 export を import し、各公開 variant と、loading、empty、error、disabled など該当する意味上異なる状態を観測できるようにする。
- **T-08 Storybook の独立性**: story は非公開実装への直接アクセスや本番バックエンドの稼働を前提にせず、公開 props、公開 provider、制御された fixture または mock だけで契約を表現する。
- **T-09 検証ツールの責務**: コードの lint には oxlint、フォーマットには oxfmt、実行時の振る舞いの自動テストには Vitest を使用する。同じ責務を持つ ESLint、Prettier、Jest などを併設しない。
- **T-10 境界の検証**: FormData、JSON、URL parameter、外部 API 応答、永続化データなど、信頼境界を越える未知の値を利用前に Zod schema で検証する。検証前の型 assertion だけで値を信頼しない。
- **T-11 契約の単一性**: Zod schema が実行時契約であるデータについて、対応する TypeScript 型を手書きで重複させず、schema から推論する。
- **T-12 ブラウザ保存の条件**: ブラウザにデータを永続化する場合は localforage を使用し、browser-only なコード境界からだけアクセスする。SSR または Worker の実行中に localforage を参照しない。
- **T-13 ブラウザ保存の所有権**: localforage に、複数端末・複数利用者で共有すべき正本、サーバー権限判定の根拠、漏えい時に問題となる秘密情報を保存しない。サーバーデータのコピーを置く場合は、破棄可能なキャッシュとして識別できる状態にする。
- **T-14 サーバー DB の条件**: サーバーで構造化データを永続化する場合は Drizzle ORM を介して D1 を使用する。D1 binding と Drizzle を browser bundle に含めず、Worker 側のコード境界に保つ。
- **T-15 DB 契約の一貫性**: D1 のテーブル、列、制約、index とアプリが利用する query は Drizzle schema および migration と一致させる。実環境だけに存在する手動 schema 変更を正本にしない。
- **T-16 オブジェクト保存**: バイナリまたは大容量オブジェクトは R2 に保存し、D1 row や localforage value をその本体の代替にしない。関係データが必要なオブジェクトは、R2 object key と必要な metadata の対応を D1 で表現する。
- **T-17 binding 境界**: D1 と R2 は Cloudflare Workers の環境 binding から取得する。認証情報、account 固有 ID、binding の実体をクライアントコードやソースコードに埋め込まない。
- **T-18 条件付き依存**: localforage はブラウザ永続化がある場合、Drizzle と D1 はサーバー DB がある場合、R2 はオブジェクト保存がある場合にだけ、その役割へ導入する。利用しない能力のために条件付き技術を必須依存にしない。

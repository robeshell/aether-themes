# Aether

[English](./README.md) · [简体中文](./README.zh-CN.md) · [日本語](./README.ja.md)

[![npm version](https://img.shields.io/npm/v/aether-themes?logo=npm)](https://www.npmjs.com/package/aether-themes)
[![npm downloads](https://img.shields.io/npm/dm/aether-themes?logo=npm)](https://www.npmjs.com/package/aether-themes)
[![Check package](https://github.com/robeshell/aether-themes/actions/workflows/check.yml/badge.svg)](https://github.com/robeshell/aether-themes/actions/workflows/check.yml)
[![License](https://img.shields.io/npm/l/aether-themes)](./LICENSE)

**コンテンツ中心の個人サイト向け、小さくフレームワークに依存しないテーマレイヤーです。**

Aether は、ブログ、ノート、フォトジャーナル、音楽アーカイブに、それぞれの雰囲気を与えます。特定の人のコンテンツ、ルート、フレームワークには依存しません。[W.Site](https://robeshell.github.io/) から抽出したビジュアルレイヤーです。

[デモサイトを見る](https://robeshell.github.io/) · [AI 正式セットアップ手順](./STARTER_PROMPT.md) · [npm パッケージを見る](https://www.npmjs.com/package/aether-themes)

## Aether は何か、何ではないか

Aether はフレームワークに依存しない CSS テーマレイヤーです。完成済みのブログテーマ、サイトジェネレーター、CMS ではありません。ルート、コンテンツモデル、管理画面、すべてのブログ基盤向けのテンプレートは提供しません。

ガイド付きのセットアップはデフォルトで Astro を使いますが、パッケージ自体に Astro のランタイム依存はありません。グローバル CSS を読み込み、HTML を出力し、[`THEME_CONTRACT.md`](./THEME_CONTRACT.md) に記載されたセマンティックフックを追加できるフレームワークや静的サイトジェネレーターに統合できます。

| 環境 | 統合レベル |
| --- | --- |
| Astro | 正式なスターターワークフローに対応 |
| Eleventy またはプレーン HTML | CSS を直接統合可能 |
| その他の HTML 出力フレームワーク／静的サイトジェネレーター | テンプレートを契約に合わせれば利用可能 |
| 既存 CMS やブログのマークアップ | そのままでは非対応。テンプレートアダプターまたはローカル上書きが必要 |

つまり、Aether は移植できますが、すべてのブログシステムで設定なしに動くわけではありません。マークアップ、コンテンツ、ルート、インタラクションは利用側のサイトが管理します。

## Aether の特徴

- **7 つの切り替え可能なテーマ**を、1 つのセマンティックなマークアップ契約で利用できます。
- **必要なテーマだけ読み込み**、サイトが提供するテーマだけを配信できます。
- **フレームワーク非依存**で、Astro、Eleventy、プレーン HTML などの静的サイトツールに対応します。
- **AI と相性のよい導入フロー**として、リポジトリから発見できる Skill と、コピーして使えるセットアッププロンプトを提供します。
- **ランタイム依存なし**。ゲームや映像作品の著作権画像、スクレイピング素材は同梱しません。

## テーマ

| テーマ | 方向性 |
| --- | --- |
| `minimal` | 静かな余白と編集的な秩序 |
| `magazine` | 紙面、カラム、印刷のリズム |
| `terminal` | 蛍光グリーン、グリッド、コマンドラインの手触り |
| `cyber` | 警告イエロー、シアンの診断線、硬質なパネル |
| `island` | 明るい島の暮らしと柔らかな角丸 |
| `wilds` | アースカラー、遺跡、広がりのある空間 |
| `persona` | 赤と黒、切り紙、予告状の構成 |

すべてのテーマは同じセマンティックフックを使います。ルート要素の属性を変えるだけで切り替えられます。

```html
<html data-theme="persona">
```

## クイックスタート

サイトのプロジェクトでインストールします。

```sh
npm install aether-themes
```

まず基礎スタイルを読み込み、その後に必要なテーマを読み込みます。

```css
@import 'aether-themes/foundation.css';
@import 'aether-themes/themes/minimal.css';
@import 'aether-themes/themes/persona.css';
```

すべての組み込みテーマを使う場合は、便利なエントリーポイントを利用できます。

```css
@import 'aether-themes/all.css';
```

Aether が提供するのはビジュアルレイヤーだけです。HTML、コンテンツ、ルート、テーマピッカー、インタラクションは利用側のサイトが管理します。

## 必要なテーマだけを読み込む

[`aether.config.example.mjs`](./aether.config.example.mjs) をサイトにコピーして `aether.config.mjs` として保存し、不要なテーマを削除します。

```js
export default {
  themes: ['minimal', 'persona'],
  defaultTheme: 'minimal',
};
```

設定からテーマのインポートバンドルを生成します。

```sh
npx aether-themes \
  --config aether.config.mjs \
  --output src/styles/aether-themes.css
```

ジェネレーターはテーマ名、重複、`defaultTheme` を検証します。テーマピッカーも同じ `themes` 配列を読み込み、無効なテーマを表示しないようにしてください。ラベルと説明は利用側のサイトで管理し、Aether をコンテンツ非依存に保ちます。

## AI でサイトを作成する

正式にサイトを作るときは、サイトのルートにする空のディレクトリを開き、このリポジトリを参照として AI エージェントに渡してください。Aether テーマリポジトリ自体をサイトの作業ディレクトリにしないでください。Aether は依存関係とビジュアルレイヤーであり、ファイル、コンテンツ、ルート、設定を所有するのはサイト側です。

ターミナルに慣れていない場合は [`STARTER_PROMPT.md`](./STARTER_PROMPT.md) を使ってください。サイト名、説明、署名、セクション、言語、テーマを先に質問し、計画を確認してから現在のサイトディレクトリに正式なサイトを作成します。現在のワークスペースが Aether テーマリポジトリなら、ファイルを作成せず停止します。

最短の引き継ぎメッセージ：

```text
https://github.com/robeshell/aether-themes/blob/main/STARTER_PROMPT.md を読んでください。まずサイト作成の要件を質問し、私が確認してから、現在のワークスペースを正式なサイトのルートとしてサイトを作成・起動してください。aether-ai-smoke-test などのテストディレクトリは作成しないでください。現在のワークスペースが aether-themes リポジトリなら停止し、サイト用の別ディレクトリに切り替えるよう案内してください。
```

Aether パッケージ自体を保守する場合は [`SMOKE_TEST_PROMPT.md`](./SMOKE_TEST_PROMPT.md) を使ってください。これはリポジトリ内に `aether-ai-smoke-test/site` を作成し、npm パッケージとジェネレーターを検証するためのもので、ユーザーサイトの作成には使いません。

すでに Aether サイトがある場合は [`UPDATE_PROMPT.md`](./UPDATE_PROMPT.md) を使ってください。コンテンツ、設定、ローカルスナップショット、未コミットの変更を保ったままテーマを更新し、CSS を再生成してサイトを検証します。

## マークアップ契約

Aether は固定ルートのページを生成するのではなく、セマンティックフックにスタイルを適用します。画像、動画、音声、コード、数式、ギャラリーを含む必須フックとリッチコンテンツフックは [`THEME_CONTRACT.md`](./THEME_CONTRACT.md) を参照してください。

利用側のサイトが管理するもの：

- コンテンツコレクションと frontmatter
- ルートとページ構成
- テーマピッカーの状態と永続化
- サイトの文言とラベル
- アセットのライセンスとサイト固有の上書き

## オプション画像

Aether はスクレイピング画像やフランチャイズ画像を同梱しません。`cyber`、`terminal`、`wilds` にはオプションの画像変数があります。

```css
:root[data-theme="cyber"] {
  --aether-cyber-dots-image: url('/assets/cyber/dots-yellow.png');
}

:root[data-theme="terminal"] {
  --aether-terminal-rain-image: url('/assets/terminal/matrix-rain.svg');
}

:root[data-theme="wilds"] {
  --aether-wilds-header-image: url('/images/wilds-header.png');
}
```

これらの変数はデフォルトでは画像を読み込まないため、追加素材なしでもテーマは動作します。自分が所有している、または再配布の許可を得た素材だけを追加してください。

## 開発

このパッケージにはランタイム依存がありません。公開内容は次のコマンドでローカル確認できます。

```sh
npm pack --dry-run
```

同じチェックは、すべての push と pull request で [GitHub Actions](https://github.com/robeshell/aether-themes/actions/workflows/check.yml) により実行されます。

## コントリビュート

変更は [`THEME_CONTRACT.md`](./THEME_CONTRACT.md) のセマンティックフックを対象にし、基礎レイヤーをコンテンツ非依存に保ち、利用側が必要なテーマだけを選べる状態を維持してください。プルリクエストの前に `npm pack --dry-run` を実行し、パッケージ内容を確認してください。

リリース手順は [`PUBLISHING.md`](./PUBLISHING.md) を参照してください。公開する変更ごとにバージョンを上げます。

## ライセンス

MIT。詳しくは [`LICENSE`](./LICENSE) を参照してください。

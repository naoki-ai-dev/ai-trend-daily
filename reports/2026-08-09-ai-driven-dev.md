# AI駆動開発の動向レポート

## Claude Codeの自動化・権限モデルの刷新

- AnthropicはClaude CodeのPro/Max/Teamプランにおいて、「Auto mode」をデフォルト設定に変更した。これによりユーザーが個別に許可を出さなくても、一定のリスク判断のもとでコマンド実行が自動化される運用が標準になる。
- この変更を受けて、auto modeの内部で使われる"classifier"がどのように許可・ブロックを判定しているかを解説する記事も登場した。権限モードは6種類存在し、classifierがコマンドのリスクを評価して自動実行の可否を振り分ける仕組みが明らかにされている。
- 自動化が進む一方で、無人実行（夜間バッチ的な運用）を狙って「信頼済みコマンド」を設定しても、実際にはunattended実行までは対応しておらず、`claude --help`を精査して初めて見落としに気づいたという報告もあり、自動化機能の設計と実運用の間にはまだギャップが残っている。

## マルチエージェント連携・オーケストレーションの進展

- Claude Codeに、実行中の別セッションへメッセージを送る「Cross-session messaging」機能が追加された。これにより、複数のエージェントセッションを並行稼働させ、互いに指示や進捗を伝達し合う協調的なワークフローが実現しやすくなる。
- 開発現場では、Claude Code・Cursor・Geminiなど複数のAIツールを横断的に使いこなす役割そのものを「AIオーケストレーター」として定義する動きが出ている。単一ツールの操作スキルではなく、複数エージェントを配置・調整する能力が新しい職能として言語化されつつある。
- エージェント間通信についても、画面上に「ご報告申し上げます」と表示するだけでは実質的な報告になっていないという指摘があり、通知や状態共有の仕組みそのものを設計し直す必要性が論じられている。

## プロトコル層の変化：MCPのステートレス化

- 2026年7月28日付の仕様更新により、MCP（Model Context Protocol）がステートレス化される変更が加えられた。セッション状態をサーバー側で保持する従来の前提が見直され、リクエスト単位での独立性が高まる方向性が示されている。
- この変更はMCPを利用するエージェント基盤の実装やスケーリング設計に影響を与えるため、プロトコルの薄い変更に見えて実際には運用アーキテクチャに波及する内容として注目されている。

## モデル評価と競合ハーネスの台頭

- Claude Opus 5を1週間使用したレビューでは、実務での挙動や旧モデルとの差分が具体的に検証されており、モデル更新のたびに実運用での再評価が求められる状況が続いている。
- Claude Code自体をベンチマークで上回ると主張する新しいコーディングハーネス「Benzi」がHacker Newsで紹介された。同じSonnetモデルを使いながらもハーネス側の設計次第で成果が変わることを示す事例であり、エージェント実行基盤（ハーネス）の設計競争が本格化していることを示唆している。

## エージェント市場の広がりとリスク事例

- 自律度と提供形態を軸に33のエージェント製品をカオスマップとして整理する試みが公開され、乱立するAIエージェント製品を俯瞰的に理解する動きが強まっている。市場は特定ベンダー依存ではなく、多様なレイヤーで製品が分化していることが可視化された。
- 一方でリスク事例として、Grok Buildにまつわる「ソース公開」インシデントの直前に何が起きていたかを追った記事があり、AIが生成・運用するプロダクトのソースコード管理や公開範囲の統制が実務上の課題として浮上している。

## 基礎理解のための整理の動き

- AIエージェントを個別ツール名ではなく、共通のレイヤー（Layer）構造で捉え直すリファレンスアーキテクチャが提案されている。プランニング層、実行層、ツール層などに分解することで、乱立するツール群を横断的に比較・理解しやすくする狙いがある。
- こうした整理は、Auto modeの浸透やマルチエージェント連携、プロトコル変更など個別の技術トピックを俯瞰する共通言語としても機能し始めている。

## 出典

- [Message your other Claude Code sessions](https://code.claude.com/docs/en/cross-session-messaging)
- [Auto mode is now the default in Claude Code for Pro, Max, and Team plans](https://simonwillison.net/2026/Aug/8/auto-mode/#atom-everything)
- [Claude Codeの権限モードは6種類。auto modeの"classifier"が許可とブロックをどう決めているか？](https://qiita.com/startdevin/items/e5828695a3e468a79976)
- [「信頼済みコマンド」を設定しても夜間オート実行はできなかった - claude --helpで分かった見落とし](https://zenn.dev/devex12/articles/claude-code-unattended-permission-mode-gap)
- [Claude CodeもCursorもGeminiも使っている。それは何という仕事なのか ── AIオーケストレーターの定義](https://zenn.dev/leading_ai/articles/46c4ff5241abba)
- [#3「ご報告申し上げます」と画面に表示しただけでは、報告にならない — AIエージェント間通信の進化史](https://zenn.dev/chisatom/articles/68ee26e2969f5a)
- [MCP Went Stateless: What the 2026-07-28 Spec Actually Changes](https://dev.to/krlz/mcp-went-stateless-what-the-2026-07-28-spec-actually-changes-273k)
- [Claude Opus 5を1週間使って分かったこと](https://zenn.dev/horizon_it00/articles/claude-opus5-one-week)
- [Show HN: Try Benzi – A coding harness/agent beating Claude Code itself on Sonnet](https://benzi.fly.dev/about)
- [Agent Product徹底比較 — 33製品を自律度×提供形態のカオスマップで整理する](https://zenn.dev/taka4/articles/cfbced9a440782)
- [Grok Build事件「ソース公開」の2日前に何が起きたか](https://zenn.dev/shuhari_ai/articles/31e8c37837d5a1)
- [AIエージェントを理解したい人に捧げる地図 — ツール名でなく層(Layer)で理解するReference Architecture](https://zenn.dev/taka4/articles/177ff2ac44587b)

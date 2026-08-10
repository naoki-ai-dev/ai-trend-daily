## Claude Codeの機能強化ラッシュ

- Claude CodeでAuto modeがデフォルトの実行モードとなり、タスクの複雑さに応じてモデルやツール利用をエージェント側が自律的に調整する運用が標準になった。ユーザーが実行モードを都度選ばなくても、適切な粒度で作業を進められる設計への転換といえる。
- macOS版Claude Codeでは、複数セッション同士が直接やり取りできる機能が追加された。並列で動く複数エージェントが情報を共有しながら作業を進められるようになり、単一セッション内で完結しない大規模な自律開発フローが現実味を帯びてきている。
- サブエージェントの起動数上限（200）が撤廃され、1セッションからより多くのサブエージェントを展開できるようになった。大規模タスクの並列分解やマルチエージェント・オーケストレーションの設計自由度が大きく広がっている。

## AIエージェント基盤・フレームワークの進化

- エージェントフレームワーク「Mastra」は、長時間稼働するエージェントの実行管理、実行トレースを解析する「Trace Intelligence」、エージェントを継続的に生産する「Factory」構想を打ち出した。単発タスク実行型から継続稼働型のエージェント運用基盤へと軸足を移す動きが見て取れる。
- マルチエージェント時代の実行制御レイヤーである「Execution Engine」を横断比較する記事が公開され、各ツールの実行制御・スケジューリング方式の違いがカオスマップとして整理された。エージェント基盤の選定軸が、単純な性能比較から「実行制御の設計思想」へ移りつつあることを示している。

## 業界動向:モデル・サービスの変化

- GitHub Modelsサービスが正式に終了（retire）し、GitHub上で複数のLLMを手軽に試せる仕組みが役目を終えた。プラットフォーム統合が進む中、開発者は代替のモデルアクセス手段への移行を迫られている。
- Anthropicの新モデルClaude Opus 5のシステムプロンプトが公開・引用され、モデルの振る舞い制御方針を読み解く材料として注目を集めている。
- 自律エージェント「OpenClaw」に関する言及が広がりを見せており、汎用エージェントの実装・運用に対する関心の高まりがうかがえる。

## マルチエージェント運用の課題と実践知

- Claude Code上で4つの異なるモデルを連携させたマルチモデル・オーケストレーションの検証では、Terminal-Bench上で4通りの失敗パターンが報告された。複数モデルの単純な組み合わせは必ずしも性能向上につながらず、責務分担やハンドオフ設計の難しさが浮き彫りになっている。
- 「コードレビューをやめる」というテーマの記事では、AIエージェント導入に伴う開発プロセスの変化が3段階の進化モデルとして整理された。レビュー工程そのものの位置づけが、AI駆動開発の中で変わりつつあることを示唆している。

## まとめ

- Claude Codeを中心に、単発の指示応答から「自律的に長時間動く」「複数エージェント・複数モデルが連携する」方向への進化が加速している。
- 一方で、モデルやエージェントを単純に増やすだけでは効果が出ないケースも報告されており、実行制御・トレース可視化・役割分担といった「運用設計」が今後のAI駆動開発の重要な論点になっていくと考えられる。

## 出典

- [Mastra YouTube 解説] Mastra新章: 長時間稼働エージェントとTrace Intelligence、Factory構想](https://zenn.dev/shiromizuj/articles/27696ae3851aa1)
- [GitHub Models is now retired](https://simonwillison.net/2026/Aug/9/github-models-is-now-retired/#atom-everything)
- [Quoting Claude Opus 5 system prompt](https://simonwillison.net/2026/Aug/9/claude-opus-5-system-prompt/#atom-everything)
- [Quoting OpenClaw](https://simonwillison.net/2026/Aug/10/openclaw/#atom-everything)
- [Auto mode is now the default in Claude Code](https://claude.com/blog/auto-mode-default-in-claude-code)
- [Claude Code now lets sessions talk to each other on macOS](https://9to5mac.com/2026/08/07/claude-code-now-lets-sessions-talk-to-each-other-on-macos/)
- [Claude Code no longer limits sessions to 200 spawned subagents](https://github.com/anthropics/claude-code/commit/66edf5358349356774812264b75b8ea792f0d0a3)
- [I wired 4 models together in Claude Code. It backfired 4 ways on Terminal-Bench](https://quesma.com/blog/tbench-orchestrator-refuses/)
- [Execution Engine徹底比較 — マルチエージェント時代の実行制御レイヤーをカオスマップで整理する](https://zenn.dev/taka4/articles/67cf58d191580c)
- [「コードレビューをやめる」は3段階で進化する ― あなたはどの段階？](https://zenn.dev/quon_agents/articles/ai-code-review-evolution)

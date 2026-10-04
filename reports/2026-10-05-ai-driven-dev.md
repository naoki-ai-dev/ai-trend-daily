# AI駆動開発の動向レポート（2026年10月5日）

## 概観：焦点は「モデル」から「ハーネス」へ

- 本日の記事群で最も目立つのは、AIエージェントの成果を左右する要因として、モデル単体よりも周辺の実行環境、つまり「ハーネス」に注目する議論です。
- 運用面でも、評価（eval）、コンテキスト管理、トークン効率、ログ保全といった仕組みづくりの話題が中心になっています。AI駆動開発は「試す段階」から「工学的に運用する段階」へ移りつつあります。
- 大規模なPR処理や無人の自律ループ、AIのみで書かれたプロダクトなど、AIに任せる範囲を極端に広げた実例も相次いでいます。

## ハーネス設計が成果を左右する

- 「AI エージェントの実力はモデルで決まる？」は、6,204回の実験から、モデルとハーネスの組み合わせ（相性）が性能に影響することを示した記事です。
- 同じモデルでもハーネス次第で結果が変わるなら、モデル選定と同じくらいハーネス選定や設計が重要になります。ベンチマーク結果を読むときにも、どのハーネスで測ったかの確認が欠かせません。
- 「11のCoding Agentから見る『Agent Harness』の設計原則」は、Claude Code、Codex、Hermes、Piなど11のコーディングエージェントを比較し、ハーネスに共通する設計原則を整理しています。
- この2本は、実験による定量的な裏付けと、既存製品の横断的な分析という別々の角度から、同じ論点を補強しています。
- 開発者にとっての示唆は、エージェントを「モデルの選択」ではなく「モデル＋ツール群＋制御ループの設計」として捉え直す必要があるという点です。

## 大規模・自律運用の実例

- 「月2,500件のPRはどう回っているのか」は、pstack作者のPoteto氏とMatt氏の対談をまとめた記事です。AIエージェントを前提に月2,500件規模のPRを回す開発体制が紹介されています。
- この規模では人間が1件ずつ丁寧にレビューする前提は成り立ちません。レビュー、検証、マージの流れそのものを再設計する必要があることがうかがえます。
- 「Claude Code を毎時起動して、クオンツ研究を仮説から本番投入まで無人で回している仕組み」は、Claude Codeを定期実行し、仮説立案から本番投入までを無人ループで回す事例です。
- この記事のURLには「decision-table」とあり、自律ループでは判断基準を明示的なルールとして事前に定義しておくことが鍵になると読み取れます。
- 「jpm」は、Rust製のJavaScriptパッケージマネージャーを全行Claude Codeで書いたというShow HNの投稿です。パッケージマネージャーのような実用インフラまでAIのみで構築を試みる段階に来ていることを示しています。

## 評価（eval）の導入と計測文化

- 「AIエージェント運用に eval を入れたら、直すべき場所が逆だった」は、6つの場面でtrain/testを分けて計測した記録です。直感で「ここを直すべき」と考えていた箇所が、計測の結果、逆だったと報告しています。
- 機械学習で一般的なtrain/test分離を、プロンプトやエージェント設定の改善にも持ち込む姿勢が特徴です。過剰適合を避けながら改善を進める手法として参考になります。
- 前述の6,204回実験の記事と合わせると、エージェント開発でも「感覚ではなく計測で判断する」文化が広がりつつあると言えます。

## コンテキストとトークンの効率化

- 「MCP を直接呼ぶ版とコードで叩く版」は、同じ集計タスクで、MCPツールを直接呼ぶ方式とコード経由で呼ぶ方式のトークン消費を実測・比較した記事です。
- ツール呼び出しの設計がトークンコストに直結するため、MCPの使い方そのものが最適化の対象になっています。
- 「Claude Codeのcompactionをロスレスにしたら、52秒が0.26秒になった」は、コンテキスト圧縮（compaction）をロスレス化した結果、処理時間が52秒から0.26秒に短縮されたと報告しています。
- 長時間セッションでの情報の欠落と待ち時間は、エージェント運用の大きな摩擦要因です。これをツール側の工夫で解消しようとする動きが、コミュニティ主導で進んでいます。

## エコシステムと運用上の注意点

- 「The Missing Middle」は、エージェントのスキルをプロンプトとして配るだけでは不十分で、パッケージマネージャーのような依存関係やバージョンの管理の仕組みが必要だと論じています。
- スキルやプラグインの数が増えるほど再利用性と互換性の管理が課題になり、ソフトウェア配布と同様の基盤整備が求められることを示す議論です。
- 「Claude Code deletes your old session logs after 30 days by default」は、Claude Codeが既定で30日経過した古いセッションログを削除する点に注意を促しています。
- セッションログを作業記録や振り返り、監査の材料として使っている場合は、保持設定の見直しやバックアップが必要です。運用設計で見落としやすいポイントと言えます。

## 今後の注目点

- ハーネスの比較・評価手法が標準化され、モデル性能とハーネス性能を分けて議論する土台が整うかが注目されます。
- 大量のPR処理や無人ループのような高度な自律運用が、一部の先進チームから一般の開発組織へどこまで広がるかも焦点です。
- スキルの配布基盤、トークン効率化、ログ保全といった「運用の地味な部分」の成熟度が、AI駆動開発の実用性を左右していくと考えられます。

## 出典

- [AI エージェントの実力はモデルで決まる？ 6,204 回の実験が示した「ハーネス」との相性](https://zenn.dev/takuh/articles/23d3c82222e264)
- [Claude Code、Codex、Hermes、Piなど11のCoding Agentから見る「Agent Harness」の設計原則](https://zenn.dev/ryodev/articles/3dbd9d26e3a094)
- [月2,500件のPRはどう回っているのか：pstack作者 Poteto さんと Matt さんの対談まとめ](https://zenn.dev/yukkie1114/articles/poteto-pstack-2500-prs)
- [Claude Code を毎時起動して、クオンツ研究を仮説から本番投入まで無人で回している仕組み](https://zenn.dev/toshipon/articles/autonomous-loop-decision-table)
- [Show HN: jpm – a JavaScript package manager in Rust, every line by Claude Code](https://getjpm.sh/)
- [AIエージェント運用に eval を入れたら、直すべき場所が逆だった — 6つの場面で train/test を分けて測った](https://zenn.dev/mameresearcher/articles/ai-agent-ops-evals-six-scenes)
- [MCP を直接呼ぶ版とコードで叩く版、同じ集計タスクで実際にトークンを数えてみた](https://zenn.dev/ma2no4413/articles/mcp-code-execution-token-benchmark)
- [Claude Codeのcompactionをロスレスにしたら、52秒が0.26秒になった](https://zenn.dev/yottayoshida/articles/lossless-compaction-v070)
- [The Missing Middle: Why Agent Skills Need Package Managers, Not Just Prompts](https://dev.to/thelazzziest/the-missing-middle-why-agent-skills-need-package-managers-not-just-prompts-57bh)
- [Claude Code deletes your old session logs after 30 days by default](https://brycewatson.com/blog/28-claude-code-deletes-old-logs/)

# AI駆動開発の動向

## 開発者の役割の変化：コーダーからオーケストレーターへ

- GitHub Blogの記事「[From coder to orchestrator](https://github.blog/developer-skills/career-growth/from-coder-to-orchestrator-how-agents-shift-the-role-of-a-developer/)」では、AIエージェントの台頭により開発者の役割が「自らコードを書く人」から「複数のエージェントに指示を出し、結果を検証・統合する人」へとシフトしていると指摘されている。
- これは単なる生産性向上の話ではなく、コードレビューやタスク分解、品質保証の設計が開発者の中心業務になることを意味する。
- 個人開発の現場でも同様の変化が見られ、Vibe coding（AIに大枠を任せて素早く作る開発スタイル）が本番運用に持ち込まれるケースが増えている。
- ただし本番化には課題があり、「[Vibe codingの本番化に必要なのは、プロンプトではなく「昇格マニフェスト」だ](https://zenn.dev/heftykoo/articles/5770d711add672)」では、プロトタイプから本番運用へ「昇格」させる際に必要な明文化されたルール・責任範囲の整備（昇格マニフェスト）の必要性が論じられている。
- プロンプトの工夫だけでなく、誰が何を承認し、どの基準で本番投入を判断するかというガバナンスの仕組みづくりが、AI駆動開発の成熟における次の課題として浮上している。

## エージェントのルール・ガバナンス管理

- AIコーディングエージェントの挙動を制御するための「ルールファイル」管理が、複数の記事で共通のテーマとして扱われている。
- 「[AGENTS.md, explained for teams that actually ship](https://dev.to/arpituppal2rgb/agentsmd-explained-for-teams-that-actually-ship-13c3)」は、チーム開発でエージェント向けの共通ルールファイル（AGENTS.md）を運用する際の実践的な考え方を解説している。
- 一方で「[Generating your agent rules from one file does not stop them drifting](https://dev.to/untactit/generating-your-agent-rules-from-one-file-does-not-stop-them-drifting-3gpb)」は、単一の元ファイルから各種エージェント設定を自動生成しても、運用が長期化するとルールが実態から乖離（ドリフト）していく問題を指摘している。
- ルールファイルの整備は「作って終わり」ではなく、継続的なメンテナンスと検証が必要であるという認識が広がりつつある。
- Claude Code関連でも同様の課題意識があり、「[Claude Code の CLAUDE.md に書くべきルール4選](https://zenn.dev/quon_agents/articles/claude-code-claude-md-rules)」では、実用的なルール項目とテンプレートが紹介されている。
- ツール横断でエージェント設定の標準化が模索される一方、設定の陳腐化やドリフトへの対策が次の焦点になっている。

## セキュリティリスクの表面化

- AI駆動開発の普及に伴い、生成コードやツール自体のセキュリティリスクが具体的な事例とともに指摘され始めている。
- 「[AI Coding Tool Security Risk for Engineering Leaders](https://dev.to/coppersundev/ai-coding-tool-security-risk-for-engineering-leaders-25mh)」では、エンジニアリング組織のリーダー層が把握すべきAIコーディングツール導入時のリスクが整理されている。
- より具体的な事例として「[Command Injection in AI-Generated Express.js: A Real Scan](https://dev.to/coppersundev/command-injection-in-ai-generated-expressjs-a-real-scan-4a54)」があり、AIが生成したExpress.jsコードを実際にスキャンした結果、コマンドインジェクションの脆弱性が発見されたことが報告されている。
- これらの記事は、AIが生成したコードをそのまま信頼せず、既存のセキュリティレビュープロセスに組み込む必要性を強調している。
- 開発速度の向上とセキュリティ担保の両立が、AI駆動開発における組織的な課題として顕在化しつつある。

## 実運用における運用知見の蓄積

- ツールの実運用に関する具体的なノウハウを共有する記事も多く見られ、現場レベルでの試行錯誤が進んでいる。
- 「[コーディングエージェント（Cursor / Claude Code）をクラウド版で動かしてみた（2026年8月版）](https://zenn.dev/satoshi_tech/articles/20260811-zenn-article-cloud-agents)」では、ローカル実行が主流だったコーディングエージェントをクラウド環境で動かす試みが報告されており、実行環境の選択肢が広がりつつあることがわかる。
- 「[Claude Codeのサブエージェントが自動で呼ばれなかったときの話](https://zenn.dev/hijio/articles/545aa114d7ebae)」は、サブエージェント機能を使う際に想定通り自動起動しないという実運用上のつまずきを共有しており、エージェント連携の設計にはまだ不安定さが残ることを示している。
- 複数組織で働くエンジニアの環境管理についても知見が出てきており、「[複数社で働くエンジニアのClaude Code環境分離](https://zenn.dev/shigerufukada/articles/d5d0ea2e7e6dec)」では、CLAUDE_CONFIG_DIRとdirenvを組み合わせてMCPサーバーの誤連携を防ぐ設計が紹介されている。
- コードレビューの分野でもAI活用が進んでおり、「[同じ差分を5つのLLMにレビューさせてみた](https://zenn.dev/ivyxon/articles/five-llms-same-code-review)」では、複数のLLMに同一の差分をレビューさせた結果、レビュー対象のバグよりも先に自分自身のコードミスが発見されたという興味深い知見が報告されている。
- これらの記事に共通するのは、AIエージェントの導入がもはや「使うかどうか」ではなく「どう安定運用するか」というフェーズに入っているという点であり、環境分離や挙動の検証など地道な運用改善が求められている。

## 出典

- [From coder to orchestrator: How agents shift the role of a developer](https://github.blog/developer-skills/career-growth/from-coder-to-orchestrator-how-agents-shift-the-role-of-a-developer/)
- [Vibe codingの本番化に必要なのは、プロンプトではなく「昇格マニフェスト」だ](https://zenn.dev/heftykoo/articles/5770d711add672)
- [AGENTS.md, explained for teams that actually ship](https://dev.to/arpituppal2rgb/agentsmd-explained-for-teams-that-actually-ship-13c3)
- [Generating your agent rules from one file does not stop them drifting](https://dev.to/untactit/generating-your-agent-rules-from-one-file-does-not-stop-them-drifting-3gpb)
- [Claude Code の CLAUDE.md に書くべきルール4選 ― 調整して使うテンプレート付き](https://zenn.dev/quon_agents/articles/claude-code-claude-md-rules)
- [AI Coding Tool Security Risk for Engineering Leaders](https://dev.to/coppersundev/ai-coding-tool-security-risk-for-engineering-leaders-25mh)
- [Command Injection in AI-Generated Express.js: A Real Scan](https://dev.to/coppersundev/command-injection-in-ai-generated-expressjs-a-real-scan-4a54)
- [コーディングエージェント（Cursor / Claude Code）をクラウド版で動かしてみた（2026年8月版）](https://zenn.dev/satoshi_tech/articles/20260811-zenn-article-cloud-agents)
- [Claude Codeのサブエージェントが自動で呼ばれなかったときの話](https://zenn.dev/hijio/articles/545aa114d7ebae)
- [複数社で働くエンジニアのClaude Code環境分離 — CLAUDE_CONFIG_DIR × direnvでMCPの誤連携を防ぐ](https://zenn.dev/shigerufukada/articles/d5d0ea2e7e6dec)
- [同じ差分を5つのLLMにレビューさせてみた——バグより先に見つかったのは自分のミスだった](https://zenn.dev/ivyxon/articles/five-llms-same-code-review)

# Git Commit message rules

- 先頭行は英語で記入する.
  - 後述の commit-prefix と ": " で始める.
  - Issueチケットに対応するコミットならば、続けて "#チケット番号 " を付ける.
  - 単一機能の修正コミットならば、続けて "機能名: " を付ける.
  - 単一ファイルの修正コミットならば、続けて "ファイル名: " を付ける.
  - 最後にコミットの要約を記入する.
- 一行空けて詳細コミットを日本語で記入する.
  - 不具合修正の場合: 先頭行の commit-prefix は "Fix: " とする. 詳細コミットには、[問題],[原因],[修正方針] の表題を付けて記入する.
  - 機能追加の場合: 先頭行の commit-prefix は "Feat: " とする. 詳細コミットには、[目的、理由],[機能概要] の表題を付けて記入する.
  - AIに与えたプロンプトがあれば、[AIプロンプト] の表題を付けてプロンプト概要を追記する. ただしコミット実行のプロンプトは除外する.
  - 詳細コミットは80から120桁で折り返す.

## commit-prefix

- Feat: A new feature
- Fix: A bug fix
- Docs: Documentation only changes. a code comment, user prompt, erorr message etc.
- Style: Changes that do not affect the meaning of the code
- Perf: A code change that improves performance
- Safety: A Code change that fool proof or security
- Refactor: A code change that neither "Feat", "Fix", "Pref" nor "Safety"
- Test: Test only changes. test codes and test datas.
- Debug: Changes to the debug staff
- Chore: Changes to the build, release or publish.

# Git Commit rules
- "do commit" のプロンプト指示を出すまでコミット実行するな.
- コミット実行前に、修正ソースの構文チェックをやれ.

# end

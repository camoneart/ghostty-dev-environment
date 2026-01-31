機能名: Ghosttyベース開発環境構築

- セッション名: recursive-beaming-blanket
- 日付: 2026-01-31 00:24:22
- 概要: Ghosttyをベースにした高速ターミナル開発環境の構築。ターミナル分割、ファイラー、Git TUI、高速検索ツールを導入。
- 実装内容:
  - zellij (v0.43.1) - ターミナル分割ツール
  - yazi (v26.1.22) - プレビュー付きファイラー + 依存関係
  - lazygit (v0.58.1) - Git TUI
  - fzf (v0.67.0) - ファジー検索
  - ripgrep (v15.1.0) - 高速grep
  - yaziオプション依存関係: ffmpeg, sevenzip, jq, poppler, fd, zoxide, imagemagick
- 設計意図:
  - Ghosttyの爆速起動を活かしつつ、モダンなCLIツールで開発効率を最大化
  - zellijを自動起動することで、常にペイン分割・タブ管理が使える状態に
  - yaziのプレビュー機能を最大限活かすため依存関係もフルインストール
  - fzf + ripgrepの連携で、隠しファイルも含めた高速検索を実現
  - zoxideでスマートなディレクトリ移動（z コマンド）を追加
- 副作用:
  - Ghostty起動時にzellijが自動起動するため、素のシェルを使いたい場合は設定変更が必要
  - .zshrcへの追記により、シェル起動時間がわずかに増加する可能性
- 関連ファイル:
  - ~/.config/zellij/config.kdl - zellij設定
  - ~/.config/yazi/ - yazi設定ディレクトリ
  - ~/.config/lazygit/ - lazygit設定ディレクトリ
  - ~/.config/ghostty/config - Ghostty設定
  - ~/.zshrc - シェル連携設定

---

## 計画内容

### インストール対象ツール

| ツール | 用途 | バージョン |
|--------|------|------------|
| zellij | ターミナル分割 | 0.43.1 |
| yazi | ファイラー | 26.1.22 |
| lazygit | Git TUI | 0.58.1 |
| fzf | ファジー検索 | 0.67.0 |
| ripgrep | 高速grep | 15.1.0 |

### 基本操作チートシート

#### zellij（ターミナル分割）
- `Ctrl+p` → ペインモード（分割操作）
- `Ctrl+t` → タブモード
- `Ctrl+n` → 新規ペイン
- `Ctrl+o` → セッションモード

#### yazi（ファイラー）
- `y` → yaziを起動（ディレクトリ移動連携付き）
- `j/k` → 上下移動
- `l` → ディレクトリに入る / ファイルを開く
- `h` → 親ディレクトリに戻る
- `q` → 終了

#### lazygit（Git TUI）
- `c` → コミット
- `p` → プッシュ
- `P` → プル
- `space` → ステージング切り替え
- `?` → ヘルプ

#### fzf + ripgrep（検索）
- `Ctrl+T` → ファイル検索
- `Ctrl+R` → コマンド履歴検索
- `Alt+C` → ディレクトリ移動

#### zoxide（ディレクトリ移動）
- `z <部分名>` → よく使うディレクトリに移動
- `zi` → インタラクティブ選択

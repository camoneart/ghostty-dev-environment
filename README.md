# Ghostty Dev Environment

Ghosttyをベースにした高速ターミナル開発環境

## 構成

```
┌─────────────────────────────────┬─────────────────┐
│            Neovim               │   Claude Code   │
│  ┌──────────┬────────────────┐  │                 │
│  │ neo-tree │    エディタ    │  ├─────────────────┤
│  │ (左)     │    (中央)      │  │   lazygit       │
│  └──────────┴────────────────┘  │                 │
└─────────────────────────────────┴─────────────────┘
```

## インストール済みツール

| ツール | 用途 | バージョン |
|--------|------|------------|
| [Ghostty](https://ghostty.org/) | ターミナル | - |
| [zellij](https://zellij.dev/) | 画面分割 | 0.43.1 |
| [Neovim](https://neovim.io/) + [LazyVim](https://www.lazyvim.org/) | エディタ | 0.11.6 |
| [yazi](https://yazi-rs.github.io/) | ファイラー | 26.1.22 |
| [lazygit](https://github.com/jesseduffield/lazygit) | Git TUI | 0.58.1 |
| [fzf](https://github.com/junegunn/fzf) | ファジー検索 | 0.67.0 |
| [ripgrep](https://github.com/BurntSushi/ripgrep) | 高速grep | 15.1.0 |
| [zoxide](https://github.com/ajeetdsouza/zoxide) | スマートcd | 0.9.8 |

## キーバインド早見表

### zellij（画面分割）

| キー | 動作 |
|------|------|
| `Ctrl+p` → `r` | 横に分割（左右） |
| `Ctrl+p` → `d` | 縦に分割（上下） |
| `Ctrl+p` → `x` | ペインを閉じる |
| `Ctrl+p` → `h/j/k/l` | ペイン間移動 |
| `Ctrl+t` | タブモード |

### Neovim (LazyVim)

| キー | 動作 |
|------|------|
| `Space` | リーダーキー（メニュー表示） |
| `Space + e` | ファイルツリー（neo-tree）トグル |
| `Space + f + f` | ファイル検索 |
| `Space + /` | 全文検索（grep） |
| `Space + b + d` | バッファを閉じる |
| `:q` | Neovim終了 |
| `:w` | 保存 |
| `:wq` | 保存して終了 |

### lazygit

| キー | 動作 |
|------|------|
| `space` | ステージング切り替え |
| `c` | コミット |
| `p` | プッシュ |
| `P` | プル |
| `?` | ヘルプ |
| `q` | 終了 |

### yazi（ファイラー）

| キー | 動作 |
|------|------|
| `y` | yazi起動（シェル連携） |
| `j/k` | 上下移動 |
| `l` | 開く/入る |
| `h` | 親ディレクトリ |
| `q` | 終了 |

### fzf（検索）

| キー | 動作 |
|------|------|
| `Ctrl+T` | ファイル検索 |
| `Ctrl+R` | コマンド履歴検索 |
| `Alt+C` | ディレクトリ移動 |

### zoxide

| キー | 動作 |
|------|------|
| `z <部分名>` | ディレクトリにジャンプ |
| `zi` | インタラクティブ選択 |

## 設定ファイルの場所

```
~/.config/
├── ghostty/config      # Ghostty設定
├── zellij/config.kdl   # zellij設定
├── nvim/               # Neovim/LazyVim設定
├── yazi/               # yazi設定
└── lazygit/            # lazygit設定

~/.zshrc                # シェル連携設定
```

## セットアップ手順

### 1. ツールのインストール

```bash
# 基本ツール
brew install zellij yazi lazygit fzf ripgrep neovim

# yaziの依存関係
brew install ffmpeg sevenzip jq poppler fd zoxide imagemagick
```

### 2. LazyVimの導入

```bash
git clone https://github.com/LazyVim/starter ~/.config/nvim
rm -rf ~/.config/nvim/.git
nvim  # 初回起動でプラグイン自動インストール
```

### 3. シェル連携（.zshrc）

```bash
# yazi - ディレクトリ移動連携
function y() {
  local tmp="$(mktemp -t "yazi-cwd.XXXXXX")" cwd
  yazi "$@" --cwd-file="$tmp"
  if cwd="$(command cat -- "$tmp")" && [ -n "$cwd" ] && [ "$cwd" != "$PWD" ]; then
    builtin cd -- "$cwd"
  fi
  rm -f -- "$tmp"
}

# fzf
source <(fzf --zsh)
export FZF_DEFAULT_COMMAND='rg --files --hidden --glob "!.git"'
export FZF_CTRL_T_COMMAND="$FZF_DEFAULT_COMMAND"

# zoxide
eval "$(zoxide init zsh)"
```

### 4. Ghostty設定

```
# ~/.config/ghostty/config
command = /opt/homebrew/bin/zellij
font-family = "JetBrainsMonoNL Nerd Font"
font-size = 14
```

## 作成日

2026-01-31

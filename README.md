# Ghostty + ターミナル中心の軽量開発環境

> VSCode の代わりに「ターミナルに寄せる」発想で構築した開発環境。

## なぜこの構成？

- **メモリ節約**: VSCode（Electron）を丸ごと排除できる
- **起動速度**: ターミナルベースなので一瞬で立ち上がる
- **カスタマイズ性**: 各ツールが独立しているので、好みに合わせて差し替え可能
- **合う人には合う**: CLI操作に抵抗がなく、キーボード中心で作業したい人向け

## ツール構成

| 役割 | ツール | ポイント |
|------|--------|----------|
| ターミナル | [Ghostty](https://ghostty.org/) | 起動が爆速、GPU描画で軽量 |
| 画面分割 | [zellij](https://zellij.dev/) | 設定が楽、tmuxより直感的 |
| ファイラー | [yazi](https://yazi-rs.github.io/) | プレビュー付き、Rust製で爆速 |
| Git操作 | [lazygit](https://github.com/jesseduffield/lazygit) | CLIなのにGUI並みの視認性 |
| 検索 | [fzf](https://github.com/junegunn/fzf) + [ripgrep](https://github.com/BurntSushi/ripgrep) | Cmd+Pより速いファジー検索 |
| AIコーディング | [Claude Code](https://claude.ai/claude-code) | ターミナルネイティブで相性抜群 |

## キーバインド早見表

### zellij（画面分割）

| キー | 動作 |
|------|------|
| `Ctrl+p` → `r` | 横に分割（左右） |
| `Ctrl+p` → `d` | 縦に分割（上下） |
| `Ctrl+p` → `x` | ペインを閉じる |
| `Ctrl+p` → `h/j/k/l` | ペイン間移動 |
| `Ctrl+t` | タブモード |

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

## セットアップ手順

### 1. ツールのインストール

```bash
# 基本ツール
brew install zellij yazi lazygit fzf ripgrep

# yaziの依存関係
brew install ffmpeg sevenzip jq poppler fd imagemagick
```

### 2. シェル連携（.zshrc）

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
```

### 3. Ghostty設定

```
# ~/.config/ghostty/config
command = /opt/homebrew/bin/zellij
font-family = "JetBrainsMonoNL Nerd Font"
font-size = 14
```

## 設定ファイルの場所

```
~/.config/
├── ghostty/config      # Ghostty設定
├── zellij/config.kdl   # zellij設定
├── yazi/               # yazi設定
└── lazygit/            # lazygit設定

~/.zshrc                # シェル連携設定
```

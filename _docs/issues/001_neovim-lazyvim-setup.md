# Issue #001: Neovim + LazyVim 導入

## 概要
Ghosttyベースの開発環境にNeovim（LazyVim）を導入し、ターミナル完結型のIDE環境を構築する。

## 背景
- Claude Code（AIコーディング）をCLIで使用するため、ターミナル操作に慣れたい
- 参考画像のような画面構成を実現したい（Neovim + Claude Code + lazygit）

## 目標画面構成
```
┌─────────────────────────────────┬─────────────────┐
│            Neovim               │   Claude Code   │
│  ┌──────────┬────────────────┐  │                 │
│  │ neo-tree │    エディタ    │  ├─────────────────┤
│  │ (左)     │    (中央)      │  │   lazygit       │
│  └──────────┴────────────────┘  │                 │
└─────────────────────────────────┴─────────────────┘
```

**ファイラー**: neo-tree（LazyVim内蔵）を使用

## タスク

### Phase 1: Neovim本体のインストール
- [ ] `brew install neovim` でNeovimをインストール
- [ ] `nvim --version` で動作確認

### Phase 2: LazyVimの導入
- [ ] 既存のNeovim設定をバックアップ（あれば）
- [ ] LazyVimのスターターテンプレートをクローン
- [ ] Neovimを起動してプラグインの自動インストールを確認
- [ ] 基本操作の確認（ファイルツリー、ファイル検索など）

### Phase 3: zellij レイアウト設定
- [ ] 目標画面構成のzellijレイアウトファイルを作成
- [ ] ワンコマンドで開発環境を起動できるようにする

### Phase 4: 動作確認・調整
- [ ] Neovim + Claude Code + lazygit の同時起動確認
- [ ] キーバインドの確認・カスタマイズ（必要に応じて）

## 参考リンク
- [Neovim公式](https://neovim.io/)
- [LazyVim公式](https://www.lazyvim.org/)
- [LazyVim GitHub](https://github.com/LazyVim/LazyVim)

## 関連
- 現在の環境: Ghostty + zellij + yazi + lazygit + fzf + ripgrep

---

作成日: 2026-01-31
ステータス: Open

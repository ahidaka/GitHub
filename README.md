# 自己流 超簡単 GitHub! これだけ使えばOK

**前提** というか **想定する環境または状況**
- コマンドだけで全て行うのでcdぐらいは知る必要あり。（コマンド恐怖症やGUI依存症は無視）
- git / git for Windows 以外の追加ツールのインストール無し。

	（環境が数十台もあるといちいち入れてられないから）

- bashとgitコマンドが使えるあらゆるLinux環境
- またはgitコマンドが使えるあらゆるWindows環境


### GitHubからのダウンロード（クローン）
基本中の基本だが一応初心者用に記す。

```sh
git clone something.git
```

### ローカルでのユーザー設定と確認

初回リポジトリ作成時、またはクローン後に必ず実行または確認。

#### ユーザー名やメールアドレスの設定
これをやっておかないと、後々面倒なことになる。

```sh
git config --local user.name ahidaka
git config --local user.email hidaka@devdrv.co.jp
git config --local --list
```


### GitHubへのアップロード（コミットとプッシュ）

リポジトリの操作が全て完了し、GitHubにアップロードする操作。最初からは、細かい用語を覚える必要は無い。


```sh
git add -A
git commit -a -m "Version 1.00 release"
git push
```

## 他のリポジトリを解析する

最新版だとビルドでエラーになる等使えない場合、以前のバージョンを探して自由に持って来れる。

```sh
git clone something.git
```

```sh
git clone something.git
```


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

これで **git clone** コマンドを実行したディレクトリ以下にクローン（複製）されたリポジトリが作成される。以降のコマンドは、全てその **複製された** ディレクトリに移動（**cd**）して実行する。

慣れると当たり前だが **git** の優れている点は、この複製でできたサブディレクトリは、いきなり直ぐに編集しても、丸ごとどこかにコピーしてそれを編集しても全く問題なく動作するという事である。
旧世代の**CVS**や**SVN**などの邪悪なツールに染まっていると違和感があるが、早く忘れて慣れるしかない。

### ローカルでのユーザー設定と確認

初回リポジトリ作成時、またはクローン後に必ず一度だけ実行または確認。

#### ユーザー名やメールアドレスの設定
これをやっておかないと、後々面倒なことになる。

```sh
git config --local user.name your-GitHub-User-Name
git config --local user.email your@email.address.for.github
git config --local --list
```


### GitHubへのアップロード（コミットとプッシュ）

リポジトリの操作が全て完了し、GitHubにアップロードする操作。最初からは、細かい用語やオプションを覚える必要は無い。

```sh
git add -A
git commit -a -m "Version 1.00 release"
git push
```

- **注意（git commit）**

	"～" には「その時何を修正したか」等、後で見てわかる様に、コミット時の気の利いたメッセージを入れる。**-a** は全ての変更に対してという意味。**-m** を付けないとローカル環境でのメッセージ入力用のテキストエディタが自動的に立ち上がり、 それはまた面倒なことになるので、お勧めしない。

- **注意（git push）**

	リポジトリ作った直後、設定を換えた後などで、"git push" コマンドでエラーが出る場合がある。その様場合には "-f" オプション付きで再度実行する。

```sh
git push -f
```

## 他のリポジトリを解析する

他人が管理するリポジトリでは、時々思った通りの内容が最新版として公開されてない場合がある。
当たり前の話だが、GitHub から 手元に "clone" した場合、指定した **branch** （デフォルトは　**master**）の過去の全ソースコードとその変更履歴が全て入っている。

例えば最新版だとビルドでエラーになる等使えない場合、以前のバージョンのコードを探して、任意の時点のコードを自由に取り出すことが可能である。
ベータ版や Preview 版などの開発途上のリポジトリを利用する場合、よく使う機能である。

親切なリポジトリでは、過去の主要な安定バージョンを **master** とは別の **branch** として保存してある場合がある。
その様場合、後述の **log機能** を使用して過去に遡らなくとも、ブランチ名を指定して **clone** すればよい。ブランチの一覧はリポジトリのページで確認できる。

- ブランチ一覧を表示（リポジトリの **Branch** ページを見た方が使い易い）

```sh
git branch -a
```

- ブランチを指定した **clone**

```sh
git clone -b (BRANCH-NAME)
```

更新（Commit）の履歴は、ブランチ一覧を表示（リポジトリの **History** ページで参照することが可能である。しかし手元で操作して直ぐに使いたい場合には、次の様に **git log** コマンドで日付と commit 番号を参照できる。 

- ログ（更新履歴）一覧を表示

```sh
git log
```

- 指定 commit を取得（checkout）

```sh
git checkout (COMMIT-NUMBER)
```

- 例

例えば **azure-iot-sdk-c** リポジトリの場合、**git log** の結果は次の通りである。

```sh
commit 354cd4297897008f203132f78ff573d31739a5a2
Merge: a263bbedf 0d9f5c6fd
Author: ewertons <ewertons@microsoft.com>
Date:   Thu Jun 18 15:39:55 2020 -0700

    Merge pull request #1565 from Azure/ewertons/gh1557

    Fix for memory leak if destroying device client right after sending Twin reported property update

commit 0d9f5c6fd864ec04f6acb6d4fd6c54f65a6a78cc
Author: Ewerton Scaboro da Silva <ewertons@microsoft.com>
Date:   Thu Jun 18 14:00:39 2020 -0700

    Fix for memory leak if destroying device client right after sending Twin reported property update

    The issue has been reported on github through https://github.com/Azure/azure-iot-sdk-c/issues/1557

commit a263bbedf508e610d10965001051bd713859261b
Author: Eric Wolz <ericwol@microsoft.com>
Date:   Mon Jun 15 11:15:56 2020 -0700

    Update setting_up_vcpkg.md (#1559)

以下省略
```

ここで、**commit** 文字の後の長い16進数が **commit 番号** である。従って "Jun 15 11:15:56 2020" にcommit したコードを入手するためには次の通り入力する。

```sh
git checkout a263bbedf508e610d10965001051bd713859261b
```


以上。

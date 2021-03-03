# セクション5: ブランチとマージ
## 38.ブランチの作成と名前変更と削除
- 特定の機能を開発したり、テスト用にブランチを切ることが多い。  
- ブランチはコミットを指すただのポインタ
- `$ git branch -a`でリモートリポを含むローカルリポに存在する全てのブランチを表示する
- `$ git checkout <branchname>`ブランチの切り替え
- `$ git branch <branchname>`ブランチの作成
- `$ git branch -m <old> <new>` ブランチ名の変更
- `$ git branch -d` ブランチを削除
- ハイフンで区切る
- add-hogeなどが良い
- test, fix-bug, featureなどはよくない例

## 39.ブランチをマージする
- mainブランチのようにチームで共有するブランチにマージする場合は、リモートリポジトリでマージする。Pull Requestを出す。
- それ以外の場合、自分で切ったブランチにさらにブランチをきり、それをマージする場合。
- `$ git merge <branchname>`
- マージする前に差分を確認するとよい
- `$ git diff <base> <compare>`
#### 注意点
`git merge`するときなbaseとするマージに、checkoutしてから行う！！！

## 40.automatic mergeをする
- Fast forwardマージ
- Fast forwardではないケースとは、マージ先に別のコミットがあるケース
- 各コミットが同じ部分を変更しているとうまくマージできない。Conflictが起きる。
- 各コミットが別の部分を変更していればマージできる。automatic mergeする。
- automatic mergeを体験してみよう。
- `$ git log --all --oneline`で、他のブランチのコミットも表示される。
- `$ git log --all --oneline --graph`で、少し視覚的になる。

## 45.リモートリポからローカルリポに情報をfetchする
- pull = fetch + merge
- `$ git fetch <remote_ref>`
- ローカルリポジトリの中にリモートリポジトリのブランチがある。
- 'git branch -a'で↑を確認できる
- ローカルリポ内のリモートリポの情報は古くなる。
- `$ git fetch `コマンドで↑の情報を更新できる。
- `$ git checkout remotes/origin/main`でローカルリポ内のリモートリポのmainに移動できる。

## 47.リモートリポからローカルリポにpullする
- `$ git pull <remote_ref> <branchname>`
- 指定したリモートリポ:remote_refの、指定したブランチ:branchnameを「今いるブランチ」にマージする
- 基本、pushするまえにpullする。ビハインドなブランチをpushすることはできない。エラーが起きる。

## 48.pull時のコンフリクトに対処する
- 業務ではmainブランチ上で作業を行わない。ブランチを切る。
- 定期的にリモートリポのmainブランチからpullすることで、後々mainブランチにマージしやすくなる。
1. github上でreadmeを変更
2. featureブランチでreadmeを変更
3. git pull origin mainするとコンフリクトが発生→指定したリモートリポ=origin, 指定したブランチ=main(リモートリポ上), マージ先=conflict_remote
4. readmeを修正し、git addし、git commitする

## 49.プルリクエストを作成する
- `git push origin conflict-remote`これによって、リモートリポジトリにconflict-remoteブランチが出来る。
- ブラウザで↑を確認。
- Compare & pull requestボタンをクリック
- デフォルトはフォークもとへのプルリクエストになっているので、注意
- commentを残す。レビューお願いします。
- create pull requestボタンをクリック
- 原則、リクエストに対するマージは他の人が行う。
- Files changedタブで変更内容を確認する。コードの横の+ボタンでコメントが書ける。
- review changesボタンをクリック.submit
- Conversationタブをクリックして、Merge pull requestボタンをクリック。必要に応じてコメントを書いて、confirm mergeボタンをクリック。
- ローカルリポのmainブランチにプルする。（やり方は割愛）

## 50.fork元のリポをローカルリポに登録する
- ローカルリポにfork元のリポ情報をセットする
  - `$ git remote add upstream <repo_url>`
- 以下、ブラウザの操作
  - 画面右上のD-S-Hub/git-practiceをクリック
  - Codeボタンからhttpsもしくはsshをクリップボードにコピー
- `$ git remote add upstream git@github.com:D-S-Hub/git-practice.git`

## 51.fork元のリポにPRを作成する
- 今回pullするが、pull先はfork元。
  - `$ git pull upstream main`
- ローカルリポからforkもとにプッシュしない。一旦自分のリモートリポへプッシュ。
  - `$ git push origin new-feature`
- fork元のリポジトリにプルリクエストを出す
  - Compare & pull requestボタンをクリック
  - base repositoryをfork元のリポジトリにする！
  - コメントはきちんと書く。
  
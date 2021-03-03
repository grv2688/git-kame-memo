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
<br>
<br>
## 39.ブランチをマージする
- mainブランチのようにチームで共有するブランチにマージする場合は、リモートリポジトリでマージする。Pull Requestを出す。
- それ以外の場合、自分で切ったブランチにさらにブランチをきり、それをマージする場合。
- `$ git merge <branchname>`
- マージする前に差分を確認するとよい
- `$ git diff <base> <compare>`
#### 注意点
`git merge`するときなbaseとするマージに、checkoutしてから行う！！！
<br>
<br>
## 40.automatic mergeをする
- Fast forwardマージ
- Fast forwardではないケースとは、マージ先に別のコミットがあるケース
- 各コミットが同じ部分を変更しているとうまくマージできない。Conflictが起きる。
- 各コミットが別の部分を変更していればマージできる。automatic mergeする。
- automatic mergeを体験してみよう。
- `$ git log --all --oneline`で、他のブランチのコミットも表示される。
- `$ git log --all --oneline --graph`で、少し視覚的になる。
<br>
<br>
## 45.リモートリポからローカルリポに情報をfetchする
- pull = fetch + merge
- `$ git fetch <remote_ref>`
- ローカルリポジトリの中にリモートリポジトリのブランチがある。
- 'git branch -a'で↑を確認できる
- ローカルリポ内のリモートリポの情報は古くなる。
- `$ git fetch `コマンドで↑の情報を更新できる。
- `$ git checkout remotes/origin/main`でローカルリポ内のリモートリポのmainに移動できる。
<br>
<br>
## 46.リモートリポからローカルリポにpullする
- `$ git pull <remote_ref> <branchname>`
- 指定したリモートリポ:remote_refの、指定したブランチ:branchnameを「今いるブランチ」にマージする
- 基本、pushするまえにpullする。ビハインドなブランチをpushすることはできない。エラーが起きる。
<br>
<br>



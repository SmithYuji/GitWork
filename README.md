# GitWork

## キーワード
### ◆SSHキー
+ リポジトリにアクセスするための、SSHを利用した公開鍵と秘密鍵のこと
### ◆リポジトリ
+ 情報が保存されているデータベースのこと
+ ファイルやディレクトリの状態を記録する場所
### ◆ローカルリポジトリ
+ リモートリポジトリに送るためのコミットを記録する場所
### ◆リモートリポジトリ
+ 複数人で共有するためのリポジトリ
### ◆コミット
+ ワーキングツリーにある管理対象の全てのファイルのその時点の状態を記録する
###　◆ワークツリー(もしくは、ワーキングツリー)
+ .gitディレクトリが追加されてGitの管理下に置かれたディレクトリのこと
### ◆ステージ領域(もしくはインデックス)
+ リポジトリにコミットをする前の一時領域
+ git addコマンドでファイルをここに登録して、git commitでここに登録されているファイルをリポジトリにコミットする
### ◆ブランチ
+ 作業の流れを分岐して記録していくためのもの
+ 分岐したブランチは他のブランチの影響を受けない
+ 別々の作業を並行して行うために利用する
### ◆統合ブランチ
+ リリース版がいつでも作成可能な要しておくためのブランチ
+ トピックブランチの分岐点であり、そのため、安定した状態を保っておくことが重要
### ◆トピックブランチ
+ 一つのトピック(テーマ)に集中して、他の作業は一切行わないブランチのこと
+ トピックブランチのトピックとされるものは、機能追加やバグ修正といった課題となる
+ 課題の数だけトピックブランチを作る
+ 作業が完了したら統合ブランチに取り込む
### ◆マージ
+ ブランチにトピックブランチを取り込むこと
+ マージする際には、ブランチは統合ブランチにしておく
### ◆fast-forward
+ コミットAとコミットBがあるとき、コミットAの歴史がコミットBの歴史に全て含まれて入る場合、fast-forwardである。
### ◆マージコミット
+ マージした際に生じた変更を取り込んだコミット
+ マージ先ブランチ(統合ブランチ)の先頭はマージコミットになる
### ◆HEAD
+ 現在使用しているブランチの先頭を表す名前
### ◆コンフリクト
+ マージをした時にブランチの変更部分で衝突が起きたこと(同じ場所で別の変更を行う)

### ◆ガベージコレクション
+ プログラムが動的に確保したメモリ領域のうち、不要になった領域を自動的に解放する機能

## 基本的な操作
### ◆git init
+ リポジトリの初期化
+ フォルダに.gitフォルダを追加し、追加されたフォルダ以下をワークツリーと呼ぶ
### ◆git status
+ リポジトリの状態を確認
### ◆git add
+ ワーキングツリーにあるファイルをステージ領域に登録してGitの管理対象にする
    ### . オプション
     + git管理下のファイル全部をステージ領域に登録する
    ### --allオプション
     + 変更が加えられたファイルと未追跡だった(新しく作った等)だったファイルをステージ領域に追加
### ◆git commit
+ リポジトリの歴史を記録
+ ステージ領域に登録されている時点のファイル群を実際にリポジトリの歴史として記録する
+ 記録した歴史を元に、ファイルをワーキングツリーに復元したりできる
    ### -mオプション
     + コミットに関する要約を書く
     + -mオプションをつけないでそのままコミットすると、エディタが立ち上がり、コミットに関する詳細なメッセージが書ける
    ### --amendオプション
     + 直前のコミットメッセージを修正する
### ◆git push
+ 現在のローカルリポジトリの内容をリモートリポジトリに送信する
    ### -f | --foure
     + 強制的にプッシュする
    ### git push [ローカルブランチ名]
     + 指定のローカルブランチを同名のリモートブランチにpushする
     + git push master は git push master : master の省略
    ### git push [ローカルブランチ名] : [リモートブランチ名]
     + 指定のローカルブランチを指定のリモートブランチにpushする

### ◆git log
+ 『現在の状態の過去』を確認できる
+ 誰が、いつ、どのような差分が発生するコミットやマージをしたかが確認できる
<img width="347" alt="2017-05-24 13 25 01" src="https://cloud.githubusercontent.com/assets/7357884/26386945/e20d784e-4084-11e7-930d-2c44cab917ff.png">

   ### ログの見方
 + 上記画像の黄色い部分、「commit ....」に続く文字列がハッシュ値。Gitの他のコマンドでこのコミットを指し示す際に利用する。
 + Author　ではGitで設定されているユーザ名とメールアドレスが記録されている
 + Dateにはコミットを実施した日時が記録されている
   ### --pretty=shorオプション
 + コミットメッセージの一行目のみを表示する
   ### git log [ファイル名]
 + 指定したディレクトリ、ファイルのみのログを表示する
   ### -pオプション
 + ファイルの差分を表示する
   ### git log --graph
 + ブランチを視覚的に確認する

### ◆git reflog
+ リポジトリにコミットされたログを確認できる
+ Gitのガベージコレクションが行われない限り、このコマンドである程度の過去と未来を行き来できる

### git diff
+ ワークツリー、ステージ領域、最新コミット間の差分を確認する
+ ステージ領域に追加していない場合は、最新コミットとの差分として表示
    ### git diff HEAD
    + ワークツリーと最新コミットの差分を確認する
### git branch
+ ローカルリポジトリのブランチを一覧表示
+ 表示されたブランチ名の中で、「\*名前」となっているブランチが現在のブランチ
### git checkout -b
+ 新しいブランチを作成し、切り替える
### git checkout -
+ 前回のブランチに切り替える
### git merge --no-ff [統合ブランチにマージするトピックブランチ名]
+ 現在のブランチ(統合ブランチが推奨)に指定の名前のブランチをマージ(取り込む)すること
    ### --ffオプション
     + マージ対象のブランチとfast-forwardの関係にある場合、マージコミットは作られず、ブランチの参照先の更新だけを行う
     + fast-forwardの関係にない場合はマージコミットが作られる
    ### --no-ffオプション
     + fast-forwardの関係であっても、必ずマージコミットを作る
    ### --squashオプション
     + ワークツリーとインデックスの状態はマージ後の状態になるが、マージコミットは作らない

### git reset
+ HEADの位置を変更する
+ オプションによってインデックス、ワーキングツリーの内容も変更できる
    ### --hard [戻りたいコミットのハッシュ値]
     + HEADの位置とインデックス、ワーキングツリーを変更して完全に復元する
    ### --soft [ハッシュ値]
     + HEAD の位置のみを変更する
    ### --mixied [ハッシュ値]
     + HEADの位置とインデックスを変更する
### git rebase -i HEAD~[HEADから修正するコミットまでの数]
+ すでにコミットした内容にちょっとしたスペルミスなどが発見されたら修正のコミットをし、そのコミットを正しく実装したコミットに含めて歴史そのものを押しつぶして改変する
```
    #  p, pick = use commit
    #  r, reword = use commit, but edit the commit message
    #  e, edit = use commit, but stop for amending
    #  s, squash = use commit, but meld into previous commit
    #  f, fixup = like "squash", but discard this commit's log message
    #  x, exec = run command (the rest of the line) using shell
```

演習5 GitHubでのプルリクエストとコンフリクトの解消
========================================================

コンフリクトは、GitHubでブランチをマージする際にも起こりえます。それをGitHub上で解決します。

今回の演習では、「他の人」「マージ担当」の作業も自分で行います（1人3役）。

この演習が成功した後、sample.txtは次のようになっています。

```
おはよう
おやすみなさい
再びおはよう
```

この演習内のコマンドはすべて、クローンしたgit-exercisesフォルダで実行してください。

# 1. 他の人（実は自分）の作業
(1) https://github.com/自分のアカウント名/git-exercises にアクセスしてください。

(2) ブラウザでsample.txtを開いた後、画面右上にある[Edit this file]ボタン（ペンのアイコン）をクリックしてください。

(3) 最後の行に「再びおはよう」を追記してください。

作業完了後のsample.txtは次のようになっています。

```
おはよう
再びおはよう
```

(4) 画面下の[Commit message]に「sample.txtに「再びおはよう」を追加」と記入後、[Commit changes]をクリックしてください。

# 2. 自分の作業 - ブランチの作成
(1) 次のコマンドでローカルリポジトリにブランチを作成してください。

```bash
$ git branch add-gn
$ git switch add-gn
```

(2) 次のコマンドで現在のブランチが `add-gn` であることを確認してください。

(3) エディタでsample.txtを開いた後、最後の行に「おやすみなさい」を追記・保存してください。

作業完了後のsample.txtは次のようになっています。

```
おはよう
おやすみなさい
```

(4) 次のコマンドでステージングとコミットを行ってください。

```bash
$ git add sample.txt
$ git commit -m "sample.txtに「おやすみなさい」を追加"
```

(5) 次のコマンドでプッシュおよびリモートブランチの作成を行ってください。

```bash
$ git push origin add-gn
```

(6) 次のコマンドで、まだ現在のブランチが `add-gn` であることを確認してください。

```bash
$ git branch
```

# 3. 自分の作業 - プルリクエストの作成
(1) ブラウザで https://github.com/自分のアカウント名/git-exercises にアクセスしてください。

(2) 画面上側のメニューにある[Pull requests]をクリックしてください。

> 画面上側に[Compare & pull request]という緑色のボタンがある場合は、これをクリックしてください。この場合は(3)と(4)の手順は飛ばされます。

(3) [New pull request]をクリックしてください。

(4) [base]で「main」、[compare]で「add-gn」を選択すると、マージできない旨が表示されます。これは、競合が起きていることを示します。この状態でもプルリクエストを作成することは可能ですので、[Create pull request]をクリックしてください。

(5) [Open a pull request]画面で、各項目に次のように記入してください。

- [Title]に「「おやすみなさい」機能の追加」
- [Leave a comment]に「sample.txtに「おやすみなさい」を追加」

記入できたら[Create pull request]をクリックしてください。

# 4. マージ担当（実は自分）の作業 - コンフリクトの解消とマージ
(1) ブラウザで表示されたプルリクエスト[「おやすみなさい」機能の追加]の画面で、[Resolve conflicts]をクリックしてください。

(2) sample.txtをブラウザ上で編集できるようになりますので、次のように編集してください。

```
おはよう
おやすみなさい
再びおはよう
```

(3) [Mark as resolved]をクリック→[Commit merge]をクリックしてください。これにより `add-gn` ブランチのsample.txtが、編集した内容に変更されます。

(4) [Merge pull request]をクリック→[Confirm merge]をクリックしてください。これで `main` ブランチへマージが完了しました。

(5) 少し待って画面上部に[Merged]と表示された後、[Delete branch]をクリックしてください。これによりリモートリポジトリから `add-gn` ブランチが削除されます。

# 5. 自分の作業 - ローカルリポジトリへの反映
(1) 次のコマンドで `main` ブランチに移動してください。

```bash
$ git switch main
```

(2) 次のコマンドで現在のブランチが `main` であることを確認してください。

```bash
$ git branch
```

(3) 次のコマンドで、リモートリポジトリの `main` ブランチの最新状態を、ローカルリポジトリの `main` ブランチに反映してください。

```bash
$ git fetch
$ git merge origin/main
```

(4) エディタでsample.txtの内容を確認してください。次のようになっているはずです。

```
おはよう
おやすみなさい
再びおはよう
```

(5) 次のコマンドで、ローカルリポジトリの `add-gn` ブランチを削除してください。

```bash
$ git branch -D add-gn
```

(6) 次のコマンドで、ブランチが `main` のみになっていることを確認してください。

```bash
$ git branch
```
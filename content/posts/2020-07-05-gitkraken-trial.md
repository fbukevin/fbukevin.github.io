+++
date = '2020-07-05T08:45:05+08:00'
draft = false
title = 'Gitkraken Trial'
+++

已經免費用了這個 GitKraken 幾年了，中途也不時有在尋找其他較符合我使用習慣的 Git GUI 工具，最後實在還是最習慣用 GitKraken，所以後來就買了 Pro Plan，以下介紹幾個我覺得它方便的地方。

1. Commit stash
我們有時候開發一個 branch 到一半，可能會突然需要切換到另一個 brach 查看一些做法，或開發的內容，此時我們通常會需要先對還沒 commit 的修改作 stash，對應的 Git 指令是：`git stash file1 file2 ...`，這在 GitKraken 可以很直觀的操作。

只要先點選為修改的那個 pre-commit (HEAD)，然後點選右鍵，就可以找到 stash file 的項目，之後切回來只要在點選那個 pre-commit 後按右鍵，選擇 pop stash 即可。
![](/images/screenshot_20250310084552.png)

2. Rebase branch
每次在不是主要的 branch (e.g. main, master, develop) 作開發前，比較安全可以避免衝突發生的習慣是，開發之前都應該更新目前的 branch 跟上最新的分岔分支，例如你是從 develop 切出一個分支，那你需要更新你的 branch 分點到最新的 develop，此時會用到的 Git 指令就是：`git rebase base_branch new_base_branch`，這個可以在 GitKraken 這樣操作：
![](/images/screenshot_20250310085040.png)

3. Reset/Revert
有時候你開發到一半，覺得邏輯亂掉，或是想到新的方法，但要修改的地方太多，你可能不想再開新的分支(可能會導致分支過散過亂而難以整合)，假設你已經確定目前的修改不要，或是只是小段的變動，但是你已經 commit 了，此時我們通常會使用 `reset` 或 `revert` 這兩個操作，而 Git 中有 reset `--soft` 和 `--hard` 兩個主要的選項，前者會回到上一個 commit 的狀態，但是保留你剛剛那個 commit (或是多個新 commits)的修改內容，你只需要重新修改那些變更就行了，反之 `--hard` 則會直接摒棄掉所有新 commits 的變更，完全乾淨地回到你要退回的那個 commit，在 GitKraken 中，你可以這樣做：
![](/images/screenshot_20250310084627.png)

雖然像是 Sourcetree, GitHub Desktop, Visual Studio Code 的 Git extension 都可以做到相同的事，但整體使用上來說，我還是最喜歡 GitKraken 的體驗。

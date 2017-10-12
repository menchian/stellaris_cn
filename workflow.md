鑒於不少同學對 github 上的合作方法不清楚，我列出我自己的工作流。需要使用 git 命令行。github desktop 等圖形工具怎樣使用請懂的同學補充。


協作工作流
==========

1. 去 github 頁面上點 fork 創建一個自己 (假設你的用戶名叫 username) 的分支倉庫用於修改。

2. 在本地 clone 你的倉庫：
```
git clone git@github.com:username/stellaris_cn.git
```

3. 加一個本地分支跟蹤原始倉庫：
```
git remote add cloudwu https://github.com/cloudwu/stellaris_cn.git	# 添加遠程倉庫
git fetch cloudwu	# 將遠程倉庫取到本地
git checkout -b cloudwu cloudwu/master	# 創建一個本地分支跟蹤遠程倉庫
```

4. 在自己的倉庫修改提交
```
git checkout master	# 切換到自己的分支
...
git commit 
git push
```

5. 同步上游倉庫
```
git checkout cloudwu	# 切換到上游跟蹤分支
git pull	# 拉取上游倉庫
git checkout master	# 切換到自己的分支
git rebase cloudwu	# 和上游倉庫合併, 注意 rebase 之後可能需要 push -f
```

6. 合併上游倉庫（可選）

如果你確定自己的倉庫和上游原始倉庫內容完全相同，只是因為合併提交等原因有差異。
為了減少 rebase 過程中的衝突，可以在每次基於上游版本做翻譯前（確定你之前的 pr 已經被合併，或已放在獨立分支）使用：
```
git checkout cloudwu
git pull
git checkout master
git reset cloudwu
git push -f
```
這樣可以直接和原始倉庫分支保持嚴格一致。但注意，這樣會丟失你的本地提交。如果誤操作，可以通過 git reflog 查詢歷史版本，再 git reset 恢復。


----

在第四步驟做修改時，可以隨時進行第五步同步上游。第五步最後的 rebase 階段，如果發生衝突，git 會有提示，手工解決衝突後可回到第四步繼續。



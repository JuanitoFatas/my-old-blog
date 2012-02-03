---
layout: post
title: "Android 原始碼下載及版本控制 - 使用git與repo"
date: 2011-11-08 10:39
comments: true
categories: Android
tags: Android
---

要取得Android的原始碼，會需要用到*Git*和*Repo*還有*Gerrit*。
以下解釋一些工具，太冗長，可直接拉到最下方看如何取得Android原始碼。

###什麼是[Git][1]?

[1]: http://en.wikipedia.org/wiki/Git_(software)

> Git is an open-source version-control system designed to handle 
> very large projects that are distributed over multiple repositories. 

<!--more-->

###那Git for Android是?

> In the context of Android, we use Git for local operations such as 
> local branching, commits, diffs, and edits. One of the challenges 
> in setting up the Android project was figuring out how to best support 
> the outside community--from the hobbiest community to large OEMs 
> building mass-market consumer devices. We wanted components to be 
> replaceable, and we wanted interesting components to be able to grow a 
> life of their own outside of Android. We first chose a distributed 
> revision control system, then further narrowed it down to Git.

###什麼是[Repo][2]?

[2]: http://en.wikipedia.org/wiki/Repo_(script)

> Repo is a tool that Google built on top of Git 
> to manage the many Git repositories, do the uploads 
> to revision control system, and automate parts of the 
> Android development workflow.
> - from wikipedia

###什麼是Gerrit?

> Gerrit is a web-based code review system for projects that use git. 
> Gerrit encourages more centralized use of Git by allowing all authorized 
> users to submit changes, which are automatically merged if they pass code 
> review. In addition, Gerrit makes reviewing easier by displaying changes 
> side by side in-browser and enabling inline comments.

####我覺得簡單來說就是：


+ Git 是玩遊戲存檔的複雜工具
+ Git for Android 是玩Android遊戲存檔的複雜工具
+ Repo 是Google推出的遊戲存檔工具
+ Gerrit 給使用git專案的雲端code review伺服器


###安裝Git

請至[Git官網][3]下載適合版本。

[3]: http://git-scm.com/


###安裝repo ( Mac OSX 為例 )

首先在HOME目錄建立bin資料夾（如果沒有）

`$ mkdir ~/bin`

將此資料夾加入環境變數 $PATH

`$ PATH=~/bin:$PATH`

下載repo至~/bin/並設置權限為可執行

`$ curl https://dl-ssl.google.com/dl/googlesource/git-repo/repo > ~/bin/repo`
`$ chmod a+x ~/bin/repo`


##基本的工作流程


<img src="http://source.android.com/images/submit-patches-0.png" style="float:right"> 
<p><ol>
<li>用repo開始一個新的分支</li>
<li>編輯檔案</li>
<li>用git加入Stage changes</li>
<li>用git commit來commit變更</li>
<li>用repo upload來上傳變更至review server</li>
</ol></p>
</img>


##基本的工作項目：


###同步clinet端


同步所有現有的專案：

`$ repo sync`

同步被選擇的的專案

`$ repo sync project0 project1 ... projectN


###建立topic branches


開始一個新分支

`$ repo start BRANCH_NAME`

確認是否建立成功

`$ repo status`

使用topic branches

`$ repo start BRANCH_NAME PROJECT`

切換分支

`$ git checkout BRANCH_NAME`

分支列表

`$ git branch` 或是 `$ repo branches`

當下的分支前面有個*號

注意：
有一個bug會使 `repo sync` 重置到local topic branch。
如果在你運行 `repo sync` 之後 `git branch` 顯示 *(no branch)
再運行一次 `git checkout` 即可。


###Staging files


添加檔案到stage

`$ git add ARGUMENTS`

ARGUMENTS可以是檔案、資料夾...etc。


###檢視Client的狀態


列出檔案狀態的清單

`$ repo status`

看還沒commit的編輯

`$ repo diff`


####git diff與repo diff的差別?


`repo diff` 顯示本機的編輯（ 不會 列入commit）
`git diff` 顯示本機的編輯（ 會 列入commit）

在執行`git diff`之前，確定你是在專案的目錄底下：

`$ cd ~/WORKING_DIRECTORY/PROJECT`    
`$ git diff --cached`


###提交變更


提交

`$ git commit`

要輸入commit message否則會提交失敗

###上傳變更到Gerrit

在上傳之前，先更新到最新版本。

`$ repo sync`

之後執行

`$ repo upload`

會問你要選擇哪個分支到 review server


###修復Sync衝突


如果 `repo sync` 顯示 sync conflicts:

+ 檢視還沒merged的檔案 (status code = U)
+ 去修改編輯有衝突的地方

+ 變更相關的專案目錄

`$ git add .`    
`$ git commit`    
`$ git rebase --continue`    

+ 當rebase完成後開始sync

`$ repo sync PROJECT0 PROJECT1 ... PROJECTN`


###清理client檔案


變動之後更新本機工作目錄

`$ repo sync`

安全移除舊的topic branches

`$ repo prune`

刪除一個client

`$ rm -rf WORKING_DIRECTORY`

注意：會永久刪除所有你還沒有上傳的變更


#Git & Repo Cheatsheet    

<img src="http://source.android.com/images/git-repo-1.png" style="float:center">


##那究竟怎麼取得 Android 原始碼呢？

###首先建立一個 *Repo Client* 

建立要放置Android 原始碼的資料夾並切換至此資料夾

`$ mkdir WORKING_DIRECTORY`    
`$ cd WORKING_DIRECTORY`       

初始化repo 

`$ repo init -u https://android.googlesource.com/platform/manifest`

要使用Gerrit code-review工具，需要輸入與google連結之email、名字。


取得特定Android branch

`$ repo init -u https://android.googlesource.com/platform/manifest -b android-2.3.7_r1`


###取得檔案

`$ repo sync`

記得要在剛剛的 WORKING_DIRECTORY

###輸入Android原始碼的公用金鑰

####會使用到[gpg][4] --import sample_name.gpg

[4]: http://www.gnupg.org/gph/en/manual.html#AEN84

打開記事本輸入以下內容並另存為 xxx.gpg

{% gist 1347589 %}

把此金鑰加入到gpg key database裡

` gpg --import sample_name.gpg `

加入金鑰後可以用來確認git的tag

`$ git tag -v TAG_NAME`
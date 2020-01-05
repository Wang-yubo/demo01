### 1. git status

> git记录的当前文件状态

### 2. git add name

> - 将工作区的文件提交到暂存区
> - git add 记录的是变化，**即使是删除文件也需要git add**
> - 从工作区提交到暂存区的会文件变大==>会记录一些文件的变化
> - git add 后面一般跟上需要提交的文件的名字

##### 2.1 git add name name 

> 在第一个提交文件的名字后面可以跟上再想要提交的文件名，一起提交

##### 2.2 git add .

> - 提交新文件(new)和被修改(modified)文件，不包括被删除(deleted)文件 
> - 注意add后面空格再加点

##### 2.3 git add -u

>  提交被修改(modified)和被删除(deleted)文件，不包括新文件(new)

##### 2.4 git add -A

> git add -A  提交所有变化（git add --all的缩写）

##### 2.5  git restore --staged name

> 将提交到暂缓区的文件清除==>挪出暂存区，但是工作区会**保存修改**

##### 2.6 git checkout -- name

> - 将提交到暂存区的文件撤销修改==>挪出暂存区并且撤销修改，回到**未修改**的状态
> - 如果是未git add 的文件使用git checkout 就回到上个版本库中的版本
> - checkout后面一定要加 --  否则成了切换分支

### 3. git commit -m " "

> - 将暂存区的文件提交到版本库
> - -m "备注信息" ==> 双引号里面写本次提交的备注信息，最好写上修改了什么。一定一定一定要详细。

### 4. 设置提交者信息

![](F:\前端开发\git和GitHub学习\images\提交者信息.png)

> 提交的时候看到git系统提示我们需要告诉它自己的身份，通过git config指令设置用户邮箱和用户名

##### 4.1 解决办法

> ![](F:\前端开发\git和GitHub学习\images\设置提交者信息.png)
>
> 复制粘贴选中的两行命令，在双引号中修改成自己的信息，然后再次提交git
>
> 注意：复制一行修改一行提交一行，一个信息一个信息的提交，不要两个一起复制修改。
>
> 修改后的效果图![](F:\前端开发\git和GitHub学习\images\afterSet.png)
>
> master 3f0c513 ==>主分支
>
> 100644 ==>普通文件

### 5. git diff

> 比较不同，一般是比较同一个文件不同版本之间的不同。也可以用于比较两个完全没有关联的文件，并显示出他们的差别。**一定要把这个文件提交到git系统之后再修改才能比较。**

##### ![](F:\前端开发\git和GitHub学习\images\不同.png)

##### 5.1 标记 a/b

> ​	比较a文件和b文件之间的差别，为了区分他们，a和b都被赋予了特别的符号：
>
> - 版本a（原版本）的符号 --- 标记为（“ - ”）   
> - 版本b的符号（新版本） +++ 标记为（“ + ”）

##### 5.2 元数据 

> index e627b2b..8b9f8dc 100644
>
> - e627b2b ==>a文件id
> - 8b9f8dc  ==>b文件id
> - 100644==>普通文件
> - 100755可执行文件
> - 120000仅仅是一符号链接

##### 5.3区块头 

> @@ -1,2 +1,3 @@
>
> - -1,2表示a文件从第一行开始后面的两行
> - +1,3表示b文件从第一行开始后面的三行

### 6. git log

> 打印日志

![](F:\前端开发\git和GitHub学习\images\log.png)

##### 6.1 git log --pretty=oneline

> 打印一行，只打印id和备注

![](F:\前端开发\git和GitHub学习\images\oneline.png)

##### 6.2 git reflog

> 记录你所有的版本id

![](F:\前端开发\git和GitHub学习\images\reflog.png)

### 7. git reset

> - 版本回滚
> - 版本回滚甚至会将目标版本当时暂存区的状态也保留

##### 7.1 git reset id

> git reset 后面加id(版本号)可以直接回到指定版本

![](F:\前端开发\git和GitHub学习\images\resetId.png)



##### 7.2 git reset HEAD^

> 回到当前版本的上一个版本
>
> - 一个^是回到上一个
> - 两个^就是回到上两个
> - 以此类推……

##### 7.3 git reset --hard id

> - 强行回滚至指定的版本
> - 本地的源码也会变为上一个版本的内容，此命令慎用！

### 8.  git r m name

> - 删除文件
>
> - 删除完之后再git add一次这个文件就真的没有了
>
> - ![](F:\前端开发\git和GitHub学习\images\addtwo.png)
>
> - ![](F:\前端开发\git和GitHub学习\images\lsone.png)
>
> - git reset 还是可以找回来的 
>
> - git restore 也可以撤销删除 但是要撤销两次：**第一次 git restore --staged name 从暂存区撤回来；第二次 git restore 从工作区撤回来，此时文件才会显示在工作区**![](F:\前端开发\git和GitHub学习\images\git restore01.png)
>
>   ![](F:\前端开发\git和GitHub学习\images\git restore02.png)


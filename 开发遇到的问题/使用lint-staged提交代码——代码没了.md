#  使用lint-staged提交代码——代码没了



## 原因

为什么代码会没——因为在 commit 之前，会运行 lint-staged, 校验代码，这一步如果发生错误，代码就会被放到暂存区，也就是lint-staged帮我执行了` git stash`

`git stash` 用于将当前工作目录中的未提交更改（包括已跟踪文件的修改和暂存区的更改）临时保存起来，使工作目录恢复到干净的状态。这样你可以切换分支或执行其他操作，而无需提交未完成的工作。

## 解决方案

使用 `git stash list` 查看所有暂存记录。

输出示例:

![image-20250106152042590](D:\Project\note\images\git-stash-list命令.png)

``````
stash@{0}: 描述信息
stash@{1}: 描述信息
``````

使用**`git stash pop`**或**`git stash apply`**将上一次stash(暂存)恢复到工作目录

- **`git stash pop`**：
  - 恢复最近一次暂存的更改。
  - 从 stash 列表中移除该记录。
- **`git stash apply`**：
  - 恢复最近一次暂存的更改。
  - **不**从 stash 列表中移除该记录。

恢复指定的stash(暂存)记录git stash pop "stash@{1}"

``````
git stash pop
git stash apply
git stash pop "stash@{1}"
``````

**如果恢复的更改与当前工作目录的内容冲突，Git 会提示冲突并需要手动解决。**


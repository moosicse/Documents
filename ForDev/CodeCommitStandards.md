[Home](../README.md)

# Code Commit Standards

> 代码提交规范

以下内容按步骤书写

## 新建 Branch

当需要提交代码更新的时候，首先从当前 master 分支创建一个新分支，以 __yourName/thingsToDo__ 命名。例如 *touko/addMusicFunction* 。然后在这个分支中进行代码修改和提交。

## 提交 Pull Request

将分支提交到远程仓库后，在 Repository 页面提交 Pull Request 请求，并在请求中写明自己这段代码所做的事。  

## Review

当代码提交后，应指定至少一人进行代码 Review。当 Review 通过后，才能进行代码合并。

## Merge

当 Review 通过，并完成 Circle CI 检查（如果有）后，合并分支并手动运行程序进行检查。

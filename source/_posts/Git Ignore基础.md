---
title: Git Ignore基础
date: 2023-09-19 11:58:00
tags: git
categories: Git
---
# Git Ignore基础

Git中忽略已修改（但未提交）的文件
在本文中，我们将介绍如何在Git中忽略已修改的文件，但是没有提交的文件。有时候，在开发过程中我们可能会修改一些文件，但是由于各种原因，我们可能并不希望将这些修改提交到Git版本控制系统中。这可能是因为这些修改不是最终版本，或者是因为这些修改仅适用于开发环境而不适用于生产环境。


Git Ignore基础
首先，让我们简要了解Git Ignore的基本概念。在Git中，.gitignore文件用于指定哪些文件和文件夹应该被Git忽略。这些被忽略的文件不会被包含在Git仓库中，Git不会跟踪和管理这些被忽略的文件。.gitignore文件可以被放置在Git仓库的根目录下，也可以放置在子目录中。

Git Ignore规则可以使用通配符来匹配文件名、文件夹名或路径。常用的通配符包括*（用于匹配任意字符），?（用于匹配单个字符），**（用于匹配任意数量的目录或文件），[]（用于匹配一组字符），!（表示否定匹配）等。

以下是一个示例的.gitignore文件内容：
```text
# 忽略所有.txt文件
*.txt

# 忽略logs文件夹及其内容
logs/

# 仅忽略根目录下的foo.txt文件，而不忽略子目录中的foo.txt文件
/foo.txt

# 忽略文件名为bar.txt的文件夹
/bar.txt/
Bash
```
忽略已被修改但未提交的文件
通常情况下，Git会将已修改但未提交的文件添加到暂存区（Index）中，以便在下次提交时将这些文件包含进去。然而，有时候我们可能希望忽略这些已修改的文件，而不让它们出现在提交中。

为了达到这个目的，我们可以使用.gitignore文件来指定要忽略的文件和文件夹，但是这种方法只适用于尚未加入暂存区的文件。如果文件已经加入暂存区，.gitignore文件的规则将不会生效。

但是，有一种方法可以解决这个问题。可以使用git update-index命令的--assume-unchanged选项来告诉Git将指定文件标记为“已修改但不关心”。这样，Git将不再跟踪这些文件的修改，除非你明确地告诉Git你要跟踪这些文件的修改。

以下是使用git update-index命令来忽略已修改但未提交的文件的示例：
```text
# 将文件标记为“已修改但不关心”
git update-index --assume-unchanged <file>

# 取消文件的“已修改但不关心”标记
git update-index --no-assume-unchanged <file>
Bash
```
例如，在项目中有一个名为config.txt的文件需要被忽略其修改。你可以使用以下命令来标记该文件为“已修改但不关心”：
```text
git update-index --assume-unchanged config.txt
Bash
```
现在，即使你对config.txt文件进行了修改，Git也不会将这些修改包含在下次提交中。

请注意，使用git update-index命令标记文件为“已修改但不关心”只是告诉Git忽略这些文件的修改，它们仍然会出现在进行版本控制的文件列表中。

取消已被修改但不希## 取消已被修改但不希望忽略的文件
如果你确定要让Git再次跟踪某个已被标记为“已修改但不关心”的文件，你可以使用git update-index命令的--no-assume-unchanged选项来取消这个标记。

假设你之前使用了以下命令将config.txt文件标记为“已修改但不关心”：
```markdown
git update-index --assume-unchanged config.txt
Bash
```
现在，如果你想要Git跟踪config.txt文件的修改，你可以运行以下命令来取消这个标记：
```text
git update-index --no-assume-unchanged config.txt
Bash
```
这样，Git将再次跟踪config.txt文件的修改，并将它们包含在下次提交中。

忽略已被修改但未提交的文件的注意事项
尽管使用git update-index命令的--assume-unchanged选项可以让我们忽略已被修改但未提交的文件，但是需要注意以下几点：

.gitignore文件的规则不会自动应用于已被修改但未提交的文件，需要使用git update-index命令来手动标记这些文件为“已修改但不关心”。
如果一个被标记为“已修改但不关心”的文件被删除并重新添加到仓库中，Git将不再将其视为“已修改但不关心”，而是将其视为一个普通的已修改文件。这意味着，如果你希望继续忽略这个文件的修改，你需要重新使用git update-index命令来标记它为“已修改但不关心”。
标记文件为“已修改但不关心”只是告诉Git在提交时不包括这些文件的修改，但这些文件仍然会出现在进行版本控制的文件列表中。因此，在协作开发中，其他人仍然可以看到这些被忽略的修改。
总结
在本文中，我们学习了如何在Git中忽略已被修改但未提交的文件。我们了解了.gitignore文件的基本概念，并学会了使用通配符来指定要忽略的文件和文件夹。我们还介绍了如何使用git update-index命令的--assume-unchanged选项来标记文件为“已修改但不关心”，以及如何使用--no-assume-unchanged选项来取消这个标记。

忽略已被修改但未提交的文件对于保持Git仓库的干净和可维护非常有帮助。通过正确使用.gitignore文件和git update-index命令，我们可以更好地管理版本控制系统，并确保只提交我们真正关心的修改。







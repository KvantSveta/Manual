# Git

```bash
git add
```

```bash
git commit
```

```bash
git branch
```

```bash
git branch -d ветка_на_удаление
```

```bash
git checkout ветка/коммит
```

```bash
git checkout -b переход на новую ветку
```

```bash
git merge ветка
```

```bash
git log --graph --pretty=short
```

```bash
git fetch origin
```

```bash
git push origin ветка
```

```bash
git pull origin
```

```bash
git clone ssh://user@server:~/.../project.git
```

```bash
git clone @server:~/.../project.git
```

```bash
git show коммит
```

удаление коммита

```bash
git reset --hard {хэш коммита, на который необходимо перейти}
```

удаление внешней ветки

```bash
git push origin --delete {branch_name}
```

change the last commit message

```bash
git commit --amend -m "commit message"
```

amending the message of the most recently pushed commit

```bash
git push --force origin branch_name
```

set sublime as default git editor

```bash
git config --global core.editor "subl --wait"
```

set vscode as default git editor

```bash
git config --global core.editor "code --wait"
```

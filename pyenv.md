# pyenv

install pyenv via [pyenv-installer](https://github.com/pyenv/pyenv-installer)

```bash
curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | zsh
```

update .zshrc

```bash
export PATH="~/.pyenv/bin:$PATH"
eval "$(pyenv init -)"
eval "$(pyenv virtualenv-init -)"
```

apply new resource

```bash
source .zshrc
```

update pyenv

```bash
pyenv update
```

show available python versions

```bash
pyenv install --list
```

install python 3.7.0

```bash
pyenv install 3.7.0
```

create virtualenv with python 3.7.0 which named venv

```bash
pyenv virtualenv 3.7.0 venv
```

use virtualenv (venv) with python 3.7.0 for current directory

```bash
pyenv local venv
```

## Установка Git

### Windows
- Скачать установщик «Git for Windows» с сайта git-scm.com и установить с настройками по умолчанию.
```powershell
https://github.com/git-for-windows/git/releases/download/v2.51.2.windows.1/Git-2.51.2-64-bit.exe
```


### macOS

- через Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

```bash
brew install git
```

### Проверка установки

```bash
git --version
```

---

## Базовая настройка (глобально)

Установите имя и почту (используются в метаданных коммитов):

```bash
git config --global user.name "Ваше Имя"
git config --global user.email "you@example.com"
```


Посмотреть текущие настройки:

```bash
git config --list --show-origin
```

---

## SSH‑ключи (рекомендуется для GitHub/GitLab)

1) Сгенерируйте ключ Ed25519:

```bash
ssh-keygen -t ed25519 -C "you@example.com"
```

2) Запустите ssh-agent и добавьте ключ:

```bash
# macOS/Linux
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# Windows (Git Bash)
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

3) Скопируйте публичный ключ и добавьте в аккаунт GitHub/GitLab:

```bash
# macOS
pbcopy < ~/.ssh/id_ed25519.pub

# Linux (вариант с xclip)
xclip -sel clip < ~/.ssh/id_ed25519.pub

# Windows (Git Bash)
clip < ~/.ssh/id_ed25519.pub
```

4) Проверьте подключение к GitHub:

```bash
ssh -T git@github.com
```

Опционально добавьте в `~/.ssh/config`:

```sshconfig
Host github.com
	HostName github.com
	User git
	IdentityFile ~/.ssh/id_ed25519
```

---

## Старт работы с репозиторием

Создать новый репозиторий в текущей папке:

```bash
git init
```

Клонировать существующий:

```bash
git clone <URL>
```

Проверить статус, добавить файлы и сделать коммит:

```bash
git status
git add <файл_или_путь>   # или: git add .
git commit -m "Сообщение коммита"
```

Просмотреть историю:

```bash
git log --oneline --graph --decorate --all
git show <коммит>
```

Посмотреть изменения:

```bash
git diff            # неиндексированные изменения
git diff --staged   # изменения в индексе (готовые к коммиту)
```

---

## Ветки и переключение

Создать ветку и переключиться:

```bash
git switch -c feature/awesome
# Альтернатива: git checkout -b feature/awesome
```

Список веток и удаление локальной ветки:

```bash
git branch
git branch -d feature/awesome   # удаление слитой ветки
git branch -D feature/awesome   # принудительное удаление
```

Переименование текущей ветки:

```bash
git branch -m main
```

Слияние (merge) и ребейз (rebase):

```bash
# Находясь в целевой ветке (например, main) слить изменения из другой ветки
git merge feature/awesome

# Переписать историю своей ветки поверх актуального main
git fetch origin
git rebase origin/main
```

---

## Удалённые репозитории

Привязать удалённый origin и запушить первую ветку:

```bash
git remote add origin git@github.com:USER/REPO.git  # или HTTPS URL
git push origin main
```

Синхронизация:

```bash
git fetch        # забрать новые ссылки и объекты
git pull         # забрать и слить в текущую ветку
git push         # отправить локальные коммиты
```

Проверить адреса remotes:

```bash
git remote -v
```

Сменить URL (например, с HTTPS на SSH):

```bash
git remote set-url origin git@github.com:USER/REPO.git
```

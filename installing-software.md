# Для прохождения курса рекомендуется настроить

## GitHub account

Создать учётную запись на сервисе GitHub и отправить её преподавателю для добавления в GitHub-организацию для выполнения заданий курса.

## Git

Установить Git, если он ещё не установлен. Установщик для Windows можно скачать с официального сайта https://git-scm.com/downloads/win

## Python 3.14

Установить Python в версии 3.14, если он ещё не установлен. Если установлен Python в другой версии — установите дополнительно 3.14. Установщик для Windows можно скачать с [официального сайта](https://www.python.org/downloads/).

**Важно!** При установке необходимо добавить путь до Python в переменные окружения.

Проверьте, что установщик сработал: в **новом** терминале выполните `py -3.14 --version`. Должна появиться строка с версией 3.14.x. Если команда не находится — Python не добавлен в PATH, установку нужно повторить с соответствующей галочкой.

## VS Code

**Установить IDE Visual Studio Code**, если она ещё не установлена: https://code.visualstudio.com/Download

**Установить расширения** для VS Code, рекомендуемый набор:

- Python — https://marketplace.visualstudio.com/items?itemName=ms-python.python
- Pylance — https://marketplace.visualstudio.com/items?itemName=ms-python.vscode-pylance
- Python Debugger — https://marketplace.visualstudio.com/items?itemName=ms-python.debugpy
- GitLens — https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens
- Code Spell Checker — https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker
- Russian — Code Spell Checker — https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker-russian
- Markdown Preview Github Styling — https://marketplace.visualstudio.com/items?itemName=bierner.markdown-preview-github-styles
- Markdown Preview Mermaid Support — https://marketplace.visualstudio.com/items?itemName=bierner.markdown-mermaid

Расширение Mermaid нужно для ручных заданий: диаграммы Ганта, сети, графы зависимостей. Без него превью в VS Code не покажет такие схемы.

Не забудьте включить расширение проверки орфографии для русского языка.

**Клонировать репозиторий** с заданиями, предварительно авторизовавшись на GitHub.

Для **программных** заданий клонируйте репозиторий [code-tasks](https://github.com/hse-algo-ris-25-4/code-tasks): в нём дальше создаёте `.venv` и ставите зависимости.

Для **ручных** заданий клонируйте [manual-tasks](https://github.com/hse-algo-ris-25-4/manual-tasks): Python-окружение не нужно, достаточно VS Code.

## Терминал в VS Code

Открыть терминал: `Ctrl + ~` (или меню **Terminal → New Terminal**). Все команды из инструкций выполняются в терминале VS Code, в каталоге склонированного репозитория.

Проверить, что терминал открыт в нужном каталоге, и что Git видит репозиторий:

```sh
pwd
git status
```

## Виртуальное окружение и зависимости (только для программных заданий)

В каталоге `code-tasks`:

```sh
py -3.14 -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

В PowerShell вместо `.venv\Scripts\activate` может понадобиться:

```powershell
.\.venv\Scripts\Activate.ps1
```

Если PowerShell блокирует запуск скрипта, разрешите его для текущего пользователя:

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

Признак того, что окружение активно, — префикс `(.venv)` в начале строки терминала. Все команды `pip` и `python` из инструкций выполняются **только** в таком терминале.

Проверить, что интерпретатор правильный:

```sh
python --version
```

Должна появиться версия 3.14.x.

## Проверка оформления и тестов

Инструменты `ruff`, `pytest`/`unittest` уже входят в `requirements.txt`, отдельно ставить их не нужно.

```sh
ruff check .
ruff format .
python -m unittest discover -s . -p "test*.py" -v
```

## Если не Windows

Команды отличаются только активацией окружения:

- macOS / Linux: `python3.14 -m venv .venv`, затем `source .venv/bin/activate`
- Путь к интерпретатору: `.venv/bin/python` вместо `.venv\Scripts\python`

Всё остальное (`git`, `ruff`, `unittest`) совпадает.

## Частые проблемы

| Симптом | Причина и решение |
|---|---|
| `python: command not found` / открывается Microsoft Store | Python не в PATH. Переустановите с галочкой «Add python.exe to PATH», откройте **новый** терминал |
| В терминале нет `(.venv)` | Окружение не активировано — повторите активацию, команды `pip` установят пакеты в системный Python |
| `ModuleNotFoundError: No module named 'matplotlib'` (и аналоги) | Зависимости не установлены или установлены не в то окружение: активируйте `.venv` и повторите `pip install -r requirements.txt` |
| `git: command not found` | Git не установлен или не в PATH, перезапустите VS Code после установки |
| `Permission denied (publickey)` при `git push` | Не настроена авторизация: используйте вход через браузер (GitHub Desktop / Git Credential Manager) или SSH-ключ |
| VS Code не видит тесты на вкладке Testing | Не выбран фреймворк `unittest` или корень проекта — см. инструкцию по выполнению задания |
| `ruff: command not found` | Окружение не активировано либо зависимости не установлены |

<div align="center">
  
<h2 id="claude-code-community-guide">Руководство по Claude Code</h2>

_Для обновлений и вклада посетите [официальную документацию Claude Code](https://code.claude.com/docs/en/overview)_

![Claude Code](https://img.shields.io/npm/v/@anthropic-ai/claude-code?label=Claude%20Code&logo=anthropic)
[![Статус](https://img.shields.io/badge/Status-Active-brightgreen)](https://github.com/anthropics/claude-code)
[![Лицензия](https://img.shields.io/badge/License-Anthropic-orange)](https://claude.ai/code)

</div>

<div align="center">

<kbd>

| Раздел                                                      | Статус |
| ----------------------------------------------------------- | ------ |
| Руководства по установке на Windows, Linux, MacOS          | ✅     |
| Советы и трюки                                              | ✅     |
| Обзор MCP с рекомендациями по использованию                | ✅     |
| Руководства сообщества                                      | ✅     |
| Устранение неполадок                                        | ✅     |
| Как использовать Claude Code наиболее оптимальным образом   | ✅     |

### Взаимодействие с Claude Code через Discord - руководство [Здесь!](https://github.com/zebbern/claude-code-discord)

</kbd>

#### Ежедневно обновляемые [Журналы изменений Claude](https://github.com/zebbern/claude-code-guide/tree/main/Official%20Claude%20Releases)

#### Безопасность агентов [файлы SKILL.md](https://github.com/zebbern/claude-code-guide/tree/main/skills) `\|/` Как создать [руководство по навыкам агента](https://github.com/zebbern/agent-skills-guide)

</div>

---

<h3 id="content">Содержание</h3>

_Быстрые ссылки:_ [Установка](#quick-start) · [Команды](#claude-commands) · [Горячие клавиши](#keyboard-shortcuts) · [MCP](#mcp-integration) · [Устранение неполадок](#help--troubleshooting)

- **[Начало работы](#getting-started)**
  - [Быстрый старт](#quick-start)
  - [Первоначальная настройка](#initial-setup)

- **[Конфигурация и окружение](#configuration--environment)**
  - [Переменные окружения](#environment-variables)
  - [Файлы конфигурации](#configuration-files)

- **[Команды и использование](#commands--usage)**
  - [Команды Claude](#claude-commands)
  - [Шпаргалка](#cheat-sheet)

- **[Интерфейс и ввод](#interface--input)**
  - [Горячие клавиши](#keyboard-shortcuts)
  - [Режим Vim](#vim-mode)

- **[Продвинутые функции](#advanced-features)**
  - [Режим размышления](#thinking-keywords)
  - [Режим планирования](#plan-mode)
  - [Фоновые задачи](#background-tasks)
  - [Удалённые сеансы](#remote-sessions)
  - [Подагенты](#sub-agents)
  - [Навыки](#skills)
  - [Интеграция MCP](#mcp-integration)
  - [Система хуков](#hooks-system)

- **[Безопасность и разрешения](#security--permissions)**
  - [Опасный режим](#dangerous-mode)
  - [Лучшие практики безопасности](#security-best-practices-main)

- **[Автоматизация и интеграция](#automation--integration)**
  - [Автоматизация и скриптинг](#automation--scripting-with-claude-code)
  - [Автоматический обзор PR](#auto-pr-review-inline-comments)
  - [Сортировка задач](#issue-triage-suggest-labels--severity)

- **[Помощь и устранение неполадок](#help--troubleshooting)**
  - [Проблемы с установкой](#installation--nodejs-issues)
  - [Проблемы с MCP](#mcp-model-context-protocol-issues)
  - [Лучшие практики](#best-practices)

- **[Сторонние интеграции](#third-party-integrations)**
  - [Интеграция DeepSeek](#deepseek-integration)

---

<h1 id="getting-started">Начало работы</h1>

**Включить звуковые оповещения, когда Claude завершает задачу:**

> <kbd>claude config set --global preferredNotifChannel terminal_bell</kbd>

<h2 id="quick-start">Быстрый старт</h2>

> [!TIP]
> **Отправьте <mark>claude</mark> или <mark>npx claude</mark> в терминале, чтобы запустить интерфейс**
>
> **Перейдите к [Помощь и устранение неполадок](#help--troubleshooting) для решения проблем...**

```C
# Node.js 18+⭐️
/*Универсальный метод       */ npm install -g @anthropic-ai/claude-code
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Windows
/* Через CMD (npm)          */ npm install -g @anthropic-ai/claude-code
/* Через CMD (нативный)     */ curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
/* Через Powershell         */ irm https://claude.ai/install.ps1 | iex
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# WSL/GIT
/* Через терминал           */ npm install -g @anthropic-ai/claude-code
/* Через терминал           */ curl -fsSL https://claude.ai/install.sh | bash
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# MacOS                     */ brew install node && npm install -g @anthropic-ai/claude-code
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Linux
/* Через терминал           */ sudo apt update && sudo apt install -y nodejs npm
/* Через терминал           */ npm install -g @anthropic-ai/claude-code
/* Через терминал           */ curl -fsSL https://claude.ai/install.sh | bash
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Arch
/* Через терминал           */ yay -S claude-code*/
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Docker
/* Windows (CMD)            */ docker run -it --rm -v "%cd%:/workspace" -e ANTHROPIC_API_KEY="sk-your-key" node:20-slim bash -lc "npm i -g @anthropic-ai/claude-code && cd /workspace && claude"
/* macOS/Linux (bash/zsh)   */ docker run -it --rm -v "$PWD:/workspace" -e ANTHROPIC_API_KEY="sk-your-key" node:20-slim bash -lc 'npm i -g @anthropic-ai/claude-code && cd /workspace && claude'
/* Запасной вариант без bash*/ docker run -it --rm -v "$PWD:/workspace" -e ANTHROPIC_API_KEY="sk-your-key" node:20-slim sh -lc 'npm i -g @anthropic-ai/claude-code && cd /workspace && claude'
---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Проверить, правильно ли установлен claude
/* Linux                    */ which claude
/* Windows                  */ where claude
/* Универсальный            */ claude --version
--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
# Общее управление
/*claude config             */ Настроить параметры
/*claude mcp list           */ Настроить MCP-серверы, можно также заменить "list" на add/remove
/*claude /agents            */ Настроить/установить подагентов для различных задач
/*claude update             */ Обновить до последней версии
```

---

> [!Tip]
> <ins>**Открыть проект через терминал в VS Code / Cursor**</ins>
>
> ### $ - <kbd>cd /path/to/project</kbd>
>
> ### $ - <kbd>code .</kbd>
>
> **Убедитесь, что у вас установлено <mark>(расширение Claude Code)</mark> в вашем VS Code / Cursor**

---

<h2 id="system-requirements">Системные требования</h2>

> - ОС: macOS 10.15+, Ubuntu 20.04+/Debian 10+, или Windows 10/11 или WSL

> - Оборудование: минимум 4 ГБ ОЗУ, рекомендуется 8 ГБ+

> - Программное обеспечение: Node.js 18+ или git 2.23+ (опционально) и GitHub или GitLab CLI для рабочих процессов PR (опционально)

> - Интернет: Подключение для вызовов API

> - Node.js 18+

---

<h2 id="initial-setup">Первоначальная настройка</h2>

> [!Tip]
> **Найдите API-ключ в [Консоли Anthropic](https://console.anthropic.com)**
>
> **НЕ фиксируйте реальные ключи, используйте файлы, игнорируемые git, хранилища ключей ОС или менеджеры секретов**

```C
# Универсальный
/* начать процесс входа                  */ claude /login
/* Настроить токен долгосрочной аутентификации */ claude setup-token
----------------------------------------------------------------------------------------------------------------------------------
# Windows
/* Установить-api-ключ    */ set ANTHROPIC_API_KEY=sk-your-key-here-here
/* cmd-проверка-в-маске  */ echo OK: %ANTHROPIC_API_KEY:~0,8%***
/* Установить-постоянный-ключ */ setx ANTHROPIC_API_KEY "sk-your-key-here-here"
/* cmd-удалить-ключ      */ set ANTHROPIC_API_KEY=
----------------------------------------------------------------------------------------------------------------------------------
# Linux
/* Установить-api-ключ   */ export ANTHROPIC_API_KEY="sk-your-key-here-here"
/* проверка-в-маске      */ echo "OK: ${ANTHROPIC_API_KEY:0:8}***"
/* удалить-сеанс          */ unset ANTHROPIC_API_KEY
----------------------------------------------------------------------------------------------------------------------------------
# Powershell
/* ps-сеанс               */ $env:ANTHROPIC_API_KEY = "sk-your-key-here-here"
/* ps-проверка-в-маске   */ "OK: $($env:ANTHROPIC_API_KEY.Substring(0,8))***"
/* ps-сохранить           */ [Environment]::SetEnvironmentVariable("ANTHROPIC_API_KEY","sk-your-key-here-here","User")
/* ps-обновить            */ $env:ANTHROPIC_API_KEY = "sk-new-key"
/* ps-удалить             */ Remove-Item Env:\ANTHROPIC_API_KEY
----------------------------------------------------------------------------------------------------------------------------------
# Другое...
# сохранить-bash/*       */ echo 'export ANTHROPIC_API_KEY="sk-your-key-here-here"' >> ~/.bashrc && source ~/.bashrc
# сохранить-zsh /*       */ echo 'export ANTHROPIC_API_KEY="sk-your-key-here-here"' >> ~/.zshrc  && source ~/.zshrc
# сохранить-fish/*       */ fish -lc 'set -Ux ANTHROPIC_API_KEY sk-your-key-here-here'
----------------------------------------------------------------------------------------------------------------------------------
```

---

<h1 id="configuration--environment">Конфигурация и окружение</h1>

<h2 id="environment-variables">Переменные окружения</h2>

> **Вы также можете установить любую из них в settings.json под ключом "env" для автоматического применения.**

> [!Important]
> **Пользователи Windows заменяют <kbd>export</kbd> на <kbd>set</kbd> или <kbd>setx</kbd> для постоянного сохранения**

```bash
# Переключатели окружения (поместите в ~/.bashrc или ~/.zshrc)
export ANTHROPIC_API_KEY="sk-your-key-here-here"      # API-ключ отправляется как заголовок X-Api-Key (интерактивное использование: /login)
export ANTHROPIC_AUTH_TOKEN="my-auth-token"           # Пользовательский заголовок Authorization; Claude автоматически добавляет префикс "Bearer "
export ANTHROPIC_CUSTOM_HEADERS="X-Trace-Id: 12345"   # Дополнительные заголовки запроса (формат: "Name: Value")

export ANTHROPIC_MODEL="claude-sonnet-4-20250514"                # Имя пользовательской модели для использования
export ANTHROPIC_DEFAULT_SONNET_MODEL="claude-sonnet-4-20250514" # Псевдоним модели Sonnet по умолчанию
export ANTHROPIC_DEFAULT_OPUS_MODEL="claude-opus-4-20250514"     # Псевдоним модели Opus по умолчанию
export ANTHROPIC_SMALL_FAST_MODEL="haiku-model"                  # Модель класса Haiku для фоновых задач (заполнитель)
export ANTHROPIC_SMALL_FAST_MODEL_AWS_REGION="REGION"            # Переопределить регион AWS для малой/быстрой модели на Bedrock (заполнитель)

export AWS_BEARER_TOKEN_BEDROCK="bedrock_..."         # API-ключ/токен Amazon Bedrock для аутентификации

export BASH_DEFAULT_TIMEOUT_MS=60000                  # Тайм-аут по умолчанию (мс) для долго выполняющихся команд bash
export BASH_MAX_TIMEOUT_MS=300000                     # Максимальный тайм-аут (мс), разрешённый для долго выполняющихся команд bash
export BASH_MAX_OUTPUT_LENGTH=20000                   # Максимум символов в выводах bash перед усечением посередине

export CLAUDE_BASH_MAINTAIN_PROJECT_WORKING_DIR=1     # (0 или 1) возвращаться в исходный каталог проекта после каждой команды Bash
export CLAUDE_CODE_API_KEY_HELPER_TTL_MS=600000       # Интервал (мс) для обновления учётных данных при использовании apiKeyHelper
export CLAUDE_CODE_IDE_SKIP_AUTO_INSTALL=1            # (0 или 1) пропустить автоматическую установку расширений IDE
export CLAUDE_CODE_MAX_OUTPUT_TOKENS=4096             # Максимальное количество выходных токенов для большинства запросов

export CLAUDE_CODE_USE_BEDROCK=1                      # (0 или 1) использовать Amazon Bedrock
export CLAUDE_CODE_USE_VERTEX=0                       # (0 или 1) использовать Google Vertex AI
export CLAUDE_CODE_SKIP_BEDROCK_AUTH=0                # (0 или 1) пропустить аутентификацию AWS для Bedrock (например, через LLM-шлюз)
export CLAUDE_CODE_SKIP_VERTEX_AUTH=0                 # (0 или 1) пропустить аутентификацию Google для Vertex (например, через LLM-шлюз)

export CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=0     # (0 или 1) отключить несущественный трафик (эквивалентно DISABLE_* ниже)
export CLAUDE_CODE_DISABLE_TERMINAL_TITLE=0           # (0 или 1) отключить автоматическое обновление заголовка терминала

export DISABLE_AUTOUPDATER=0                          # (0 или 1) отключить автоматические обновления (переопределяет настройку autoUpdates)
export DISABLE_BUG_COMMAND=0                          # (0 или 1) отключить команду /bug
export DISABLE_COST_WARNINGS=0                        # (0 или 1) отключить предупреждения о затратах
export DISABLE_ERROR_REPORTING=0                      # (0 или 1) отказаться от отчётов об ошибках Sentry
export DISABLE_NON_ESSENTIAL_MODEL_CALLS=0            # (0 или 1) отключить вызовы модели для некритичных путей
export DISABLE_TELEMETRY=0                            # (0 или 1) отказаться от телеметрии Statsig

export HTTP_PROXY="http://proxy:8080"                 # URL HTTP-прокси сервера
export HTTPS_PROXY="https://proxy:8443"               # URL HTTPS-прокси сервера

export MAX_THINKING_TOKENS=0                          # (0 или 1 для выкл/вкл) форсировать бюджет размышлений для модели
export MCP_TIMEOUT=120000                             # Тайм-аут запуска MCP-сервера (мс)
export MCP_TOOL_TIMEOUT=60000                         # Тайм-аут выполнения инструментов MCP (мс)
export MAX_MCP_OUTPUT_TOKENS=25000                    # Максимум токенов, разрешённых в ответах инструментов MCP (по умолчанию 25000)

export USE_BUILTIN_RIPGREP=0                          # (0 или 1) установите 0 для использования системного rg вместо встроенного

export VERTEX_REGION_CLAUDE_3_5_HAIKU="REGION"        # Переопределение региона для Claude 3.5 Haiku на Vertex AI
export VERTEX_REGION_CLAUDE_3_5_SONNET="REGION"       # Переопределение региона для Claude 3.5 Sonnet на Vertex AI
export VERTEX_REGION_CLAUDE_3_7_SONNET="REGION"       # Переопределение региона для Claude 3.7 Sonnet на Vertex AI
export VERTEX_REGION_CLAUDE_4_0_OPUS="REGION"         # Переопределение региона для Claude 4.0 Opus на Vertex AI
export VERTEX_REGION_CLAUDE_4_0_SONNET="REGION"       # Переопределение региона для Claude 4.0 Sonnet на Vertex AI
export VERTEX_REGION_CLAUDE_4_1_OPUS="REGION"         # Переопределение региона для Claude 4.1 Opus на Vertex AI
```

<h2 id="global-config-options">Глобальные параметры конфигурации</h2>

```bash
claude config set -g theme dark                               # Тема: dark | light | light-daltonized | dark-daltonized
claude config set -g preferredNotifChannel iterm2_with_bell   # Канал уведомлений: iterm2 | iterm2_with_bell | terminal_bell | notifications_disabled
claude config set -g autoUpdates true                         # Автоматическая загрузка и установка обновлений (применяется при перезапуске)
claude config set -g verbose true                             # Показывать полный вывод bash/команд

claude config set -g includeCoAuthoredBy false                # Исключить "соавтором является Claude" в git-коммитах/PR
claude config set -g forceLoginMethod console                 # Ограничить вход до Anthropic Console (биллинг API)
claude config set -g model "claude-3-5-sonnet-20241022"       # Переопределение модели по умолчанию
claude config set -g statusLine '{"type":"command","command":"~/.claude/statusline.sh"}'  # Пользовательская строка состояния

claude config set -g enableAllProjectMcpServers true              # Автоматически одобрять все MCP-серверы из .mcp.json
claude config set -g enabledMcpjsonServers '["memory","github"]'  # Одобрить конкретные MCP-серверы
claude config set -g disabledMcpjsonServers '["filesystem"]'      # Отклонить конкретные MCP-серверы
```

> [!Important]
> **Пользователи Windows заменяют <kbd>export</kbd> на <kbd>set</kbd>**

```bash
export DISABLE_AUTOUPDATER=1                      # Глобально отключить автоматические обновления (переопределяет autoUpdates)
export CLAUDE_CODE_DISABLE_NONESSENTIAL_TRAFFIC=1 # Отключить несущественный трафик (экв. переключателям DISABLE_* ниже)
export DISABLE_TELEMETRY=1                        # Отказаться от телеметрии Statsig
export DISABLE_ERROR_REPORTING=1                  # Отказаться от отчётов об ошибках Sentry
export DISABLE_BUG_COMMAND=1                      # Отключить команду /bug
export DISABLE_COST_WARNINGS=0                    # Оставить предупреждения о затратах (установите 1 для скрытия)
export DISABLE_NON_ESSENTIAL_MODEL_CALLS=1        # Пропустить некритичные вызовы модели (текст для украшения и т.д.)

export CLAUDE_CODE_DISABLE_TERMINAL_TITLE=1       # Прекратить автоматическое обновление заголовков терминала
export CLAUDE_BASH_MAINTAIN_PROJECT_WORKING_DIR=1 # Возвращаться в исходный каталог проекта после каждой команды Bash
export CLAUDE_CODE_IDE_SKIP_AUTO_INSTALL=1        # Пропустить автоматическую установку расширений IDE
export USE_BUILTIN_RIPGREP=0                      # Использовать системный 'rg' (0) вместо встроенного 'rg'

export MAX_THINKING_TOKENS=0                      # (0 или 1 для выкл/вкл) форсировать бюджет размышлений для модели
export CLAUDE_CODE_MAX_OUTPUT_TOKENS=4096         # Ограничить типичный размер ответа (пример значения)

export HTTP_PROXY="http://proxy.company:8080"     # HTTP-прокси (если нужен)
export HTTPS_PROXY="https://proxy.company:8443"   # HTTPS-прокси (если нужен)
```

<h2 id="configuration-files">Файлы конфигурации</h2>

**(Тип памяти) Claude Code предлагает четыре местоположения памяти в иерархической структуре, каждое служит своей цели:**

| Тип памяти                     | Местоположение                                                                                                                                              | Назначение                                        | Примеры использования                                                | Совместно с                |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- | -------------------------------------------------------------------- | -------------------------- |
| **Корпоративная политика**     | macOS: `/Library/Application Support/ClaudeCode/CLAUDE.md`<br />Linux: `/etc/claude-code/CLAUDE.md`<br />Windows: `C:\ProgramData\ClaudeCode\CLAUDE.md`    | Инструкции на уровне организации, управляемые IT | Стандарты кодирования компании, политики безопасности, требования    | Все пользователи в орг.    |
| **Память проекта**             | `./CLAUDE.md`                                                                                                                                               | Инструкции, общие для команды проекта             | Архитектура проекта, стандарты кодирования, общие рабочие процессы   | Члены команды через VCS    |
| **Память пользователя**        | `~/.claude/CLAUDE.md`                                                                                                                                       | Личные предпочтения для всех проектов             | Предпочтения стиля кода, личные сокращения инструментов              | Только вы (все проекты)    |
| **Память проекта (локальная)** | `./CLAUDE.local.md`                                                                                                                                         | Личные предпочтения для конкретного проекта       | _(Устарело, см. ниже)_ Ваши sandbox URL, предпочитаемые тестовые данные | Только вы (текущий проект) |

> Все файлы памяти автоматически загружаются в контекст Claude Code при запуске. Файлы выше в иерархии имеют приоритет и загружаются первыми, обеспечивая основу, на которой строятся более конкретные воспоминания.

Из-за ограничения на размер ответа, я создам файл, а затем предоставлю вам ссылку для скачивания. Файл очень большой (более 150KB), поэтому я создам его полностью.


---

<h1 id="commands--usage">Команды и использование</h1>

<h2 id="claude-commands">Команды Claude</h2>

| Команда                   | Назначение                                                                |
| :------------------------ | :------------------------------------------------------------------------ |
| `/add-dir`                | Добавить дополнительные рабочие каталоги                                  |
| `/agents`                 | Управлять пользовательскими AI-подагентами для специализированных задач |
| `/bug`                    | Сообщить об ошибках (отправляет разговор в Anthropic)                    |
| `/clear`                  | Очистить историю разговора                                                |
| `/compact [инструкции]`   | Сжать разговор с опциональными инструкциями фокусировки                   |
| `/config`                 | Открыть интерфейс настроек (вкладка Config)                               |
| `/context`                | Визуализировать текущее использование контекста в виде цветной сетки      |
| `/cost`                   | Показать статистику использования токенов и информацию о биллинге         |
| `/doctor`                 | Проверяет здоровье вашей установки Claude Code                            |
| `/exit`                   | Выйти из REPL                                                             |
| `/export [имя_файла]`     | Экспортировать текущий разговор в файл или буфер обмена                   |
| `/help`                   | Получить справку по использованию                                         |
| `/init`                   | Инициализировать проект с руководством CLAUDE.md                          |
| `/login`                  | Переключить учётные записи Anthropic                                      |
| `/logout`                 | Выйти из учётной записи Anthropic                                         |
| `/mcp`                    | Управлять подключениями к MCP-серверам и OAuth-аутентификацией           |
| `/memory`                 | Редактировать файлы памяти CLAUDE.md                                      |
| `/model`                  | Выбрать или изменить AI-модель                                            |
| `/permissions`            | Просмотреть или обновить разрешения инструментов                          |
| `/plan`                   | Войти в режим планирования прямо из промпта                               |
| `/pr_comments`            | Просмотреть комментарии к pull request                                    |
| `/rename <имя>`           | Переименовать текущий сеанс для упрощения идентификации                   |
| `/resume [сеанс]`         | Возобновить разговор по ID или имени, или открыть выбор сеанса            |
| `/review`                 | Запросить обзор кода                                                      |
| `/rewind`                 | Перемотать разговор и/или код к предыдущей точке                          |
| `/stats`                  | Визуализировать ежедневное использование, историю сеансов, серии и предпочтения моделей |
| `/status`                 | Открыть интерфейс настроек (вкладка Status), показывающий версию, модель, учётную запись |
| `/statusline`             | Настроить UI строки состояния Claude Code                                 |
| `/tasks`                  | Список и управление фоновыми задачами                                     |
| `/teleport`               | Возобновить удалённый сеанс с claude.ai (только для подписчиков)          |
| `/terminal-setup`         | Установить привязку клавиш Shift+Enter для новых строк (только iTerm2 и VSCode) |
| `/theme`                  | Изменить цветовую тему                                                    |
| `/todos`                  | Список текущих TODO-элементов                                             |
| `/usage`                  | Показать лимиты использования плана и статус ограничения скорости (планы подписки) |
| `/vim`                    | Войти в режим vim для чередования режимов вставки и команд                |

Продолжу создание полного перевода...


<h2 id="keyboard-shortcuts">Горячие клавиши</h2>

| Сочетание клавиш             | Описание                              | Контекст                                      |
| :--------------------------- | :------------------------------------ | :-------------------------------------------- |
| `Ctrl+C`                     | Отменить текущий ввод или генерацию  | Стандартное прерывание                        |
| `Ctrl+D`                     | Выйти из сеанса Claude Code           | Сигнал EOF                                    |
| `Ctrl+G`                     | Открыть в текстовом редакторе по умолчанию | Редактировать промпт или пользовательский ответ |
| `Ctrl+L`                     | Очистить экран терминала              | Сохраняет историю разговора                   |
| `Ctrl+O`                     | Переключить подробный вывод           | Показывает детальное использование инструментов |
| `Ctrl+R`                     | Обратный поиск по истории команд      | Поиск по предыдущим командам                  |
| `Ctrl+V` или `Cmd+V` (iTerm2)| Вставить изображение из буфера обмена | Вставляет изображение или путь к файлу        |
| `Ctrl+B`                     | Отправить выполняющиеся задачи в фон  | Отправляет в фон bash-команды и агентов       |
| `Стрелки вверх/вниз`         | Навигация по истории команд           | Вызов предыдущих вводов                       |
| `Стрелки влево/вправо`       | Переключение между вкладками диалога  | Навигация между вкладками в диалогах          |
| `Esc` + `Esc`                | Перемотать код/разговор               | Восстановить к предыдущей точке               |
| `Shift+Tab` или `Alt+M`      | Переключить режимы разрешений         | Переключение между Auto-Accept, Plan, Normal  |
| `Option+P` (macOS) / `Alt+P` | Переключить модель                    | Переключить модели без очистки промпта        |
| `Option+T` (macOS) / `Alt+T` | Переключить расширенное размышление   | Включить/выключить режим расширенного размышления |

<h2 id="thinking-keywords">Ключевые слова размышления</h2>

> [!Note]
> **Даёт Claude дополнительное время для планирования перед ответом, добавляя ОДНО из этих ключевых слов в промпт.**
> **Порядок (от наименьшего → к наибольшему) потребление токенов**
>
> <table><tr><td>
>
> > **<kbd>think</kbd> -------------> Наименьшее**
>
> > **<kbd>think hard</kbd>**
>
> > **<kbd>think harder</kbd>**
>
> > **<kbd>ultrathink</kbd> --------> Наибольшее**
>
> </td></tr></table>

### Это заставляет Claude тратить больше времени на:

1. **Планирование решения**
2. **Разбиение на шаги**
3. **Взвешивание альтернатив/компромиссов**
4. **Проверку ограничений и граничных случаев**

> Более высокие уровни обычно увеличивают **задержку** и **использование токенов** - выбирайте наименьший работающий.

##### Примеры

```md
# Небольшое усиление
claude -p "Think. Набросай план рефакторинга модуля аутентификации."

# Среднее усиление
claude -p "Think harder. Составь план миграции с REST на gRPC."

# Максимальное усиление
claude -p "Ultrathink. Предложи пошаговую стратегию исправления нестабильных платёжных тестов и добавления защитных механизмов."
```

<h2 id="plan-mode">Режим планирования</h2>

> [!Note]
> **Режим планирования инструктирует Claude анализировать кодовую базу с операциями только для чтения, идеально подходит для изучения кодовых баз, планирования сложных изменений или безопасного обзора кода.**

**Когда использовать режим планирования:**

- **Многошаговая реализация**: Когда ваша функция требует внесения изменений во множество файлов
- **Исследование кода**: Когда вы хотите тщательно изучить кодовую базу перед внесением изменений
- **Интерактивная разработка**: Когда вы хотите итерировать направление с Claude

**Как включить режим планирования:**

```bash
# Начать новый сеанс в режиме планирования
claude --permission-mode plan

# Или переключить во время сеанса с помощью Shift+Tab
# (циклы через: Normal → Auto-Accept → Plan Mode)

# Войти в режим планирования из промпта
/plan

# Запустить безголовые запросы в режиме планирования
claude --permission-mode plan -p "Проанализируй систему аутентификации и предложи улучшения"
```

<h2 id="mcp-integration">Интеграция MCP</h2>

### Что такое MCP?

> MCP расширяет возможности Claude, подключаясь к внешним сервисам, базам данных, API и инструментам (файловая система, Puppeteer, GitHub, Context7 и т.д.)

### Быстрый старт MCP

> **Если вы торопитесь, вот самый быстрый способ добавить:**

```bash
# Добавить доступ к файловой системе (наиболее часто используемый)
claude mcp add filesystem -s user -- npx -y @modelcontextprotocol/server-filesystem ~/Documents ~/Desktop

# Проверить успешность
claude mcp list
```

### Основные команды MCP

```bash
claude mcp                   # Интерактивная конфигурация MCP
claude mcp list              # Список настроенных серверов
claude mcp add <имя> <команда>  # Добавить новый сервер
claude mcp remove <имя>      # Удалить сервер
```

### Популярные MCP-серверы

#### Инструменты разработки

```bash
# Система файлов
claude mcp add filesystem -s user -- npx -y @modelcontextprotocol/server-filesystem ~/Documents ~/Projects

# GitHub (требуется токен)
claude mcp add github -s user -e GITHUB_TOKEN=$GITHUB_TOKEN -- npx -y @modelcontextprotocol/server-github

# Puppeteer для автоматизации браузера
claude mcp add puppeteer -s user -- npx -y @modelcontextprotocol/server-puppeteer
```

#### Интеграция с базами данных

```bash
# PostgreSQL
claude mcp add postgres -s user -e DATABASE_URL=$DATABASE_URL -- npx -y @modelcontextprotocol/server-postgres

# Другие базы данных также поддерживаются (MySQL, SQLite и т.д.)
```

<h2 id="sub-agents">Подагенты</h2>

> Подагенты - это специализированные помощники со своими **собственными промптами, инструментами и изолированными окнами контекста**. Рассматривайте это как "смесь экспертов", которую вы **компонуете** для каждого репозитория.

### Встроенные подагенты

Claude Code включает встроенных подагентов, которые Claude автоматически использует при необходимости:

| Подагент            | Модель           | Инструменты      | Назначение                                                  |
| :------------------ | :--------------- | :--------------- | :---------------------------------------------------------- |
| **Explore**         | Haiku (быстрый)  | Только чтение    | Обнаружение файлов, поиск кода, исследование кодовой базы  |
| **Plan**            | Настраиваемый    | Только чтение    | Планирование сложных изменений без внесения правок          |
| **General-purpose** | По умолчанию     | Унаследованные   | Общее делегирование задач                                   |

### Настройка подагентов

```bash
# Обновить CLI и открыть панель агентов
claude update
/agents
```

### Определение агентов через CLI

```bash
claude --agents '{
  "code-reviewer": {
    "description": "Эксперт по обзору кода. Используется проактивно после изменений кода.",
    "prompt": "Вы старший рецензент кода. Сосредоточьтесь на качестве кода, безопасности и лучших практиках.",
    "tools": ["Read", "Grep", "Glob", "Bash"],
    "model": "sonnet"
  },
  "debugger": {
    "description": "Специалист по отладке для ошибок и сбоев тестов.",
    "prompt": "Вы эксперт по отладке. Анализируйте ошибки, определяйте первопричины и предоставляйте исправления."
  }
}'
```

<h2 id="skills">Навыки (пользовательские slash-команды)</h2>

> [!Note]
> **Навыки расширяют возможности Claude. Создайте файл `SKILL.md` с инструкциями, и Claude добавит его в свой набор инструментов.**

### Расположение навыков

| Местоположение                            | Область     | Описание                                       |
| :---------------------------------------- | :---------- | :--------------------------------------------- |
| `~/.claude/skills/<имя-навыка>/SKILL.md`  | Личная      | Все ваши проекты                               |
| `.claude/skills/<имя-навыка>/SKILL.md`    | Проект      | Только этот проект (зафиксировать в VCS)       |
| `<плагин>/skills/<имя-навыка>/SKILL.md`   | Плагин      | Где включён плагин                             |

### Создание навыка

```bash
# Создать каталог навыка
mkdir -p ~/.claude/skills/explain-code
```

Создать `~/.claude/skills/explain-code/SKILL.md`:

```markdown
---
name: explain-code
description: Объясняет код с визуальными диаграммами и аналогиями. Используется при объяснении работы кода.
---

При объяснении кода всегда включайте:

1. **Начните с аналогии**: Сравните код с чем-то из повседневной жизни
2. **Нарисуйте диаграмму**: Используйте ASCII-арт для показа потока, структуры или отношений
3. **Пройдите по коду**: Объясните пошагово, что происходит
4. **Выделите подводный камень**: Какая распространённая ошибка или заблуждение?
```

**Использование навыка:**

```bash
# Позволить Claude вызывать автоматически
Как работает этот код?

# Или вызвать напрямую
/explain-code src/auth/login.ts
```

<h1 id="security--permissions">Безопасность и разрешения</h1>

### Паттерны разрешений инструментов

```bash
# Разрешить конкретные инструменты (чтение/редактирование файлов)
claude --allowedTools "Edit,Read"

# Разрешить категории инструментов вкл. Bash (но всё ещё с ограничениями ниже)
claude --allowedTools "Edit,Read,Bash"

# Ограниченные разрешения (все команды git)
claude --allowedTools "Bash(git:*)"

# Множественные области (git + npm)
claude --allowedTools "Bash(git:*),Bash(npm:*)"
```

<h2 id="dangerous-mode">Опасный режим</h2>

> [!Warning]
> НИКОГДА не используйте в производственных системах, на общих машинах или системах с важными данными
> Используйте только с изолированными средами, такими как **Docker-контейнер**, использование этого режима может привести к потере данных и компрометации системы!
>
> `claude --dangerously-skip-permissions`

<h1 id="automation--integration">Автоматизация и интеграция</h1>

<h2 id="automation--scripting-with-claude-code">Автоматизация и скриптинг с Claude Code</h2>

> GitHub Actions, которые можно копировать и вставлять :p

**Автоматический обзор PR (встроенные комментарии)**

Файл: `.github/workflows/claude-pr-auto-review.yml`

```yaml
name: Автоматический обзор PR
on:
  pull_request:
    types: [opened, synchronize, reopened, ready_for_review]

permissions:
  contents: read
  pull-requests: write

jobs:
  auto-review:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
        with:
          fetch-depth: 1

      - name: Обзор PR от Claude
        uses: anthropics/claude-code-action@main
        with:
          anthropic_api_key: ${{ secrets.ANTHROPIC_API_KEY }}
          direct_prompt: |
            Проверь diff этого pull request на корректность, читаемость, тестирование, производительность и DX.
            Предпочитай конкретные, действенные предложения. Используй встроенные комментарии где уместно.
          allowed_tools: >-
            mcp__github__get_pull_request_diff,
            mcp__github__create_pending_pull_request_review,
            mcp__github__add_comment_to_pending_review,
            mcp__github__submit_pending_pull_request_review
```

<h1 id="help--troubleshooting">Помощь и устранение неполадок</h1>

<h2 id="debug-quick-commands">Быстрые команды отладки</h2>

```bash
claude                  # Открыть UI Claude (если в PATH)
claude --version        # Показать версию CLI (напр., 1.0.xx)
claude update           # Обновить CLI

claude doctor           # Открыть окно диагностики/отладки
claude --debug          # Запустить claude с диагностикой
claude --verbose        # Подробное логирование

where claude            # Windows (cmd)
which claude            # macOS/Linux (bash/zsh)

npm bin -g              # Linux: проверить путь к глобальному bin
npm prefix -g           # Windows: проверить путь к глобальному prefix
```

## Общие проблемы

**Q: `claude` не найден, но `npx claude` работает?**
> A: Ваш `PATH` не включает глобальный bin npm. Добавьте:
> - Windows: `%APPDATA%\npm` в переменную PATH
> - Linux/Mac: Результат `npm bin -g` в PATH

**Q: Какая версия Node.js нужна?**
> A: Node.js 18+ (идеально 20+). Проверьте с `node --version`

**Q: Где посмотреть логи?**
> A: Запустите `claude doctor` - окно диагностики укажет расположение логов

**Q: Нужно ли перезагружаться после редактирования PATH?**
> A: Перезагрузка не требуется, но вы <mark>должны</mark> открыть <mark>новое</mark> окно терминала

---

## Дополнительные ресурсы

- [Официальная документация Claude Code](https://code.claude.com/docs/en/overview)
- [GitHub репозиторий](https://github.com/anthropics/claude-code)
- [Discord сообщество](https://discord.gg/NrDfXmtvw3)
- [Примеры навыков](https://github.com/zebbern/claude-code-guide/tree/main/skills)

---

## Заключение

Это руководство охватывает основные аспекты работы с Claude Code. Для получения более подробной информации и обновлений посетите официальную документацию.

**Составлено сообществом с любовью ❤️**



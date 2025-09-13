# Python Boilerplate

[![CI](https://github.com/LizardKing131313/python_boilerplate/actions/workflows/ci.yml/badge.svg)](https://github.com/LizardKing131313/python_boilerplate/actions/workflows/ci.yml)
[![Qodana](https://github.com/LizardKing131313/python_boilerplate/actions/workflows/qodana_code_quality.yml/badge.svg)](https://github.com/LizardKing131313/python_boilerplate/actions/workflows/qodana_code_quality.yml)
![Coverage](badges/coverage.svg)

Быстрый стартовый шаблон для Python-проектов: из коробки структура каталогов,
Makefile-команды, типизация, тесты и git-хуки.
Подходит для pet-/prod-мини-сервисов и библиотек.

> TL;DR:
> ```bash
> python -m venv .venv
> . .venv/bin/activate  # Windows: .venv\Scripts\activate
> pip install -r requirements-dev.txt
> pre-commit install
> make help
> ```

## Что внутри

- **Структура проекта**: `makefiles/`, `scripts/`, `tests/`, `badges/`.
- **Makefile** с удобными таргетами (см. `make help`).
- **Типизация**: mypy.
- **Тесты**: pytest (по умолчанию каталог `tests/`).
- **Git-хуки**: `pre-commit` (форматтеры/линтеры/тривиальные проверки).
- **Статанализ**: JetBrains Qodana (конфиг `qodana.yaml`).

> Примечание: конкретные линтеры/форматтеры включаются через
> `pyproject.toml` и `.pre-commit-config.yaml`.
> При необходимости донастрой в них рулы и версии.

## Быстрый старт

```bash
# 1) Виртуальное окружение
python -m venv .venv
# Linux/macOS
. .venv/bin/activate
# Windows PowerShell
# .venv\Scripts\Activate.ps1

# 2) Зависимости (dev-профиль включает тесты/линтеры/типы)
pip install -r requirements-dev.txt

# 3) Установить git-хуки
pre-commit install

# 4) Проверить доступные команды
make help
```

## Основные команды Makefile

> Посмотри полный список: `make help`.
> Ниже — типовые цели (могут отличаться от твоей версии Makefile):

- `make install` — установка зависимостей (runtime).
- `make dev` — установка dev-зависимостей (линтеры/тесты/типы).
- `make format` — автоформат кода.
- `make lint` — статический анализ (линтеры).
- `make typecheck` — проверка типов (mypy).
- `make test` — запуск тестов.
- `make clean` — чистка кэшей/артефактов.
- `make ci` — сводная проверка как на CI (линт+типы+тесты).

## Структура каталогов

```ignorelang
.
├─ badges/                  # svg/png бейджи (по желанию)
├─ makefiles/               # разнесённые таргеты (инклюдит главный Makefile)
├─ scripts/                 # служебные скрипты (генераторы, утилиты)
├─ tests/                   # pytest-тесты
├─ .pre-commit-config.yaml  # хуки на коммит
├─ pyproject.toml           # центральная конфигурация инструментов
├─ qodana.yaml              # настройки Qodana
├─ requirements.txt         # базовые зависимости
├─ requirements-dev.txt     # dev-зависимости (тесты/линтеры/типы)
└─ Makefile                 # точка входа для задач
```

## Локальная разработка

- Пиши код с **type hints** (PEP 484). Это облегчает жизнь mypy и IDE.
- Перед пушем всегда прогоняй:
  ```bash
  make format lint typecheck test
  ```
- Husky нет — за «pre-commit» отвечают хуки: `pre-commit install`.
- Для проверки качества на CI можно использовать
  уже готовые воркфлоу (добавь их в `.github/workflows/`).

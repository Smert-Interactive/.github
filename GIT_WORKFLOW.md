# Git workflow

DiceBound использует GitHub Flow. `main` — единственная долгоживущая ветка, и
она всегда должна оставаться собираемой. Постоянную ветку `develop` не используем.

## 1. Выбрать или создать Issue

У каждого изменения должен быть GitHub Issue с исполнителем и критериями приёмки.
Исключение — небольшие первоначальные настройки репозитория.

## 2. Создать ветку от `main`

Перед созданием ветки нужно обновить локальную `main`. Используем следующие
префиксы:

| Префикс | Назначение | Пример |
|---|---|---|
| `feature/` | Новая функциональность | `feature/12-health-endpoint` |
| `fix/` | Исправление ошибки | `fix/24-docker-startup` |
| `docs/` | Документация | `docs/31-erd-v1` |
| `refactor/` | Внутреннее изменение кода | `refactor/42-formula-parser` |
| `test/` | Тесты | `test/46-character-service` |
| `chore/` | Инструменты и обслуживание | `chore/50-update-eslint` |
| `ci/` | Настройка CI/CD | `ci/54-backend-checks` |

Имя пишется в lowercase kebab-case. При наличии Issue указываем его номер. После
слияния ветка удаляется.

## 3. Делать коммиты

Сообщения коммитов соответствуют Conventional Commits:

```text
<type>(<scope>): <description>
```

Основные допустимые типы: `feat`, `fix`, `docs`, `refactor`, `test`, `build`,
`ci` и `chore`.

Examples:

```text
feat(backend): add health check endpoint
fix(frontend): handle unavailable API response
docs(erd): add initial database diagram
ci(backend): run lint and tests on pull requests
chore(infra): add Docker Compose configuration
```

Нельзя коммитить секреты, локальные `.env`, результаты сборки, директории
зависимостей и настройки конкретной IDE.

## 4. Открыть Pull Request

- Pull Request открывается в `main`.
- Название соответствует Conventional Commits: после squash merge оно станет
  названием итогового коммита.
- Issue связывается строкой `Closes #<номер>`.
- Один Pull Request решает одну задачу.
- Незаконченное изменение оформляется как Draft Pull Request.
- Изменения API, событий, JSON Schema, UI Schema, миграций и переменных окружения
  отражаются в документации.

## 5. Провести review и слияние

Pull Request готов к слиянию, когда:

- CI-проверки завершились успешно;
- получен минимум один approve от участника команды;
- закрыты все обсуждения review;
- выполнены критерии приёмки;
- обновлена связанная документация;
- отсутствуют секреты и посторонние сгенерированные файлы.

Используем **Squash and merge**. Прямые и принудительные push в `main` запрещены.

## Правила защищённой `main`

В каждом репозитории DiceBound должны действовать следующие правила:

- изменения только через Pull Request;
- один approve со сбросом устаревших одобрений;
- обязательное закрытие всех обсуждений;
- обязательное успешное прохождение CI;
- линейная история и только squash merge;
- запрет force push и удаления ветки;
- правила распространяются и на администраторов репозитория.

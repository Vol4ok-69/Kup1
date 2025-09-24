# Kup1
📋 ОСНОВНЫЕ ПРАВИЛА КОМАНДЫ
1. Модель ветвления (Git Flow)
text
main/master (production)
├── develop (стабильная разработка)
│   ├── feature/новая-фича
│   ├── hotfix/срочный-фикс
│   └── release/версия-1.0
2. Правила именования веток
bash
# Фичи
feature/auth-system
feature/payment-integration

# Багфиксы
fix/login-error
fix/payment-bug

# Хотфиксы
hotfix/critical-security-fix

# Релизы
release/v1.2.0
3. Коммит-конвенции
text
feat: добавить аутентификацию
fix: исправить баг с сессиями
docs: обновить README
style: форматирование кода
refactor: переработка модуля API
test: добавить тесты для юзеров
chore: обновить зависимости
🛠 ОСНОВНЫЕ КОМАНДЫ ДЛЯ КОМАНДЫ
Ежедневный workflow:
bash
# 1. Получить свежие изменения
git fetch origin
git pull origin develop

# 2. Создать ветку для задачи
git checkout -b feature/task-name

# 3. Работать и коммитить
git add .
git commit -m "feat: добавить функционал X"

# 4. Пушить ветку
git push -u origin feature/task-name
Синхронизация с основной веткой:
bash
# Вариант 1: Merge (проще, но грязнее история)
git fetch origin
git merge origin/develop

# Вариант 2: Rebase (чище история, но сложнее)
git fetch origin
git rebase origin/develop
Разрешение конфликтов:
bash
# После конфликта при мерже/ребазе:
git status                    # посмотреть конфликтующие файлы
# Редактируем файлы, убираем <<<<<<<, =======, >>>>>>>
git add .                    # добавляем исправления
git rebase --continue        # или git commit для мержа
🔄 PROCESS PULL REQUEST (Code Review)
Создание PR:
Запушить ветку: git push origin feature/task-name

Создать PR на GitHub из feature → develop

Добавить ревьюверов

Ждать аппрувы

Ревью кода:
bash
# Перед ревью обновить ветку:
git fetch origin
git checkout feature/task-name
git rebase origin/develop

# После замечаний - исправить и обновить PR:
git add .
git commit --amend           # или новый коммит
git push --force-with-lease  # обновить PR
🚨 ЧТО НЕЛЬЗЯ ДЕЛАТЬ В КОМАНДЕ
Запрещенные действия:
bash
# ❌ Никогда не делать в общих ветках!
git push --force origin develop
git push --force origin main

# ❌ Не коммитить в develop/main напрямую
# ❌ Не игнорировать код-ревью
# ❌ Не оставлять мерж-конфликты
В случае проблем:
bash
# Откатить локальные изменения
git reset --hard HEAD

# Откатить конкретный файл
git checkout -- filename.txt

# Восстановить удаленную ветку
git reflog
git checkout -b restored-branch commit-hash
📝 GIT CONFIG ДЛЯ КОМАНДЫ
Глобальные настройки:
bash
git config --global user.name "Ваше Имя"
git config --global user.email "ваш@email.com"
git config --global push.default simple
git config --global pull.rebase false  # или true для rebase по умолчанию

# Полезные алиасы
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.unstage 'reset HEAD --'
🎯 BEST PRACTICES
1. Частые маленькие коммиты
bash
# Хорошо:
feat: добавить валидацию email
fix: исправить баг с кодировкой

# Плохо:
feat: добавить всю авторизацию + фиксы багов + рефакторинг
2. Перед пуллом всегда обновляться
bash
git fetch origin
git rebase origin/develop  # или git merge origin/develop
3. Тестировать перед пушем
bash
# Запустить тесты
npm test
# Проверить линтер
npm run lint
4. Использовать .gitignore
text
# Пример для Node.js
node_modules/
.env
*.log
dist/
🆘 ЧТО ДЕЛАТЬ ЕСЛИ ВСЁ СЛОМАЛ?
Экстренные команды:
bash
# Отменить последний коммит (если не запушен)
git reset --soft HEAD~1

# Откатить до конкретного коммита
git reset --hard commit-hash

# Создать ветку с спасительного коммита
git checkout -b rescue-branch commit-hash
🔧 ПОЛЕЗНЫЕ СКРИПТЫ ДЛЯ КОМАНДЫ
pre-push hook (.git/hooks/pre-push):
bash
#!/bin/bash
# Запретить пуш в develop/main
current_branch=$(git symbolic-ref --short HEAD)
protected_branches=("main" "develop")

for branch in "${protected_branches[@]}"; do
    if [ "$current_branch" = "$branch" ]; then
        echo "❌ Запрещено пушить в $branch!"
        echo "Создайте feature-ветку"
        exit 1
    fi
done
Этот гайд покрывает 95% рабочих ситуаций в команде! Есть вопросы по конкретным сценариям? 🚀


# Report Jira Tasks
Выгрузка отчета из группы пользователей Jira Cloud формате .xlsx
***

### Excel файл состоит из листов:
- Выгрузка общего листа задач
- Выгрузка задач отдельных пользователей (по листам) состоящих в группе jira

### Excel файл состоит из таблицы c колонки:

- `Ключ`
- `№ задачи`
- `URL задачи`
- `Название задачи`
- `Тип задачи`
- `Статус задачи`
- `Автор`
- `Исполнитель`
- `Задача Создана`
- `Задача Закрыта`

### 1. Создать группу
Создать группу пользователей в jira по которым делать выгрузку задач:
- Откройте панель администрации https://admin.atlassian.com/
- Перейдите в раздел: **Groups** -> **Create group**
- Укажите название группы например: "**My Group**"
- Добавьте пользователей в группу.

### 2. Настройка поумолчанию параметров (флагов) утилиты
1) Откройте файл `cmd/app/main.go`
2) Отредактируйте параметры в переменной `var paramDefault`
    
   1) `Host`: URL Jira Cloud
   2) `Token`: Чтобы создать свой токен https://id.atlassian.com/manage/api-tokens
   3) `UserName`: `Логин` от учетной записи с которого был с генерирован `Token`
   4) `Group`: Название группы (Которую создали) в Jira.
   5) `Status`: Статусы задач. (Можно перечислять через запятую)
   
**Совет**: Переменные `Token` и `UserName` - лучше оставить пустыми`""` в целях безопасности. Указывайте их при запуске 
программы например: - `go run cmd/app/main.go --user=Почта_Пользователя --token=Токен`

### 3. Описание флагов:

- `--help` Подробное описания парметров (Обязательно к просмотру)
- `--date_start` Начальная дата запроса. Формат: YYYY-MM-DD `Default`: `Сегоднешний день 00:00`
- `--date_end` Конечная дата запроса Формат: YYYY-MM-DD. `Default`: `Сегоднешний день 23:59`
- `--group` Название группы в Jira. Список пользователей. `Default`: `My Group`
- `--host` Хост Jira Cloud. `Default`: `https://myserver.atlassian.net`
- `--status` Статус задачи. `Default`: `Done`
- `--token` Токен
- `--user` Логин пользователя

**Заметка**: Значения `Default` могут различаться из-за пункта _2._

### 4. Запуск утилиты "Выгрузка отчета за сегодня":

```
go run cmd/app/main.go --user=Почта_Пользователя --token=Токен`
```

### 5. Запуск утилиты "Выгрузка отчета за конкретный период":

```
go run cmd/app/main.go --user=Почта_Пользователя --token=Токен --date_start=2022-10-01 --date_end=2022-10-31`
```
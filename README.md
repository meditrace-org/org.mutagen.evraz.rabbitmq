# Брокер для общения бэкенда с процессингом

## Очередь `uploaded_to_review`

Очередь `uploaded_to_review` используется для хранения информации о проектах, которые необходимо отревьюить. Каждое сообщение в очереди содержит следующие данные:

- **request_id** (uuid): Уникальный идентификатор запроса
- **target_file_url** (строка): Ссылка на файл или архив, который необходимо проанализировать
- **instructions_file_url** (строка): Ссылка на pdf-файл с инструкциями - правилами проекта
- **last_modified_dttm** (строка или `null`): Дата последнего изменения проекта в формате ISO. Если не указано (`null`), то дата определяется из метаданных файлов проекта
- **status** (строка): Статус

### Пример сообщения:

```json
{
  "request_id": "65a2dd0d-dc56-49ee-9e33-5e1a97c36b4e",
  "target_file_url": "http://mutagen.org/files/projects/project.zip",
  "instructions_file_url": "http://mutagen.org/files/projects/instructions.pdf",
  "last_modified_dttm": "2024-10-10T12:30:00+03:00",
  "status": "received"
}

```

## Очередь `review_results`

Очередь `review_results` используется для хранения результатов ревью. Каждое сообщение в очереди содержит следующие данные:

- **request_id** (uuid): Уникальный идентификатор запроса
- **report_content** (строка): Текст отчета в формате markdown
- **status** (строка): Статус

### Пример сообщения:

```json
{
  "request_id": "65a2dd0d-dc56-49ee-9e33-5e1a97c36b4e",
  "report_content": "# Пример отчета: <...>",
  "status": "success"
}
```
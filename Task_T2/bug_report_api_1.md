# Баг-репорт 1. API. Отличие кода ответа от ожидаемого.

## Описание:
При попытке создания папки по уже существующему пути, приходит ответ от сервера с кодом 409.
## Предусловия:
- Используется действительный OAuth-токен
- Уже создана папка с путём disk:/tmp_folder
## Шаги воспроизведения
1. Выполнить запрос:PUT https://cloud-api.yandex.net:443/v1/disk/resources?path=tmp_folder
## Ожидаемый результат
При попытке создания папки по уже существующему пути получен ответ 400
## Фактический результат
Получен ответ с кодом 409 и телом ответа:
{
"error": "DiskPathPointsToExistentDirectoryError",
"description": "Specified path \"tmp_folder\" points to existent directory.",
"message": "По указанному пути \"tmp_folder\" уже существует папка с таким именем."
}

## Окружение
Postman 12.0.1;
Браузер: Google Chrome. Версия: 146.0.7680.153 (официальная сборка) (arm64)

## Серьёзность
Trivial

## Вложения
![img.png](/Task_T2/assets/bug_report_api_1.png)
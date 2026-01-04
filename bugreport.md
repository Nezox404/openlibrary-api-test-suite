# BUGREPORTS — OpenLibrary API

---

## BUG-01

**ID / Номер:** BUG-01  

**Название (Summary):** 500 Internal Server Error при использовании спецсимволов в параметре q  

**Описание (Description):**  
При передаче спецсимволов в параметре запроса q эндпоинт поиска возвращает внутреннюю ошибку сервера.  
Ошибка приводит к падению Python-бэкенда и утечке stacktrace в ответе.

**Шаги воспроизведения (Steps to Reproduce):**  
1. Отправить GET-запрос на эндпоинт поиска.  
2. В параметре q указать строку со спецсимволами: @#$%^&  
3. Получить ответ сервера.

**Ожидаемый результат (Expected Result):**  
- HTTP 200 OK  
- Валидный JSON-ответ с результатами поиска или пустым массивом.

**Фактический результат (Actual Result):**  
- HTTP 500 Internal Server Error  
- HTML-страница с stacktrace  
- Сообщение об ошибке: TypeError: conversion from NoneType to Decimal

**Приоритет (Priority):** Medium  

**Серьёзность (Severity):** High  

**Окружение (Environment):**  
- API: OpenLibrary Search API  
- Эндпоинт: GET /search.json  
- Параметры: q=@#$%^&  
- Серверная часть: Python backend

**Прикреплённые файлы (Attachments):**  
Отсутствуют

**Статус (Status):** New  

---

## BUG-02

**ID / Номер:** BUG-02  

**Название (Summary):** Возврат 422 при длине параметра q менее 3 символов  

**Описание (Description):**  
При передаче строки длиной менее 3 символов в параметре q API возвращает ошибку 422,  
при этом данное ограничение не описано в спецификации.

**Шаги воспроизведения (Steps to Reproduce):**  
1. Отправить GET-запрос на эндпоинт поиска.  
2. В параметре q указать строку из одного символа, например: a  
3. Получить ответ сервера.

**Ожидаемый результат (Expected Result):**  
- HTTP 200 OK  
- Корректный JSON-ответ.

**Фактический результат (Actual Result):**  
- HTTP 422 Unprocessable Entity  
- Сообщение об ошибке: Query too short, must be at least 3 characters

**Приоритет (Priority):** Low  

**Серьёзность (Severity):** Low  

**Окружение (Environment):**  
- API: OpenLibrary Search API  
- Эндпоинт: GET /search.json  
- Параметры: q=a

**Прикреплённые файлы (Attachments):**  
Отсутствуют

**Статус (Status):** New  





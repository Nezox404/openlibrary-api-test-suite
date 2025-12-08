# BUGREPORTS — OpenLibrary API
Источник: bugreport.txt :contentReference[oaicite:0]{index=0}

---

## BUG-01 — 500 Internal Error на спецсимволах в параметре q
Эндпоинт:  
GET /search.json?q=@#$%^&

### Ожидаемо
- 200 OK  
- валидный JSON

### Фактически
- 500 Internal Server Error  
- HTML + stacktrace  
- Ошибка: "TypeError: conversion from NoneType to Decimal"

**Severity:** High  
**Priority:** Medium  
**Тип дефекта:** Input Validation / API Stability  

**Описание:**  
Спецсимволы вызывают некорректную выборку данных и падение Python-бэкенда.

---

## BUG-02 — Несоответствие ожиданий: длина q < 3 → 422
Эндпоинт:  
GET /search.json?q=a

### Ожидаемо
- 200 OK

### Фактически
- 422 Unprocessable Entity  
- Error: "Query too short, must be at least 3 characters"

**Severity:** Low  
**Тип дефекта:** Undocumented Feature / API Specification Gap

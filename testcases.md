# TEST CASES — OpenLibrary API Testing
## Объект тестирования
Публичный API OpenLibrary:
https://openlibrary.org/dev/docs/api/search

## Методика
Использованы техники тест-дизайна:
- Equivalence Classes
- Boundary Value Analysis (BVA)
- Negative Testing
- Security Testing (XSS, SQLi, Path Traversal)
- Rate Limiting
- Functional Testing

---

## TC-FUNC-01 — Позитивная функциональность (базовый поиск)
Метод: GET  
URL: /search.json?q=harry+potter  
Ожидаемо:
- 200 OK  
- JSON содержит ключи numFound, docs  
- docs — не пустой  

---

## TC-EQ-01 — Класс эквивалентности: валидная строка
Метод: GET  
URL: /search.json?q=tolkien  
Ожидаемо:
- 200 OK  
- docs > 0

---

## TC-EQ-02 — Класс эквивалентности: несуществующий поисковый запрос
Метод: GET  
URL: /search.json?q=zxqwyplmno  
Ожидаемо:
- 200 OK  
- docs пуст или почти пуст  
- ошибок нет

---

## TC-EQ-03 — Пустой параметр q
Метод: GET  
URL: /search.json?q=  
Ожидаемо:
- 200 OK  
- docs пуст или numFound = 0

---

## TC-EQ-04 — Спецсимволы в q
Метод: GET  
URL: /search.json?q=@#$%^&  
Ожидаемо:
- 200 OK  
- валидный JSON  
- API не падает

---

## TC-EQ-05 — Unicode
Метод: GET  
URL: /search.json?q=гарри+поттер  
Ожидаемо:
- 200 OK  
- корректная обработка Unicode

---

# BVA — тестирование границ

## TC-BVA-01 — q длиной 1 символ
Метод: GET  
URL: /search.json?q=a  
Ожидаемо: 200 OK

## TC-BVA-02 — q длиной 255 символов
Метод: GET  
URL: /search.json?q=aaaa...(255)  
Ожидаемо: 200 OK

## TC-BVA-03 — q длиной 256 символов
Метод: GET  
URL: /search.json?q=aaaa...(256)  
Ожидаемо: 200 OK или увеличенная задержка

## TC-BVA-04 — q длиной 5000 символов
Метод: GET  
URL: /search.json?q=aaaa...(5000)  
Ожидаемо:
- 200 OK или
- 414 Request-URI Too Long или
- 400 Bad Request  
Недопустимо:
- 500 Internal Server Error  
- HTML-ответ  
- stacktrace  

---

# NEGATIVE TESTING

## TC-NEG-01 — Отсутствие параметра q
Метод: GET  
URL: /search.json  
Ожидаемо: 200 OK

## TC-NEG-02 — Некорректный путь
Метод: GET  
URL: /searchzzz.json?q=harry  
Ожидаемо: 404 Not Found

## TC-NEG-03 — Неверный HTTP метод
Метод: POST  
URL: /search.json?q=harry  
Ожидаемо: 405 Method Not Allowed  
Допустимо: интерпретация как GET

---

# SECURITY TESTING

## TC-SEC-01 — SQL Injection
Метод: GET  
URL: /search.json?q='1'='1  
Ожидаемо:
- 200 или 400  
- JSON валидный  
- нет SQL ошибок  

---

## TC-SEC-02 — XSS Injection
Метод: GET  
URL: /search.json?q=<script>alert(1)</script>  
Ожидаемо:
- JSON  
- нет HTML  
- нет выполнения JS

---

## TC-SEC-03 — Path Traversal
Метод: GET  
URL: /isbn/../../../etc/passwd  
Ожидаемо:
- 404 Not Found  
- нет утечки системной информации  

---

# RATE LIMITING

## TC-RATE-01 — 50 последовательных запросов
Метод: GET  
URL: /search.json?q=harry  
Ожидаемо:
- стабильный 200 OK  
или  
- 429 Too Many Requests

---

# ISBN FUNCTIONALITY

## TC-ISBN-01 — Корректный ISBN
Метод: GET  
URL: /isbn/9780439554930.json  
Ожидаемо:
- 200 OK  
- JSON содержит title, isbn_10/isbn_13, works

---

## TC-ISBN-02 — Некорректный ISBN
Метод: GET  
URL: /isbn/ABCDEFG.json  
Ожидаемо:
- 404 Not Found

---

## TC-ISBN-03 — Слишком длинный ISBN
Метод: GET  
URL: /isbn/12345678901234567890.json  
Ожидаемо:
- 404 или 400  
НЕ должно быть:
- 500

# RESULTS — OpenLibrary API Testing  

## TC-FUNC-01  
200 OK — PASSED

## TC-EQ-01  
200 OK — PASSED

## TC-EQ-02  
200 OK, docs пустой — PASSED

## TC-EQ-03  
200 OK — PASSED

## TC-EQ-04 — АНОМАЛИЯ  
500 Internal Server Error → FAILED

## TC-EQ-05  
200 OK — PASSED

---

# BVA RESULTS

## TC-BVA-01 — АНОМАЛИЯ  
422 Unprocessable Entity — EXPECTATION MISMATCH

## TC-BVA-02  
200 OK — PASSED

## TC-BVA-03  
200 OK — PASSED

## TC-BVA-04  
200 OK — PASSED

---

# NEGATIVE TESTING RESULTS

## TC-NEG-01  
200 OK — PASSED

## TC-NEG-02  
404 Not Found — PASSED

## TC-NEG-03  
200 OK — ACCEPTABLE

---

# SECURITY TESTING

## TC-SEC-01 — SQL Injection  
200 OK — PASSED

## TC-SEC-02 — XSS  
JSON возвращает строку, JS не выполняется — PASSED

## TC-SEC-03 — Path Traversal  
400 Bad Request — PASSED

---

# RATE LIMITING
## TC-RATE-01  
200 OK — PASSED

---

# ISBN RESULTS

## TC-ISBN-01  
200 OK — PASSED

## TC-ISBN-02  
404 — PASSED

## TC-ISBN-03  
404 — PASSED



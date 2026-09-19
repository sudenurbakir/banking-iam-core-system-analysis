# Postman API Test Cases

## 1. Postman Nedir?

Postman, API'lere istek göndermek, dönen cevapları incelemek ve API davranışlarını test etmek için kullanılan bir araçtır.

Business Analyst açısından Postman özellikle;

* API request/response kontrolü,
* Alanların doğru gönderilip gönderilmediğinin incelenmesi,
* Başarılı ve hatalı senaryoların kontrol edilmesi,
* Test senaryolarının oluşturulması

için kullanılabilir.

BA'nın burada API geliştirmesi gerekmez.

Temel olarak:

```text
Request
   ↓
API
   ↓
Response
   ↓
Beklenen sonuç ile karşılaştırma
```

---

## 2. Postman'da Neye Bakılır?

Bir API isteğini test ederken temel olarak şu bilgiler incelenir:

| Alan        | Açıklama                       |
| ----------- | ------------------------------ |
| Method      | GET, POST, PUT, PATCH, DELETE  |
| URL         | API endpoint'i                 |
| Headers     | İstekle gönderilen ek bilgiler |
| Body        | API'ye gönderilen veri         |
| Response    | API'nin döndürdüğü cevap       |
| Status Code | İşlemin HTTP sonucu            |

---

## 3. Örnek API

Projemizde erişim talebi oluşturmak için:

```text
POST /api/access-requests
```

kullanıldığını varsayalım.

### Request Body

```json id="g4sl1k"
{
  "employeeId": "EMP001",
  "system": "CORE_BANKING",
  "role": "CREDIT_OPERATIONS_USER",
  "accessLevel": "TRANSACTION",
  "reason": "Credit operations tasks"
}
```

### Beklenen Response

```json id="f8l1x2"
{
  "requestId": "IAM-1001",
  "status": "PENDING_APPROVAL"
}
```

### Beklenen Status Code

```text
201 Created
```

Bu durumda test başarılı kabul edilir.

---

# 4. API Test Senaryoları

## TC-API-001 – Geçerli Erişim Talebi

**Amaç:** Geçerli bilgilerle erişim talebi oluşturulabildiğini kontrol etmek.

**Method:**

```text
POST
```

**Endpoint:**

```text
/api/access-requests
```

**Request:**

```json id="o0g2cb"
{
  "employeeId": "EMP001",
  "system": "CORE_BANKING",
  "role": "CREDIT_OPERATIONS_USER",
  "accessLevel": "TRANSACTION",
  "reason": "Credit operations tasks"
}
```

**Beklenen sonuç:**

* HTTP Status: `201 Created`
* `requestId` oluşturulmalı.
* Status: `PENDING_APPROVAL` olmalı.

---

## TC-API-002 – Zorunlu Alan Eksik

**Amaç:** Zorunlu alanlardan biri gönderilmediğinde sistemin doğru hata vermesini kontrol etmek.

Request:

```json id="1q1c5q"
{
  "employeeId": "EMP001",
  "system": "CORE_BANKING",
  "accessLevel": "TRANSACTION"
}
```

Burada `role` alanı eksiktir.

**Beklenen sonuç:**

* HTTP Status: `400 Bad Request`
* Hata mesajı dönmeli.
* Erişim talebi oluşturulmamalı.

---

## TC-API-003 – Yetkisiz İşlem

**Amaç:** Yetkisi olmayan kullanıcının API üzerinden işlem yapamamasını kontrol etmek.

**Beklenen sonuç:**

```text
403 Forbidden
```

Sistem erişim talebini oluşturmamalıdır.

---

## TC-API-004 – Talep Bulunamadı

**Amaç:** Olmayan bir request ID ile sorgulama yapıldığında doğru hata alınmasını kontrol etmek.

**Request:**

```text
GET /api/access-requests/IAM-9999
```

**Beklenen sonuç:**

```text
404 Not Found
```

Sistem talebin bulunamadığını belirtmelidir.

---

## TC-API-005 – Sunucu Hatası

**Amaç:** Sistem tarafında beklenmeyen bir hata oluştuğunda uygun response döndüğünü kontrol etmek.

**Beklenen sonuç:**

```text
500 Internal Server Error
```

Ayrıca:

* Hata loglanmalı.
* İlgili teknik ekibin bilgilendirilmesi sağlanmalı.
* Kullanıcıya uygun hata mesajı gösterilmeli.

---

# 5. API Test Case Tablosu

| Test ID    | Senaryo            | Method | Beklenen Status | Beklenen Sonuç          |
| ---------- | ------------------ | ------ | --------------- | ----------------------- |
| TC-API-001 | Geçerli talep      | POST   | 201             | Talep oluşturulur       |
| TC-API-002 | Zorunlu alan eksik | POST   | 400             | Talep oluşturulmaz      |
| TC-API-003 | Yetkisiz işlem     | POST   | 403             | İşlem reddedilir        |
| TC-API-004 | Talep bulunamadı   | GET    | 404             | Talep bulunamadı mesajı |
| TC-API-005 | Sunucu hatası      | POST   | 500             | Hata yönetilir          |

---

# 6. Postman'da Örnek Test Akışı

Gerçek bir API ortamı mevcut olduğunda Postman üzerinden:

### 1. Method seçilir

```text
POST
```

### 2. Endpoint girilir

```text
https://example-bank-api/access-requests
```

### 3. Body seçilir

`raw → JSON`

ve request body girilir.

### 4. Request gönderilir

**Send** butonuna basılır.

### 5. Response incelenir

Örneğin:

```json id="8d0vby"
{
  "requestId": "IAM-1001",
  "status": "PENDING_APPROVAL"
}
```

### 6. Beklenen sonuçla karşılaştırılır

Beklenen:

```text
201 Created
status = PENDING_APPROVAL
```

Gerçek sonuç aynıysa test başarılıdır.

---

# 7. BA Açısından Postman Kullanımı

* API doğru endpoint'e mi gidiyor?
* Gerekli alanlar gönderiliyor mu?
* Response beklenen yapıda mı?
* Hata durumunda doğru response geliyor mu?
* Business kuralı API tarafında uygulanıyor mu?
* Yetkisiz kullanıcı işlem yapabiliyor mu?

Örneğin business rule:

> Yönetici onayı olmadan erişim tanımlanmamalıdır.

API üzerinden erişim tanımlama isteği gönderildiğinde sistem onay kontrolü yapmalıdır.

Eğer onaysız bir talep için:

```text
201 Created
```

dönüyorsa, BA bunun bir **business rule / requirement ihlali** olabileceğini fark edip ilgili ekiple inceleyebilir.

---

# 8. Postman ve Test Case İlişkisi

API testleri de genel test sürecinin bir parçasıdır.

Örneğin:

```text
Requirement
     ↓
API Requirement
     ↓
API Test Scenario
     ↓
Postman Request
     ↓
Response
     ↓
Expected vs Actual
```

Örnek:

**Requirement:**

> Onaylanmış erişim talepleri Core Banking'e gönderilmelidir.

↓

**API Request:**

```text
POST /api/access-requests
```

↓

**Expected:**

```text
201 Created
```

↓

**Response:**

```json
{
  "status": "PENDING_APPROVAL"
}
```

Bu zincir sayesinde gereksinimin teknik tarafta nasıl kontrol edileceği belirlenmiş olur.

---

# 9. BA İçin Önemli Nokta

Bu projede Postman kullanımını **“API developer” seviyesi olarak değil, BA / System Analyst perspektifiyle** ele alıyoruz.

Bilmen gereken temel yapı:

**Method → Endpoint → Request → Response → Status Code → Expected Result**


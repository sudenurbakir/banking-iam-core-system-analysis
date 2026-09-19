# REST API Analysis

## 1. API Nedir?

API (Application Programming Interface), farklı yazılım sistemlerinin birbiriyle iletişim kurmasını sağlayan arayüzdür.

Bu projede IAM sistemi ile Core Banking sisteminin birbiriyle iletişim kurması için API kullanıldığı varsayılmıştır.

Örneğin:

**IAM → Core Banking**

> "EMP001 kullanıcısına CREDIT_OPERATIONS_USER rolünü tanımla."

Core Banking bu isteği işler ve IAM'e bir cevap döner.

---

## 2. REST API Nedir?

REST (Representational State Transfer), web tabanlı API'lerde yaygın olarak kullanılan bir mimari yaklaşımdır.

REST API'lerde genellikle HTTP protokolü kullanılır.

En sık karşılaşılan HTTP methodları:

| Method | Temel kullanım          | Örnek                      |
| ------ | ----------------------- | -------------------------- |
| GET    | Veri görüntüleme        | Erişim talebini getir      |
| POST   | Yeni kayıt oluşturma    | Yeni erişim talebi oluştur |
| PUT    | Mevcut kaydı güncelleme | Talebi güncelle            |
| PATCH  | Kısmi güncelleme        | Talep durumunu değiştir    |
| DELETE | Kayıt silme             | Erişim talebini kaldır     |

BA açısından methodların teknik detayından çok **hangi iş ihtiyacında hangi işlemin yapılacağını** anlamak önemlidir.

---

## 3. Endpoint Nedir?

Endpoint, API üzerinden belirli bir işlemin gerçekleştirildiği adrestir.

Örneğin:

```text
POST /api/access-requests
```

Burada:

**POST**

→ Yeni bir kayıt oluşturulacağını belirtir.

**/api/access-requests**

→ Erişim talepleriyle ilgili endpoint'i temsil eder.

Yani bu endpoint'in anlamı:

> "Yeni bir erişim talebi oluştur."

Başka örnekler:

```text
GET /api/access-requests/IAM-1001
```

> IAM-1001 numaralı talebi getir.

```text
PATCH /api/access-requests/IAM-1001
```

> IAM-1001 numaralı talebin belirli bilgilerini güncelle.

---

## 4. Request Nedir?

Request, bir sisteme gönderilen istektir.

Örneğin IAM, Core Banking'e erişim tanımlama isteği gönderebilir.

### Request

```json
{
  "employeeId": "EMP001",
  "system": "CORE_BANKING",
  "role": "CREDIT_OPERATIONS_USER",
  "accessLevel": "TRANSACTION"
}
```

Bu verinin anlamı:

* Çalışan: EMP001
* Sistem: Core Banking
* Rol: Credit Operations User
* Erişim seviyesi: Transaction

BA burada şu soruları sorar:

* Hangi alanlar zorunlu?
* Hangi alanlar opsiyonel?
* Alanların veri tipi nedir?
* Hangi değerler kabul edilir?
* Eksik veya hatalı veri gönderilirse ne olur?

---

## 5. Response Nedir?

Response, API'ye gönderilen request'in karşılığında sistemin verdiği cevaptır.

### Başarılı Response

```json
{
  "requestId": "IAM-1001",
  "status": "SUCCESS"
}
```

Bu response:

> İşlemin başarılı olduğunu gösterir.

### Hatalı Response

```json
{
  "requestId": "IAM-1001",
  "status": "ERROR",
  "errorCode": "CB-403",
  "message": "Access could not be created"
}
```

Bu durumda BA olarak hata davranışının ne olması gerektiğini analiz ederiz.

Örneğin:

* Hata loglanacak mı?
* Kullanıcı bilgilendirilecek mi?
* İşlem tekrar denenecek mi?
* IT ekibine bildirim gidecek mi?

---

## 6. HTTP Status Code

API response'larında HTTP status code kullanılır.

BA'nın başlangıç seviyesinde bilmesi gerekenler:

| Kod | Anlam                 | Örnek                             |
| --- | --------------------- | --------------------------------- |
| 200 | Başarılı              | Veri başarıyla getirildi          |
| 201 | Oluşturuldu           | Yeni talep oluşturuldu            |
| 400 | Hatalı istek          | Eksik/hatalı veri gönderildi      |
| 401 | Yetkilendirme gerekli | Kullanıcı doğrulanamadı           |
| 403 | Erişim reddedildi     | Kullanıcının işlem yetkisi yok    |
| 404 | Bulunamadı            | Talep bulunamadı                  |
| 500 | Sunucu hatası         | Sistem tarafında beklenmeyen hata |

Örneğin:

```text
POST /api/access-requests
Response: 201 Created
```

şunu ifade eder:

> Erişim talebi başarıyla oluşturuldu.

---

## 7. Bu Projedeki REST API Örneği

### Access Request Oluşturma

```text
POST /api/access-requests
```

### Request

```json
{
  "employeeId": "EMP001",
  "system": "CORE_BANKING",
  "role": "CREDIT_OPERATIONS_USER",
  "accessLevel": "TRANSACTION",
  "reason": "Credit operations tasks"
}
```

### Response

```json
{
  "requestId": "IAM-1001",
  "status": "PENDING_APPROVAL"
}
```

Bu response sonrasında talep yöneticinin onayına gönderilebilir.

---

## 8. Access Request Görüntüleme

Belirli bir talebin durumunu görüntülemek için:

```text
GET /api/access-requests/IAM-1001
```

Örnek response:

```json
{
  "requestId": "IAM-1001",
  "employeeId": "EMP001",
  "system": "CORE_BANKING",
  "role": "CREDIT_OPERATIONS_USER",
  "status": "APPROVED"
}
```

BA açısından burada önemli olan:

> Çalışan veya yetkili kullanıcı, erişim talebinin mevcut durumunu görebiliyor mu?

---

## 9. Hata Senaryoları

API analizi yalnızca başarılı senaryoyu düşünmemelidir.

### Senaryo 1 – Eksik bilgi

Request içerisinde `role` alanı gönderilmemiş.

Beklenen:

```text
400 Bad Request
```

Sistem:

> "Role is required."

---

### Senaryo 2 – Yetkisiz erişim

Kullanıcının ilgili işlemi yapma yetkisi yok.

Beklenen:

```text
403 Forbidden
```

---

### Senaryo 3 – Talep bulunamadı

Gönderilen request ID sistemde bulunmuyor.

Beklenen:

```text
404 Not Found
```

---

### Senaryo 4 – Sistem hatası

Core Banking sistemi beklenmeyen bir hata döndürüyor.

Beklenen:

```text
500 Internal Server Error
```

Bu durumda sistemin hata logu oluşturması ve ilgili ekibin bilgilendirilmesi gibi gereksinimler tanımlanabilir.

---

## 10. BA API Analizi Kontrol Listesi

Bir API dokümanı incelerken BA olarak şu sorular sorulabilir:

### İşlev

* Bu API ne işe yarıyor?
* Hangi business ihtiyacını karşılıyor?
* Kim kullanacak?

### Request

* Hangi bilgiler gönderilecek?
* Hangi alanlar zorunlu?
* Veri tipleri neler?
* Geçerli değerler neler?

### Response

* Başarılı olduğunda ne dönecek?
* Hangi bilgiler dönecek?
* Hata durumunda ne dönecek?

### Güvenlik

* API'yi kim çağırabilir?
* Authentication nasıl yapılacak?
* Yetkisiz isteklerde ne olacak?

### Hata Yönetimi

* Hangi hatalar oluşabilir?
* Hatalar loglanacak mı?
* İşlem tekrar denenebilir mi?
* Kullanıcı nasıl bilgilendirilecek?

---

## 11. BA'nın Buradaki Rolü

BA'nın REST API konusunda görevi API'yi geliştirmek değildir.

BA;

* Business ihtiyacını belirler,
* API'nin hangi işlem için kullanılacağını tanımlar,
* Request alanlarını analiz eder,
* Response beklentilerini belirler,
* Hata senaryolarını düşünür,
* API gereksinimlerini dokümante eder,
* Geliştirici ve test ekipleriyle bu gereksinimleri paylaşır.

Örneğin:

> **Business ihtiyaç:** Onaylanan erişim talebi Core Banking'e iletilmeli.

BA bunu şu şekilde teknik gereksinime dönüştürebilir:

> **TR-009:** IAM sistemi, onaylanan erişim taleplerini Core Banking sistemine REST API üzerinden iletebilmelidir.

Ardından:

**Technical Requirement → API Request → API Response → Test Case**

şeklinde ilerlenebilir.

---

## 12. Bu Projede REST API'nin Yeri

Projedeki genel yapı:

```text
Employee
    ↓
IAM
    ↓
Manager Approval
    ↓
Role & Policy Check
    ↓
REST API
    ↓
Core Banking
    ↓
Response
    ↓
Audit Log
    ↓
Notification
```

Bu akışta REST API, IAM ile Core Banking arasındaki **sistemler arası iletişim katmanı** olarak ele alınmıştır.

# Technical Requirements

Technical Requirement, sistemin teknik olarak **hangi koşulları sağlaması gerektiğini** tanımlar.

Bu projede teknik gereksinimler; IAM, Core Banking ve diğer sistemler arasındaki iletişim, veri aktarımı ve erişim yönetimi açısından ele alınmıştır.

## Technical Requirements

| ID     | Teknik Gereksinim   | Açıklama                                                                         | Örnek                                                                        |
| ------ | ------------------- | -------------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| TR-001 | Sistem Entegrasyonu | IAM, erişim tanımlamak için ilgili sistemlerle iletişim kurabilmelidir.          | IAM → Core Banking                                                           |
| TR-002 | API Desteği         | Sistemler arasında veri alışverişi için API kullanılabilmelidir.                 | IAM, Core Banking'e erişim isteği gönderebilir.                              |
| TR-003 | SOAP Desteği        | SOAP kullanan sistemlerle iletişim kurulabilmelidir.                             | Eski bir Core Banking servisine SOAP üzerinden erişim talebi gönderilebilir. |
| TR-004 | Kimlik Doğrulama    | API istekleri yetkili sistemler tarafından yapılmalıdır.                         | IAM API isteği gönderirken gerekli authentication bilgilerini kullanır.      |
| TR-005 | Veri Formatı        | Sistemler arasında gönderilen veriler belirlenen veri formatına uygun olmalıdır. | JSON veya XML formatında veri gönderilebilir.                                |
| TR-006 | Hata Yönetimi       | Entegrasyon hataları sistem tarafından yakalanmalı ve kayıt altına alınmalıdır.  | Core Banking cevap vermediğinde hata loglanır.                               |
| TR-007 | Audit Log           | Erişim işlemleri teknik olarak loglanmalıdır.                                    | ACCESS_GRANTED işlemi log kaydına eklenir.                                   |
| TR-008 | Veri Tabanı         | Erişim taleplerinin gerekli bilgileri veritabanında saklanmalıdır.               | Talep ID, kullanıcı ID, sistem ve durum bilgileri tutulur.                   |

---

## 1. API Neden Kullanılıyor?

API'yi basitçe **iki sistemin birbiriyle iletişim kurmasını sağlayan bir arayüz** olarak düşünebiliriz.

Bu projede:

```text 
IAM
 ↓
API
 ↓
Core Banking
```

IAM, Core Banking'e:

> "Bu kullanıcı için şu erişimi tanımla."

şeklinde bir istek gönderebilir.

BA açısından burada önemli olan API'yi kodlamak değil;

* Hangi sistem iletişim kuruyor?
* Hangi bilgi gönderiliyor?
* Hangi cevap bekleniyor?
* Hata olursa ne yapılacak?

sorularını tanımlayabilmektir.

---

## 2. SOAP Neden Kullanılıyor?

SOAP, sistemler arasında mesajlaşma için kullanılan bir web servis yaklaşımıdır.

Özellikle eski veya kurumsal sistemlerde SOAP servisleriyle karşılaşılabilir.

Örneğin:

```text 
IAM
 ↓
SOAP Request
 ↓
Core Banking
 ↓
SOAP Response
```

Burada BA'nın bilmesi gereken temel konu, **SOAP ile de sistemler arasında veri alışverişi yapılabildiğidir.**

Bu projede SOAP'ın teknik implementasyonu yapılmamaktadır.

---

## 3. REST ve SOAP Arasındaki Temel Fark

| REST                             | SOAP                                             |
| -------------------------------- | ------------------------------------------------ |
| Daha hafif ve esnek bir yaklaşım | Daha standart ve kurallı bir yapı                |
| Genellikle JSON kullanılır       | Genellikle XML kullanılır                        |
| HTTP metodları kullanılır        | XML tabanlı mesajlaşma kullanılır                |
| Modern web servislerinde yaygın  | Kurumsal/legacy sistemlerde sık karşılaşılabilir |

Bu projede her ikisinin de bilinmesinin nedeni, iş ilanındaki **REST/SOAP** beklentisini anlamaktır.

---

## 4. Örnek Veri Akışı

Bir erişim talebi Core Banking'e gönderilirken aşağıdaki gibi bilgiler kullanılabilir:

```json
{
  "employeeId": "EMP001",
  "system": "CORE_BANKING",
  "role": "CREDIT_OPERATIONS_USER",
  "accessLevel": "TRANSACTION"
}
```

Core Banking'in cevabı:

```json
{
  "requestId": "IAM-1001",
  "status": "SUCCESS"
}
```

BA olarak burada JSON'un nasıl kodlandığını bilmekten çok, **hangi verinin gönderildiğini ve hangi cevabın beklendiğini** anlayabilmek önemlidir.

---

## 5. Hata Durumu

Entegrasyon sırasında her işlem başarılı olmayabilir.

Örneğin:

```text 
IAM
 ↓
Core Banking
 ↓
Hata
 ↓
IAM hata kaydı oluşturur
 ↓
IT / IAM ekibine bildirim
```

Örneğin Core Banking cevap vermiyorsa sistem:

> `CORE_BANKING_UNAVAILABLE`

gibi bir hata kodu oluşturabilir.

Bu hata daha sonra log analizinde veya test süreçlerinde incelenebilir.

---

## 6. BA Açısından Teknik Requirement

Bir BA'nın teknik requirement yazarken kendisine sorabileceği temel sorular:

* Hangi sistemler entegre olacak?
* Hangi veri gönderilecek?
* Veri hangi formatta olacak?
* İstek nasıl doğrulanacak?
* Başarılı cevap nasıl olacak?
* Hata durumunda ne olacak?
* İşlem loglanacak mı?
* Veritabanında hangi bilgiler tutulacak?

Bu sorular teknik ekip ile yapılacak görüşmelerin temelini oluşturabilir.

---

## 7. Genel Akış

```text 
Business Requirement
        ↓
Functional Requirement
        ↓
Business Rules
        ↓
Technical Requirement
        ↓
Development
        ↓
Testing
        ↓
UAT
```

Bu projede teknik gereksinimlerin amacı **kod yazmak değil**, iş ihtiyacının teknik ekip tarafından uygulanabilmesi için gerekli temel teknik beklentileri açık hale getirmektir.

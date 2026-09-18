# Business Rules

Business Rule, sistemin iş süreçlerinde uyması gereken **kuralları ve karar kriterlerini** tanımlar.

Bu projede business rule'lar, çalışanların sistem erişimlerinin hangi koşullarda verileceğini veya reddedileceğini belirlemek için kullanılmıştır.

## Business Rules

| ID     | İş Kuralı       | Açıklama                                                                                     | Örnek                                                            |
| ------ | --------------- | -------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| BR-001 | Yönetici Onayı  | Erişim tanımlanmadan önce ilgili yöneticinin onayı alınmalıdır.                              | Yönetici onaylamadan Core Banking erişimi verilmez.              |
| BR-002 | Rol Uyumu       | Talep edilen erişim çalışanın görev rolüyle uyumlu olmalıdır.                                | Kredi Operasyon Uzmanı'na kredi operasyon rolü verilebilir.      |
| BR-003 | Yetki Seviyesi  | Kullanıcıya yalnızca ihtiyacı olan yetki seviyesi verilmelidir.                              | Görüntüleme ihtiyacı olan kullanıcıya yönetici yetkisi verilmez. |
| BR-004 | Yetkisiz Erişim | Rol ile uyumsuz erişim talepleri otomatik olarak reddedilmeli veya ek onaya gönderilmelidir. | CRM yetkisi olmayan bir çalışan doğrudan admin rolü alamaz.      |
| BR-005 | Audit Kaydı     | Erişim verme, değiştirme ve kaldırma işlemleri kayıt altına alınmalıdır.                     | Kullanıcıya verilen erişim tarih ve işlem bilgisi loglanır.      |
| BR-006 | Offboarding     | İşten ayrılan çalışanın aktif sistem erişimleri kaldırılmalıdır.                             | Çalışan ayrıldığında Core Banking erişimi kaldırılır.            |
| BR-007 | Talep Takibi    | Her erişim talebinin bir durumu bulunmalıdır.                                                | Beklemede → Onaylandı → Tamamlandı.                              |
| BR-008 | Bildirim        | Talep sonucu çalışana bildirilmelidir.                                                       | Erişim reddedildiğinde kullanıcıya bildirim gönderilir.          |

---

## Business Rule Nasıl Kullanılır?

Business rule'lar sistemin karar mekanizmasını belirler.

Örneğin bir çalışan Core Banking erişimi istediğinde:

```text
Erişim Talebi
      ↓
Yönetici Onayı
      ↓
Rol Kontrolü
      ↓
Yetki Seviyesi Kontrolü
      ↓
Uygun mu?
 ┌────┴────┐
Evet       Hayır
 ↓           ↓
IAM        Red / Ek Onay
 ↓
Erişim
```

Burada sistem yalnızca "erişim talebi oluşturma" fonksiyonunu gerçekleştirmiyor.

Aynı zamanda belirlenen **iş kurallarına göre karar veriyor.**

---

## Requirement ve Business Rule İlişkisi

Bir requirement ile birden fazla business rule ilişkili olabilir.

### Örnek

**FR-004 – Erişim Tanımlama**

> Onaylanan erişim talebi IAM üzerinden ilgili sisteme iletilmelidir.

Bu requirement'ın uygulanmasında:

* BR-001 → Yönetici onayı alınmalı
* BR-002 → Rol uygun olmalı
* BR-003 → Yetki seviyesi uygun olmalı
* BR-004 → Yetkisiz erişim engellenmeli

gibi kurallar dikkate alınır.

Yani:

```text
Requirement
    ↓
Business Rules
    ↓
Sistem Davranışı
```

---

## BA Açısından Neden Önemli?

Business Analyst olarak yalnızca:

> "Kullanıcı erişim talebi oluşturacak."

demek yeterli değildir.

Şu soruların da cevaplanması gerekir:

* Kim onaylayacak?
* Hangi durumda onaylanacak?
* Hangi durumda reddedilecek?
* Kullanıcı hangi role sahip olmalı?
* Hangi yetki seviyesi verilebilir?
* Erişim ne zaman kaldırılmalı?
* Yapılan işlem nasıl takip edilecek?

Bu soruların cevapları business rule'ların oluşmasına yardımcı olur.

---

## Örnek Gereksinim Zinciri

Basit bir örnek üzerinden:

**İhtiyaç:**

> Çalışan görevini yapabilmek için Core Banking sistemine erişmek istiyor.

↓

**Functional Requirement:**

> Sistem çalışanın Core Banking erişim talebi oluşturmasına izin vermelidir.

↓

**Business Rules:**

> Yönetici onayı alınmalıdır.

> Çalışanın rolü erişim için uygun olmalıdır.

> Kullanıcıya gerekli yetki seviyesinden fazlası verilmemelidir.

↓

**User Story:**

> Bir çalışan olarak görevimi yerine getirebilmek için Core Banking erişim talebi oluşturmak istiyorum.

↓

**Acceptance Criteria:**

> Yönetici onayı olmadan erişim tanımlanmamalıdır.

Bu bağlantı, projenin ilerleyen bölümlerinde **User Story → Acceptance Criteria → Testing → UAT** çalışmalarında kullanılacaktır.

# Project Scope

## 1. Amaç

Bu dokümanın amacı, IAM ve Core Banking entegrasyon projesinin kapsamını belirlemek ve proje kapsamında gerçekleştirilecek çalışmalar ile kapsam dışında bırakılan konuları netleştirmektir.

Kapsamın açık şekilde tanımlanması, gereksiz çalışmaların önlenmesine ve stakeholder beklentilerinin yönetilmesine yardımcı olur.

---

## 2. In Scope

Aşağıdaki konular proje kapsamında ele alınacaktır:

### Business Analysis

* Business ihtiyaçlarının analiz edilmesi
* Stakeholder analizi
* Mevcut sürecin (AS-IS) incelenmesi
* Hedef sürecin (TO-BE) oluşturulması
* Proje gereksinimlerinin dokümante edilmesi

### Access Management

* Çalışan erişim talebinin oluşturulması
* Erişim talebinin yönetici tarafından onaylanması
* Kullanıcı rolünün kontrol edilmesi
* Rol bazlı erişim kurallarının uygulanması
* Erişim oluşturma, güncelleme ve kaldırma süreçleri
* İşten ayrılan çalışanların erişimlerinin kapatılması

### System Integration

* IAM ve Core Banking arasındaki entegrasyonun analiz edilmesi
* API iletişimlerinin incelenmesi
* REST ve SOAP servislerinin temel seviyede analiz edilmesi
* Request / response yapılarının dokümante edilmesi
* Entegrasyon hata senaryolarının belirlenmesi

### Database

* Kullanıcı ve erişim bilgilerinin veri modelinin oluşturulması
* Temel SQL sorgularının hazırlanması
* Erişim kayıtlarının analiz edilmesi

### UX / Requirements Visualization

* Erişim talep ekranı için temel mock-up hazırlanması
* Kullanıcı akışlarının görselleştirilmesi
* UML ve process diagramlarının oluşturulması

### Testing & UAT

* Test senaryolarının hazırlanması
* API test senaryolarının oluşturulması
* Business rule testlerinin belirlenmesi
* Bug senaryolarının dokümante edilmesi
* UAT senaryolarının hazırlanması
* Business acceptance kriterlerinin tanımlanması

### Project & Documentation

* Agile backlog yapısının oluşturulması
* Sprint kapsamının örneklenmesi
* Jira workflow'unun modellenmesi
* Confluence benzeri proje dokümantasyon yapısının oluşturulması
* Requirements Traceability Matrix hazırlanması
* Release sürecinin dokümante edilmesi
* Temel IT governance kontrollerinin belirlenmesi

---

## 3. Out of Scope

Aşağıdaki konular bu proje kapsamında ele alınmayacaktır:

* Gerçek bir bankanın sistemlerine erişim
* Gerçek müşteri veya çalışan verilerinin kullanılması
* Gerçek bankacılık işlemlerinin gerçekleştirilmesi
* Gerçek para transferleri
* Gerçek IAM ürününün kurulumu
* IAM altyapısının kodlanması
* Core Banking sisteminin geliştirilmesi
* Gerçek production ortamına deployment
* Gerçek güvenlik açığı testleri
* Gerçek banka entegrasyonlarının kurulması
* Kurumsal kimlik doğrulama altyapısının fiziksel kurulumu

Bu proje eğitim ve portföy amacıyla oluşturulmuş kurgusal bir BA/System Analysis case study'sidir.

---

## 4. Proje Sınırları

Projenin temel sınırı, IAM ve Core Banking sistemlerinin teknik olarak geliştirilmesi yerine bu sistemler arasındaki **iş gereksinimleri, süreçler ve entegrasyon noktalarının analiz edilmesidir.**

Örneğin proje kapsamında:

> IAM sisteminin nasıl kodlandığı

incelenmeyecektir.

Bunun yerine:

> IAM hangi bilgiyi alıyor, hangi kurala göre değerlendiriyor, hangi sisteme hangi bilgiyi gönderiyor ve sonuç nasıl takip ediliyor?

sorularına odaklanılacaktır.

---

## 5. Kapsam Özeti

Projenin kapsamı aşağıdaki akış üzerinden özetlenebilir:

```text 
Employee
   ↓
Access Request
   ↓
Manager Approval
   ↓
Role & Policy Check
   ↓
IAM
   ↓
API / SOAP Integration
   ↓
Core Banking
   ↓
Database
   ↓
Audit Log
   ↓
Notification
```

Bu akışta Business Analyst'in temel görevi, her adımın iş gereksinimini ve sistem davranışını anlamak, dokümante etmek ve ilgili ekiplerle ortak bir anlayış oluşturmaktır.

---

## 6. Scope Change

Proje sırasında kapsam değişikliği ihtiyacı ortaya çıkması durumunda değişikliğin;

1. İş ihtiyacı,
2. Etkilenen gereksinimler,
3. Etkilenen sistemler,
4. Test kapsamı,
5. UAT kapsamı,
6. Zaman ve kaynak ihtiyacı

açısından değerlendirilmesi gerekir.

Kapsam değişiklikleri ilgili stakeholder'larla değerlendirilerek onay sonrasında proje dokümanlarına yansıtılmalıdır.

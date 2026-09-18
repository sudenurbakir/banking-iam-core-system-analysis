# Stakeholder Analysis

## 1. Amaç

Bu dokümanın amacı, IAM ve Core Banking entegrasyon projesinden etkilenen veya proje üzerinde etkisi bulunan stakeholder'ları belirlemek ve beklentilerini analiz etmektir.

Stakeholder analizi, gereksinimlerin doğru kişilerden toplanması ve farklı beklentilerin proje kapsamında yönetilebilmesi açısından önemlidir.

---

## 2. Stakeholder'lar

| Stakeholder                    | Projedeki Rolü                                    | Temel İhtiyacı / Beklentisi                                                              |
| ------------------------------ | ------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| Çalışan                        | Erişim talebinde bulunan kullanıcı                | İhtiyaç duyduğu sistemlere doğru ve zamanında erişebilmek                                |
| Yönetici                       | Erişim talebini onaylayan kişi                    | Çalışanın görevine uygun erişim talep ettiğini doğrulamak                                |
| İnsan Kaynakları               | Çalışan bilgilerinin kaynağı                      | İşe giriş, departman değişikliği ve işten ayrılma bilgilerinin sisteme doğru aktarılması |
| IAM Ekibi                      | Erişim yönetim sisteminden sorumlu teknik ekip    | Kullanıcı ve yetki süreçlerinin doğru çalışması                                          |
| Core Banking Ekibi             | Core Banking sisteminden sorumlu ekip             | IAM üzerinden gelen erişim bilgilerinin doğru şekilde işlenmesi                          |
| Bilgi Güvenliği                | Güvenlik ve erişim politikalarını takip eden ekip | Yetkilerin güvenlik kurallarına uygun olması                                             |
| IT Operations                  | Sistemlerin operasyonel takibinden sorumlu ekip   | Sistemlerin ve entegrasyonların sürdürülebilir şekilde çalışması                         |
| QA / Test Ekibi                | Sistemin test edilmesinden sorumlu ekip           | Gereksinimlerin test edilebilir ve anlaşılır olması                                      |
| Business Analyst               | İş ve teknik ekipler arasında köprü               | Gereksinimleri analiz etmek, dokümante etmek ve ekipler arasında iletişimi desteklemek   |
| Product Owner / Business Owner | İş önceliklerini belirleyen kişi                  | Projenin iş ihtiyacını karşılaması ve önceliklerin doğru yönetilmesi                     |

---

## 3. Stakeholder Beklentileri

### Çalışan

Çalışan, görevini yerine getirebilmek için ihtiyaç duyduğu sistemlere erişebilmek ister.

Temel beklentileri:

* Erişim talebinin kolay oluşturulması
* Talebin durumunun görüntülenebilmesi
* Onaylanan erişimin zamanında tanımlanması
* Gereksiz erişimlerin verilmemesi

---

### Yönetici

Yönetici, çalışanların yalnızca görevleri için gerekli olan erişimleri talep ettiğini kontrol eder.

Temel beklentileri:

* Bekleyen talepleri görebilmek
* Talebi onaylayabilmek veya reddedebilmek
* Talep edilen rol ve erişim hakkında bilgi görebilmek
* Yapılan işlemlerin kayıt altında tutulması

---

### İnsan Kaynakları

İnsan Kaynakları, çalışanların işe giriş, departman değişikliği ve işten ayrılma bilgilerinin doğru şekilde sisteme aktarılmasını bekler.

Örneğin bir çalışan şirketten ayrıldığında, bu bilginin erişim yönetimi sürecini tetiklemesi beklenebilir.

---

### IAM Ekibi

IAM ekibi, kullanıcıların ve rollerin merkezi olarak yönetilmesini sağlar.

Beklentileri:

* Gereksinimlerin açık ve anlaşılır olması
* Rol ve erişim kurallarının net tanımlanması
* Sistem entegrasyonlarının belirlenmiş olması
* Hataların ve işlemlerin takip edilebilir olması

---

### Core Banking Ekibi

Core Banking ekibi, IAM tarafından gönderilen erişim bilgilerinin ilgili sistem tarafından doğru şekilde işlenmesini bekler.

Örneğin:

```text
IAM
 ↓
Access Request
 ↓
Core Banking
 ↓
Role Assignment
```

akışının doğru çalışması gerekir.

---

### Bilgi Güvenliği

Bilgi Güvenliği ekibi, kullanıcıların görevleriyle uyumlu yetkilere sahip olmasını ve erişim işlemlerinin kayıt altında tutulmasını bekler.

Özellikle:

* Yetki kontrolü
* Onay mekanizması
* Audit log
* Erişim değişikliklerinin takip edilmesi

önemlidir.

---

### QA / Test Ekibi

QA ekibinin gereksinimleri test edebilmesi için acceptance criteria ve business rule'ların açık olması gerekir.

Örneğin:

> Yönetici onayı olmadan erişim tanımlanmamalıdır.

şeklinde açık bir kural test senaryosuna dönüştürülebilir.

---

## 4. BA'nın Stakeholder'larla İletişimi

Business Analyst olarak stakeholder'larla iletişim şekli ihtiyaca göre değişebilir.

| Stakeholder        | Kullanılabilecek Teknik / İletişim Yöntemi    |
| ------------------ | --------------------------------------------- |
| Çalışan            | Görüşme, kullanıcı senaryosu                  |
| Yönetici           | Görüşme, süreç analizi                        |
| İnsan Kaynakları   | Gereksinim toplantısı, doküman analizi        |
| IAM Ekibi          | Teknik toplantı, API / entegrasyon analizi    |
| Core Banking Ekibi | Teknik toplantı, sequence diagram             |
| Bilgi Güvenliği    | Gereksinim ve business rule görüşmesi         |
| QA                 | Test case ve acceptance criteria incelemesi   |
| Product Owner      | Backlog refinement, gereksinim toplantısı     |
| IT Operations      | Teknik toplantı, release / operasyon dokümanı |

---

## 5. Stakeholder Önceliklendirme

Stakeholder'ların projeye etkisi ve projeden etkilenme seviyeleri farklı olabilir.

Bu nedenle proje boyunca aşağıdaki gruplandırma kullanılabilir:

| Stakeholder              | Etki   | İlgi   | Yaklaşım                                  |
| ------------------------ | ------ | ------ | ----------------------------------------- |
| Product / Business Owner | Yüksek | Yüksek | Yakın iletişim                            |
| IAM Ekibi                | Yüksek | Yüksek | Yakın iletişim                            |
| Bilgi Güvenliği          | Yüksek | Yüksek | Yakın iletişim                            |
| Core Banking Ekibi       | Yüksek | Yüksek | Yakın iletişim                            |
| QA                       | Orta   | Yüksek | Düzenli iletişim                          |
| İnsan Kaynakları         | Orta   | Orta   | Gereksinim bazlı iletişim                 |
| IT Operations            | Yüksek | Orta   | Süreç bazlı iletişim                      |
| Yönetici                 | Orta   | Yüksek | Onay süreçlerinde iletişim                |
| Çalışan                  | Düşük  | Yüksek | Kullanıcı ihtiyaçları kapsamında iletişim |

---

## 6. BA Perspektifi

Stakeholder analizi sırasında Business Analyst'in temel amacı, farklı ekiplerin ihtiyaçlarını anlamak ve bu ihtiyaçları ortak bir gereksinim yapısında birleştirmektir.

Örneğin:

**Çalışan:**

> “Kredi sistemine erişmem gerekiyor.”

**Yönetici:**

> “Çalışanın görevine uygun olduğunu onaylamam gerekiyor.”

**Bilgi Güvenliği:**

> “Yetki güvenlik kurallarına uygun olmalı.”

**IAM Ekibi:**

> “Rol ve erişim kuralları sistem tarafından uygulanabilir olmalı.”

BA'nın görevi bu farklı ihtiyaçları analiz ederek ortak bir sistem gereksinimine dönüştürmektir.

Örneğin:

> “Çalışan tarafından oluşturulan erişim talebi, çalışanın rolü ve tanımlı erişim kuralları doğrultusunda değerlendirilerek gerekli yönetici onayından sonra IAM sistemi üzerinden ilgili uygulamaya iletilmelidir.”

Bu gereksinim daha sonra business rule, user story, acceptance criteria ve test case'lere dönüştürülebilir.

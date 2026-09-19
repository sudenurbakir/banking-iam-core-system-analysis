# User Stories

User Story, bir kullanıcının sistemden **ne yapmak istediğini ve bunu neden istediğini** anlatır.

Bu projede erişim yönetimi sürecindeki temel ihtiyaçlar user story formatında tanımlanmıştır.

## US-001 – Erişim Talebi Oluşturma

**As a:** Çalışan
**I want:** Sistem erişim talebi oluşturmak
**So that:** Görevimi yerine getirebilmek için gerekli sistemlere erişebileyim.

**İlgili Requirement:** FR-001

### Acceptance Criteria

* Çalışan erişim talep ekranını açabilmelidir.
* Sistem ve rol bilgisi seçilebilmelidir.
* Gerekli bilgiler girildiğinde talep oluşturulabilmelidir.

---

## US-002 – Yönetici Onayı

**As a:** Yönetici
**I want:** Çalışanın erişim talebini incelemek ve onaylamak/reddetmek
**So that:** Çalışanlara yalnızca uygun erişimlerin verilmesini sağlayabileyim.

**İlgili Requirement:** FR-002

### Acceptance Criteria

* Yönetici bekleyen talepleri görebilmelidir.
* Talebi onaylayabilmelidir.
* Talebi reddedebilmelidir.
* İşlem sonucunda talep durumu güncellenmelidir.

---

## US-003 – Rol Kontrolü

**As a:** IAM Sistemi
**I want:** Talep edilen erişimi çalışanın rolüyle karşılaştırmak
**So that:** Uygun olmayan erişimlerin verilmesini engelleyebileyim.

**İlgili Requirement:** FR-003

### Acceptance Criteria

* Çalışanın mevcut rolü kontrol edilmelidir.
* Talep edilen erişim kontrol edilmelidir.
* Erişim uygun değilse sistem talebi engellemelidir veya ek onaya göndermelidir.

---

## US-004 – Erişim Tanımlama

**As a:** IAM Sistemi
**I want:** Onaylanan erişim talebini ilgili sisteme iletmek
**So that:** Çalışanın gerekli sistem erişimi tanımlanabilsin.

**İlgili Requirement:** FR-004

### Acceptance Criteria

* Yönetici onayı olmayan talepler sisteme iletilmemelidir.
* Onaylanan talep ilgili sisteme gönderilmelidir.
* İşlem sonucunun başarılı veya başarısız olduğu takip edilebilmelidir.

---

## US-005 – Talep Durumunu Görüntüleme

**As a:** Çalışan
**I want:** Erişim talebimin durumunu görüntülemek
**So that:** Talebimin hangi aşamada olduğunu takip edebileyim.

**İlgili Requirement:** FR-005

### Acceptance Criteria

* Çalışan kendi taleplerini görüntüleyebilmelidir.
* Talebin güncel durumu gösterilmelidir.
* Örneğin `Beklemede`, `Onaylandı`, `Reddedildi`, `Tamamlandı` gibi durumlar görüntülenebilmelidir.

---

## US-006 – Audit Log

**As a:** Bilgi Güvenliği / IT Ekibi
**I want:** Erişim işlemlerinin kayıt altına alınması
**So that:** Yapılan işlemleri daha sonra takip ve kontrol edebileyim.

**İlgili Requirement:** FR-006

### Acceptance Criteria

* Erişim verme işlemi loglanmalıdır.
* Erişim kaldırma işlemi loglanmalıdır.
* İşlem tarihi ve kullanıcı bilgisi tutulmalıdır.

---

## US-007 – Bildirim

**As a:** Çalışan
**I want:** Erişim talebimin sonucu hakkında bilgilendirilmek
**So that:** Talebimin sonucunu takip edebileyim.

**İlgili Requirement:** FR-007

### Acceptance Criteria

* Talep onaylandığında bildirim gönderilmelidir.
* Talep reddedildiğinde bildirim gönderilmelidir.
* Bildirimde talep sonucu açıkça belirtilmelidir.

---

## US-008 – Erişim Kaldırma

**As a:** IT / IAM Ekibi
**I want:** Çalışanın erişimlerini kaldırmak
**So that:** Artık ihtiyaç duyulmayan erişimlerin aktif kalmasını engelleyebileyim.

**İlgili Requirement:** FR-008

### Acceptance Criteria

* Çalışanın aktif erişimleri görüntülenebilmelidir.
* Erişim kaldırma işlemi gerçekleştirilebilmelidir.
* Kaldırılan erişim audit log'a kaydedilmelidir.

---

# User Story → Acceptance Criteria İlişkisi

User Story bize **kullanıcının ihtiyacını** söyler.

Acceptance Criteria ise bu ihtiyacın **hangi koşullarda karşılanmış sayılacağını** açıklar.

Örneğin:

```text
User Story
    ↓
"Çalışan erişim talebi oluşturmak istiyor."
    ↓
Acceptance Criteria
    ↓
"Gerekli bilgiler girildiğinde talep oluşturulmalı."
```

Bu yapı daha sonra test senaryolarının hazırlanmasında kullanılacaktır.

# Gereksinim İzlenebilirliği

```text
Requirement
    ↓
User Story
    ↓
Acceptance Criteria
    ↓
Test Case
    ↓
UAT
```

Bu bağlantı sayesinde bir gereksinimin geliştirme ve test sürecindeki karşılığı takip edilebilir.

# Functional Requirements

## 1. Amaç

Functional Requirement (FR), sistemin **hangi işlemleri yapması gerektiğini** tanımlar.

Bu projede çalışan erişim yönetimi süreci için temel fonksiyonel gereksinimler aşağıdaki gibidir.

---

## 2. Functional Requirements

| ID     | Gereksinim              | Açıklama                                                                                                           |
| ------ | ----------------------- | ------------------------------------------------------------------------------------------------------------------ |
| FR-001 | Erişim talebi oluşturma | Sistem, çalışanın erişim talebi oluşturmasına izin vermelidir.                                                     |
| FR-002 | Yönetici onayı          | Sistem, erişim talebini yöneticinin onaylamasına veya reddetmesine izin vermelidir.                                |
| FR-003 | Rol kontrolü            | Sistem, talep edilen erişimin çalışanın rolüyle uyumunu kontrol etmelidir.                                         |
| FR-004 | Erişim tanımlama        | Onaylanan erişim talebi IAM üzerinden ilgili sisteme iletilmelidir.                                                |
| FR-005 | Talep durumu            | Sistem, erişim talebinin güncel durumunu göstermelidir.                                                            |
| FR-006 | Audit log               | Sistem, erişim işlemlerini kayıt altına almalıdır.                                                                 |
| FR-007 | Bildirim                | Sistem, talep sonucu hakkında çalışana bildirim göndermelidir.                                                     |
| FR-008 | Erişim kaldırma         | Sistem, işten ayrılan veya erişimi kaldırılması gereken çalışanların erişimlerinin kaldırılmasını desteklemelidir. |

---

### FR-001 – Erişim Talebi Oluşturma

Sistem, çalışanın erişim talebi oluşturmasına izin vermelidir.

**Örnek:**
Çalışan, Core Banking → Kredi Modülü → Görüntüleme erişimi için talep oluşturur.

---

### FR-002 – Yönetici Onayı

Sistem, yöneticinin erişim talebini onaylamasına veya reddetmesine izin vermelidir.

**Örnek:**
Yönetici talebi inceler ve **Onayla** veya **Reddet** seçeneğini kullanır.

---

### FR-003 – Rol Kontrolü

Sistem, talep edilen erişimin çalışanın rolüyle uyumlu olup olmadığını kontrol etmelidir.

**Örnek:**
Kredi Operasyon Uzmanı → Kredi İşlemleri erişimi → Uygun.

---

### FR-004 – Erişim Tanımlama

Onaylanan erişim talebi IAM üzerinden ilgili sisteme iletilmelidir.

**Örnek:**
Yönetici onayından sonra IAM, Core Banking sistemine erişim tanımlama isteği gönderir.

---

### FR-005 – Talep Durumu

Sistem, erişim talebinin güncel durumunu göstermelidir.

**Örnek:**

```text
Talep No: IAM-1001
Durum: Yönetici Onayında
```

---

### FR-006 – Audit Log

Sistem, erişim işlemlerini kayıt altına almalıdır.

**Örnek:**

```text
Kullanıcı: EMP001
İşlem: ACCESS_GRANTED
Sistem: Core Banking
Tarih: 18.09.2026
```

---

### FR-007 – Bildirim

Sistem, talep sonucu hakkında çalışana bildirim göndermelidir.

**Örnek:**
“Core Banking erişim talebiniz onaylanmıştır.”

---

### FR-008 – Erişim Kaldırma

Sistem, çalışanın erişimlerinin kaldırılmasını desteklemelidir.

**Örnek:**
Çalışanın işten ayrılması durumunda aktif sistem erişimleri kaldırılır.

---

## Gereksinim Akışı

```text
FR
↓
Business Rule
↓
User Story
↓
Acceptance Criteria
↓
Test Case
↓
UAT
```

Bu yapı sayesinde bir gereksinimin geliştirme ve test süreçlerinde takip edilmesi sağlanır.


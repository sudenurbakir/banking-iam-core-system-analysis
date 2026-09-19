# Screen Requirements

Bu doküman, erişim talebi ekranının hangi alanları içereceğini ve kullanıcı işlemlerine nasıl cevap vereceğini tanımlar.

## 1. Ekran Alanları

| ID      | Alan             | Gereksinim                                                 | Zorunlu |
| ------- | ---------------- | ---------------------------------------------------------- | ------- |
| SCR-001 | Çalışan          | Sistem çalışan bilgisini göstermelidir.                    | Evet    |
| SCR-002 | Sistem           | Kullanıcı erişim istenen sistemi seçebilmelidir.           | Evet    |
| SCR-003 | Rol              | Kullanıcı uygun rolü seçebilmelidir.                       | Evet    |
| SCR-004 | Erişim Seviyesi  | Kullanıcı erişim seviyesini seçebilmelidir.                | Evet    |
| SCR-005 | Talep Nedeni     | Kullanıcı erişim nedenini girebilmelidir.                  | Evet    |
| SCR-006 | Başlangıç Tarihi | Kullanıcı erişimin başlangıç tarihini belirleyebilmelidir. | Evet    |
| SCR-007 | Talebi Gönder    | Kullanıcı doldurduğu talebi gönderebilmelidir.             | Evet    |

---

## 2. Ekran Davranışları

### SCR-008 – Zorunlu Alan Kontrolü

Zorunlu alanlardan biri boş bırakılırsa sistem talebin gönderilmesine izin vermemelidir.

**Örnek:**

```text
Sistem: [ Core Banking ✓ ]
Rol:   [                ]

→ "Rol alanı zorunludur."
```

---

### SCR-009 – Başarılı Talep

Tüm gerekli bilgiler doğru girildiğinde sistem talebi oluşturmalıdır.

**Örnek:**

```text
[ Talebi Gönder ]

→ "Erişim talebiniz oluşturuldu.
   Talep No: IAM-1001"
```

---

### SCR-010 – Talep Durumu

Talep oluşturulduktan sonra başlangıç durumu gösterilmelidir.

**Örnek:**

```text
Talep No: IAM-1001
Durum: Yönetici Onayında
```

---

### SCR-011 – Uygunsuz Rol

Seçilen rol çalışanın mevcut görevine uygun değilse sistem talebi engellemeli veya ek onay sürecine yönlendirmelidir.

**Örnek:**

```text
Çalışan Rolü:
Kredi Operasyon Uzmanı

Talep Edilen Rol:
System Administrator

→ Uygunluk kontrolü başarısız.
```

---

## 3. Hata Mesajları

Sistem kullanıcıya teknik ve anlaşılması zor hata mesajları yerine açıklayıcı mesajlar göstermelidir.

| Durum              | Mesaj                                               |
| ------------------ | --------------------------------------------------- |
| Eksik alan         | "Lütfen zorunlu alanları doldurun."                 |
| Sistem hatası      | "İşlem gerçekleştirilemedi. Lütfen tekrar deneyin." |
| Yetkisiz işlem     | "Bu işlem için yetkiniz bulunmamaktadır."           |
| Entegrasyon hatası | "Erişim tanımlama işlemi tamamlanamadı."            |

---

## 4. BA Açısından Ekran Gereksinimleri

* Hangi alanlar olmalı?
* Hangileri zorunlu?
* Kullanıcı hangi seçenekleri seçebilir?
* Yanlış bilgi girilirse ne olacak?
* Başarılı işlemde ne gösterilecek?
* Hata durumunda ne gösterilecek?
* Kullanıcının yetkisi yoksa ne olacak?

Bu bilgiler daha sonra **development ve testing** ekipleri tarafından kullanılabilir.

---

## 5. Mock-up → Requirement → Test İlişkisi

```text
Mock-up
   ↓
Screen Requirement
   ↓
User Story
   ↓
Acceptance Criteria
   ↓
Test Case
```

Örneğin:

**Screen Requirement:**
Rol alanı zorunludur.

**Acceptance Criteria:**
Rol seçilmeden talep gönderilemez.

**Test Case:**
Rol alanı boş bırakılarak "Talebi Gönder" butonuna basılır.

**Expected Result:**
Sistem hata mesajı gösterir ve talep oluşturmaz.

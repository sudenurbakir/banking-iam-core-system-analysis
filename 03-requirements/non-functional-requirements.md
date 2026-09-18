# Non-Functional Requirements

Non-Functional Requirement (NFR), sistemin fonksiyonlarını yerine getirirken sahip olması gereken **kalite ve performans özelliklerini** tanımlar.

| ID      | Gereksinim        | Açıklama                                                                      | Kısa Örnek                                                                     |
| ------- | ----------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------ |
| NFR-001 | Performans        | Sistem işlemleri kabul edilebilir sürede tamamlamalıdır.                      | Erişim talebi gönderildiğinde kullanıcı uzun süre beklememelidir.              |
| NFR-002 | Güvenlik          | Erişim işlemleri yalnızca yetkili kullanıcılar tarafından yapılabilmelidir.   | Bir çalışan başka bir çalışanın talebini onaylayamamalıdır.                    |
| NFR-003 | Kullanılabilirlik | Erişim talep ekranı kolay anlaşılabilir olmalıdır.                            | Gerekli alanlar kullanıcıya açık şekilde gösterilmelidir.                      |
| NFR-004 | Veri Gizliliği    | Çalışan ve erişim bilgileri yetkisiz kişiler tarafından görüntülenmemelidir.  | Çalışanın erişim bilgileri sadece yetkili kişiler tarafından görülebilmelidir. |
| NFR-005 | İzlenebilirlik    | Erişim işlemleri daha sonra incelenebilecek şekilde kayıt altına alınmalıdır. | Erişimin ne zaman ve kim tarafından verildiği görülebilmelidir.                |
| NFR-006 | Hata Yönetimi     | Sistem başarısız işlemlerde anlaşılır hata mesajı göstermelidir.              | “Erişim tanımlama işlemi gerçekleştirilemedi.” mesajı gösterilmelidir.         |
| NFR-007 | Erişilebilirlik   | Sistem ihtiyaç duyulan zamanlarda kullanılabilir durumda olmalıdır.           | Çalışan mesai saatlerinde erişim talebi oluşturabilmelidir.                    |

## Functional vs Non-Functional

| Tür                        | Soru                           | Örnek                             |
| -------------------------- | ------------------------------ | --------------------------------- |
| Functional Requirement     | Sistem **ne yapmalı?**         | Erişim talebi oluşturabilmeli.    |
| Non-Functional Requirement | Sistem bunu **nasıl yapmalı?** | Güvenli ve kullanılabilir olmalı. |


## NFR-001 – Performans

Sistem, erişim talebi oluşturma işlemini kabul edilebilir bir sürede tamamlamalıdır.

**Örnek:**
Talep gönderildiğinde kullanıcı uzun süre beklememelidir.

---

## NFR-002 – Güvenlik

Erişim yönetimi yalnızca yetkili kullanıcılar tarafından gerçekleştirilebilmelidir.

**Örnek:**
Bir çalışan başka bir çalışanın erişim talebini onaylayamamalıdır.

---

## NFR-003 – Kullanılabilirlik

Erişim talep ekranı kullanıcı tarafından kolayca anlaşılabilir olmalıdır.

**Örnek:**
Sistem, gerekli alanları açık şekilde göstermelidir.

---

## NFR-004 – Veri Gizliliği

Çalışan ve erişim bilgileri yalnızca yetkili kişiler tarafından görüntülenebilmelidir.

**Örnek:**
Çalışanların erişim bilgileri yetkisiz kullanıcılar tarafından görüntülenememelidir.

---

## NFR-005 – İzlenebilirlik

Erişim işlemleri daha sonra incelenebilecek şekilde kayıt altına alınmalıdır.

**Örnek:**
Bir erişimin ne zaman ve kim tarafından verildiği loglardan görülebilmelidir.

---

## NFR-006 – Hata Yönetimi

Sistem bir işlem başarısız olduğunda kullanıcıya anlaşılır bir hata mesajı göstermelidir.

**Örnek:**
Core Banking'e erişim tanımlanamazsa:

> “Erişim tanımlama işlemi gerçekleştirilemedi. Lütfen IT destek ekibiyle iletişime geçin.”

---

## NFR-007 – Erişilebilirlik

Sistem, ihtiyaç duyulan çalışma saatlerinde erişilebilir durumda olmalıdır.

**Örnek:**
Çalışan erişim talebi oluşturmak istediğinde sistemin kullanılabilir olması beklenir.

---

## Kısa Özet

```text id="v4n9tc"
Functional Requirement
→ Sistem NE yapmalı?

Non-Functional Requirement
→ Sistem bunu NASIL yapmalı?
```

Örneğin:

**FR:** Sistem erişim talebi oluşturmalıdır.

**NFR:** Erişim talebi oluşturma işlemi güvenli ve kullanıcı açısından anlaşılır olmalıdır.

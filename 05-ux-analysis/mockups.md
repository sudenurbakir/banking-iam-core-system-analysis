# Mockups

## 1. Amaç

Mock-up, bir ekranın temel yapısını ve kullanıcı akışını göstermek için hazırlanan taslaktır.

Bu projede çalışanların sistem erişim talebi oluşturabilmesi için basit bir ekran tasarlanmıştır.

Mock-up'ın amacı görsel tasarım yapmak değil, **ekranın hangi bilgileri ve işlemleri içermesi gerektiğini** göstermektir.

---

## 2. Erişim Talebi Ekranı

```text
+------------------------------------------+
|          Erişim Talebi Oluştur           |
+------------------------------------------+

Çalışan:
[ EMP001                         ]

Sistem:
[ Core Banking ▼                ]

Rol:
[ Credit Operations User ▼      ]

Erişim Seviyesi:
[ Görüntüleme ▼                ]

Talep Nedeni:
[______________________________]
[______________________________]

Başlangıç Tarihi:
[ 18.09.2026 ]

              [ Talebi Gönder ]
+------------------------------------------+
```

---

## 3. Ekran Alanları

| Alan             | Açıklama                                  | Zorunlu |
| ---------------- | ----------------------------------------- | ------- |
| Çalışan          | Erişim talebi oluşturacak çalışan         | Evet    |
| Sistem           | Erişim istenen sistem                     | Evet    |
| Rol              | Talep edilen kullanıcı rolü               | Evet    |
| Erişim Seviyesi  | Kullanıcının sahip olacağı yetki seviyesi | Evet    |
| Talep Nedeni     | Erişim ihtiyacının açıklaması             | Evet    |
| Başlangıç Tarihi | Erişimin başlayacağı tarih                | Evet    |

---

## 4. Kullanıcı Akışı

```text
Erişim Talep Ekranı
        ↓
Bilgileri Gir
        ↓
Talebi Gönder
        ↓
Bilgi Kontrolü
        ↓
Başarılı → Talep Oluşturuldu
        ↓
Yönetici Onayı
```

---

## 5. BA'nın Mock-up'taki Rolü

BA'nın mock-up hazırlamasındaki amaç:

* Kullanıcı ihtiyacını ekrana yansıtmak
* Gerekli alanları belirlemek
* Zorunlu alanları tanımlamak
* Kullanıcı akışını göstermek
* Geliştirme ekibine ekran davranışını anlatmak

Mock-up daha sonra Figma veya Balsamiq gibi araçlarla görselleştirilebilir.

Bu projede hazırlanan taslak, **fonksiyonel gereksinimleri destekleyen basit bir BA mock-up'ı** olarak değerlendirilmiştir.

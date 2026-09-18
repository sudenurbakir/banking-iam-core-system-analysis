# TO-BE Process Analysis

## 1. Amaç

Bu dokümanın amacı, AS-IS analizinde tespit edilen problemlere yönelik hedeflenen erişim yönetimi sürecini (TO-BE) tanımlamaktır.

TO-BE süreçte erişim taleplerinin merkezi bir yapı üzerinden yönetilmesi, gerekli onayların alınması, çalışan rolüne uygun erişimlerin kontrol edilmesi ve tüm işlemlerin izlenebilir olması hedeflenmektedir.

---

## 2. Hedeflenen Süreç

Yeni yapıda çalışanların sistem erişim talepleri merkezi bir erişim yönetimi süreci üzerinden oluşturulacaktır.

Temel süreç:

```text
Çalışan
   ↓
Erişim Talebi Oluşturur
   ↓
Yönetici Onayı
   ↓
Rol ve Erişim Kuralı Kontrolü
   ↓
IAM Sistemi
   ↓
İlgili Sisteme Erişim Tanımlama
   ↓
Audit Log
   ↓
Çalışana Bildirim
```

---

## 3. TO-BE Süreç Adımları

### Adım 1 – Erişim Talebinin Oluşturulması

Çalışan merkezi erişim yönetimi ekranından erişim talebi oluşturur.

Talepte aşağıdaki bilgiler bulunabilir:

* Çalışan bilgisi
* Talep edilen sistem
* Talep edilen rol
* Erişim seviyesi
* Talep nedeni
* Talep başlangıç tarihi
* Gerekiyorsa erişim bitiş tarihi

Örnek:

```text
Çalışan: Kredi Operasyon Uzmanı
Sistem: Core Banking
Rol: Credit Operations User
Erişim: Görüntüleme + İşlem
Talep Nedeni: Kredi operasyon işlemlerinin yürütülmesi
```

---

### Adım 2 – Yönetici Onayı

Talep çalışanın yöneticisine iletilir.

Yönetici:

* Talebin iş gereksinimiyle uyumlu olup olmadığını,
* Talep edilen sistemin görev için gerekli olup olmadığını,
* Talep edilen rolün uygunluğunu

değerlendirir.

Yönetici talebi:

* Onaylayabilir
* Reddedebilir

---

### Adım 3 – Rol ve Erişim Kuralı Kontrolü

Yönetici tarafından onaylanan talep IAM sistemi tarafından kontrol edilir.

Bu aşamada çalışanın rolü ile talep edilen erişimin uyumlu olup olmadığı değerlendirilir.

Örneğin:

```text
Çalışan Rolü
      ↓
Kredi Operasyon Uzmanı
      ↓
İzin Verilen Roller
      ↓
Credit Operations User
```

Eğer talep edilen erişim çalışanın rolüyle uyumlu değilse talep otomatik olarak reddedilebilir veya ek onaya gönderilebilir.

---

### Adım 4 – IAM Üzerinden Erişim Tanımlanması

Kontroller başarılı olduğunda IAM sistemi erişim işlemini gerçekleştirir.

IAM burada merkezi erişim yönetim noktası olarak çalışır.

Örneğin:

```text
IAM
 ↓
Core Banking
 ↓
Credit Operations User
 ↓
Erişim Tanımlandı
```

Bu projede IAM altyapısının teknik olarak geliştirilmesi değil, **erişim yönetimi sürecindeki rolü ve sistemlerle olan etkileşimi** analiz edilmektedir.

---

### Adım 5 – İlgili Sisteme Entegrasyon

IAM sistemi, erişimin tanımlanması için ilgili sistemle iletişim kurar.

Örneğin:

```text
IAM
 ↓
API / SOAP
 ↓
Core Banking
```

Bu iletişim sırasında:

* Talep edilen kullanıcı
* Rol
* Erişim seviyesi
* İşlem tipi

gibi bilgiler ilgili sisteme iletilebilir.

---

### Adım 6 – Audit Log Oluşturulması

Erişim işlemi tamamlandığında işlem hakkında log kaydı oluşturulur.

Örneğin:

```text
User: EMP00125
Action: ACCESS_GRANTED
System: CORE_BANKING
Role: CREDIT_OPERATIONS_USER
Date: 2026-09-18
Result: SUCCESS
```

Bu kayıt sayesinde daha sonra:

* Kim erişim aldı?
* Hangi sisteme erişim aldı?
* Hangi rol verildi?
* İşlem ne zaman gerçekleşti?
* İşlem başarılı oldu mu?

gibi sorular cevaplanabilir.

---

### Adım 7 – Çalışana Bildirim

İşlem tamamlandığında çalışana erişim durumuyla ilgili bildirim gönderilir.

Örneğin:

```text
Erişim talebiniz onaylanmış ve
Core Banking sistemine erişiminiz tanımlanmıştır.
```

Talep reddedilmişse kullanıcıya reddedilme durumu da bildirilir.

---

## 4. Offboarding Süreci

TO-BE yapısında yalnızca yeni erişim verme süreci değil, çalışanların görev değişikliği veya işten ayrılması durumundaki erişimlerinin kaldırılması da ele alınmalıdır.

Örnek süreç:

```text
Çalışan İşten Ayrılır
        ↓
HR Bilgiyi Sisteme Girer
        ↓
IAM Bilgilendirilir
        ↓
Aktif Erişimler Kontrol Edilir
        ↓
Erişimler Kaldırılır
        ↓
Audit Log Oluşturulur
```

Bu sayede çalışan şirketten ayrıldıktan sonra eski sistem erişimlerinin aktif kalması önlenmeye çalışılır.

---

## 5. AS-IS → TO-BE Değişiklikleri

| AS-IS                                              | TO-BE                                  |
| -------------------------------------------------- | -------------------------------------- |
| Farklı kanallardan talep                           | Merkezi erişim talebi                  |
| Manuel takip                                       | Merkezi durum takibi                   |
| Standart olmayan bilgiler                          | Standart talep alanları                |
| Manuel erişim kontrolü                             | Rol bazlı erişim kontrolü              |
| Sınırlı geçmiş takibi                              | Audit log                              |
| Manuel sistem iletişimi                            | IAM üzerinden entegrasyon              |
| Ayrılan çalışan erişimleri manuel takip edilebilir | Offboarding sürecinin merkezi yönetimi |
| Kullanıcıya sınırlı bilgi                          | Otomatik bildirim                      |

---

## 6. Hedeflenen İş Kuralları

TO-BE süreçte aşağıdaki temel kuralların uygulanması hedeflenmektedir:

**BR-TOBE-001:** Erişim talebi merkezi sistem üzerinden oluşturulmalıdır.

**BR-TOBE-002:** Erişim talebi ilgili yönetici tarafından onaylanmadan erişim tanımlanmamalıdır.

**BR-TOBE-003:** Kullanıcıya verilecek erişim çalışanın rolüyle uyumlu olmalıdır.

**BR-TOBE-004:** Uygun olmayan erişim talepleri otomatik olarak reddedilebilmeli veya ek onaya gönderilebilmelidir.

**BR-TOBE-005:** Erişim değişiklikleri audit log içerisinde kayıt altına alınmalıdır.

**BR-TOBE-006:** İşten ayrılan çalışanların aktif erişimleri kaldırılmalıdır.

**BR-TOBE-007:** Kullanıcı erişim talebinin güncel durumunu görüntüleyebilmelidir.

---

## 7. BA Perspektifinden Değerlendirme

TO-BE analizinde Business Analyst'in amacı yalnızca yeni bir ekran veya sistem önermek değildir.

AS-IS sürecindeki problemlerin hangi gereksinimlerle çözüleceğini belirlemek önemlidir.

Örneğin:

**Problem:**
Erişim taleplerinin takip edilmesi zor.

**TO-BE yaklaşımı:**
Merkezi erişim talep ekranı ve talep durumlarının takip edilebildiği bir yapı oluşturulması.

**Problem:**
Kullanıcının görevine uygun olmayan erişim talep etme riski bulunuyor.

**TO-BE yaklaşımı:**
Rol bazlı erişim kurallarının uygulanması.

**Problem:**
Kim tarafından hangi erişimin verildiği takip edilemiyor.

**TO-BE yaklaşımı:**
Audit log oluşturulması.

Bu nedenle TO-BE süreç, sonraki aşamada oluşturulacak **functional requirements, business rules, user stories ve acceptance criteria** için temel oluşturacaktır.

---

## 8. TO-BE Süreç Özeti

```text
Çalışan
   ↓
Erişim Talebi
   ↓
Yönetici Onayı
   ↓
Rol & Policy Kontrolü
   ↓
IAM
   ↓
API / SOAP Entegrasyonu
   ↓
İlgili Sistem
   ↓
Audit Log
   ↓
Bildirim
```

### Hedef

Amaç; erişim taleplerinin **merkezi, standart, rol bazlı, izlenebilir ve kontrollü** bir süreç üzerinden yönetilmesidir.

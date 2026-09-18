# AS-IS Process Analysis

## 1. Amaç

Bu dokümanın amacı, kurgusal bir bankada çalışanların sistem erişimi alma sürecinin mevcut durumunu (AS-IS) analiz etmektir.

Analiz kapsamında erişim talebinin oluşturulması, yönetici onayı, ilgili ekiplerin kontrolü ve erişimin tanımlanması gibi temel adımlar incelenmiştir.

---

## 2. Mevcut Süreç

Mevcut durumda çalışanların farklı sistemlere erişim talepleri merkezi ve standart bir süreç üzerinden yönetilmemektedir.

Bir çalışanın Core Banking, CRM veya raporlama gibi sistemlere erişim ihtiyacı olduğunda talep farklı kanallar üzerinden ilgili ekip veya yöneticilere iletilebilmektedir.

Örnek olarak süreç aşağıdaki şekilde ilerleyebilir:

```text
Çalışan
   ↓
Erişim İhtiyacını Belirtir
   ↓
Yöneticiye Talep İletilir
   ↓
Yönetici Onayı
   ↓
İlgili IT/IAM Ekibine İletim
   ↓
Erişim Kontrolü
   ↓
Sistemde Erişim Tanımlama
   ↓
Çalışana Bilgi Verilmesi
```

---

## 3. AS-IS Süreç Adımları

### Adım 1 – Erişim İhtiyacının Oluşması

Çalışan, görevini yerine getirebilmek için bir veya birden fazla sisteme erişim ihtiyacı duyar.

Örneğin:

* Core Banking sistemine erişim
* CRM sistemine erişim
* Raporlama sistemine erişim

### Adım 2 – Erişim Talebinin İletilmesi

Çalışan erişim ihtiyacını mevcut iletişim kanallarından biri aracılığıyla yöneticisine veya ilgili IT ekibine iletir.

Talep e-posta, form veya farklı bir şirket içi iletişim kanalı üzerinden oluşturulabilir.

### Adım 3 – Yönetici Onayı

Yönetici, çalışanın görevini ve talep edilen erişimi değerlendirir.

Örneğin:

> Çalışanın görev tanımı nedeniyle Core Banking sistemine erişmesi gerekiyor mu?

Uygun görülürse talep onaylanır.

### Adım 4 – IT / IAM Kontrolü

Onaylanan talep ilgili teknik ekibe iletilir.

IAM veya IT ekibi:

* Çalışanın mevcut rollerini,
* Talep edilen sistemi,
* İstenen erişim seviyesini,
* İlgili erişim kurallarını

kontrol eder.

### Adım 5 – Erişimin Tanımlanması

Kontroller uygun ise çalışanın ilgili sisteme erişimi tanımlanır.

Örneğin:

```text
Çalışan Rolü: Kredi Operasyon Uzmanı

Talep:
Core Banking → Kredi Modülü → Görüntüleme + İşlem Yetkisi
```

### Adım 6 – Bilgilendirme

Erişim tanımlandıktan sonra çalışan bilgilendirilir.

Ancak mevcut süreçte talebin hangi aşamada olduğu veya işlemin ne zaman tamamlandığı konusunda merkezi bir takip mekanizması bulunmayabilir.

---

## 4. Mevcut Süreçte Tespit Edilen Problemler

AS-IS analizinde aşağıdaki problemler tespit edilmiştir:

### 4.1. Merkezi Talep Takibinin Olmaması

Erişim talepleri farklı kanallar üzerinden oluşturulduğunda tüm taleplerin tek bir noktadan takip edilmesi zorlaşabilir.

### 4.2. Süreç Görünürlüğünün Düşük Olması

Çalışan talebin:

* Beklemede mi,
* Yönetici onayında mı,
* IT incelemesinde mi,
* Tamamlandı mı

olduğunu kolayca takip edemeyebilir.

### 4.3. Standart Olmayan Talep Bilgileri

Farklı kanallar kullanıldığında talep içerisinde bulunan bilgiler değişebilir.

Örneğin bir talepte erişim seviyesi belirtilirken diğerinde yalnızca sistem adı belirtilmiş olabilir.

### 4.4. Erişimlerin Rol Bazlı Kontrolünün Zorlaşması

Çalışanın görevine uygun erişim seviyesinin standart şekilde kontrol edilmesi zorlaşabilir.

### 4.5. İşten Ayrılan Çalışanların Erişimleri

Çalışanın görevden ayrılması veya görev değişikliği durumunda sahip olduğu erişimlerin zamanında kaldırılmaması operasyonel ve güvenlik açısından risk oluşturabilir.

### 4.6. Audit / Geçmiş Takibinin Zor Olması

Hangi çalışana, hangi sistem için, ne zaman ve kim tarafından erişim verildiğinin merkezi şekilde takip edilmesi zorlaşabilir.

---

## 5. AS-IS Problemlerinin Özeti

| Problem                                 | Olası Etki               |
| --------------------------------------- | ------------------------ |
| Merkezi talep yönetiminin olmaması      | Takip zorluğu            |
| Standart olmayan talepler               | Eksik veya hatalı bilgi  |
| Süreç durumunun görünmemesi             | Kullanıcı belirsizliği   |
| Rol bazlı kontrolün standart olmaması   | Uygunsuz erişim riski    |
| Offboarding sürecinin manuel ilerlemesi | Eski erişimlerin kalması |
| Merkezi audit geçmişinin olmaması       | İzlenebilirlik sorunu    |

---

## 6. BA Perspektifinden Değerlendirme

Business Analyst olarak AS-IS analizinde temel amaç mevcut sürecin nasıl çalıştığını anlamaktır.

Bu aşamada doğrudan çözüm üretmek yerine öncelikle:

* Sürece kimler dahil?
* Hangi adımlar mevcut?
* Hangi sistemler kullanılıyor?
* Hangi bilgiler oluşturuluyor?
* Onay nerede gerçekleşiyor?
* Hangi noktalarda manuel işlem bulunuyor?
* Nerelerde gecikme veya hata oluşabiliyor?
* Hangi bilgilerin takip edilmesi gerekiyor?

sorularına cevap aranır.

Bu analiz sonucunda elde edilen problemler, bir sonraki aşamada oluşturulacak **TO-BE sürecinin** temelini oluşturacaktır.

---

## 7. AS-IS Süreç Özeti

```text
Çalışan
   ↓
Erişim İhtiyacı
   ↓
Talebin İletilmesi
   ↓
Yönetici Onayı
   ↓
IT / IAM Kontrolü
   ↓
Erişim Tanımlama
   ↓
Çalışana Bilgilendirme
```

### Temel AS-IS Problemi

Mevcut süreçte erişim taleplerinin merkezi, standart, izlenebilir ve rol bazlı bir yapı üzerinden yönetilmemesi nedeniyle süreç takibi ve erişim kontrolü zorlaşabilmektedir.

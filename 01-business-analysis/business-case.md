# Business Case

## 1. Proje Tanımı

Bu proje, kurgusal bir bankada çalışanların farklı bankacılık uygulamalarına erişimlerinin merkezi olarak yönetilmesi amacıyla oluşturulmuştur.

Bankada çalışanların görev ve sorumluluklarına göre farklı sistemlere erişim ihtiyacı bulunmaktadır. Mevcut yapıda erişim taleplerinin farklı ekipler üzerinden manuel olarak yönetilmesi, erişimlerin takip edilmesini ve kontrol edilmesini zorlaştırmaktadır.

Proje kapsamında, çalışan erişim taleplerinin merkezi bir IAM (Identity and Access Management) sistemi üzerinden yönetilmesi ve ilgili bankacılık sistemleriyle entegre edilmesi analiz edilmektedir.

---

## 2. İş Problemi

Mevcut durumda kullanıcı erişim taleplerinin manuel veya farklı kanallar üzerinden yönetildiği varsayılmaktadır.

Bu durum aşağıdaki problemlere neden olabilir:

* Erişim taleplerinin takip edilmesinin zorlaşması
* Kullanıcıya yanlış yetki verilmesi riski
* Onay süreçlerinin uzaması
* Çalışan görev değişikliklerinde erişimlerin güncellenmesinin gecikmesi
* İşten ayrılan çalışanların erişimlerinin zamanında kapatılmaması
* Erişim geçmişinin yeterince izlenememesi
* Farklı sistemlerde kullanıcı bilgilerinin ayrı ayrı yönetilmesi

---

## 3. Business Need

Bankanın çalışan erişimlerini daha kontrollü ve izlenebilir şekilde yönetebilmesi için merkezi bir erişim yönetimi sürecine ihtiyaç duyulmaktadır.

Yeni yapıda çalışanların erişim taleplerinin belirlenen kurallara göre oluşturulması, gerekli onaylardan geçirilmesi ve ilgili sistemlerdeki erişimlerin kontrollü şekilde yönetilmesi hedeflenmektedir.

---

## 4. Proje Amacı

Projenin amacı;

* Çalışan erişim taleplerinin merkezi olarak yönetilmesini,
* Erişim taleplerinin gerekli onay süreçlerinden geçirilmesini,
* Çalışan rolüne göre uygun erişimlerin belirlenmesini,
* Yetki değişikliklerinin takip edilmesini,
* Çalışanın işten ayrılması durumunda erişimlerin kapatılmasını,
* Erişim işlemlerinin izlenebilir olmasını

sağlayacak iş ve sistem gereksinimlerini analiz etmektir.

---

## 5. Proje Kapsamındaki Temel Akış

Proje kapsamında temel erişim talep süreci aşağıdaki şekilde ele alınacaktır:

```text
Çalışan
   ↓
Erişim Talebi Oluşturma
   ↓
Yönetici Onayı
   ↓
IAM Kontrolü
   ↓
Rol / Yetki Kontrolü
   ↓
İlgili Sisteme Erişim Tanımlama
   ↓
Audit Log
   ↓
Çalışana Bildirim
```

---

## 6. Beklenen Faydalar

Projenin uygulanmasıyla birlikte:

* Erişim taleplerinin daha düzenli takip edilmesi,
* Yetki taleplerinin belirli kurallar çerçevesinde değerlendirilmesi,
* Onay süreçlerinin izlenebilir hale gelmesi,
* Kullanıcı erişimlerinin merkezi olarak takip edilebilmesi,
* Erişim değişikliklerinin kayıt altına alınması,
* İşten ayrılan çalışanların erişimlerinin kapatılmasının kolaylaştırılması,
* Bankacılık sistemleri arasındaki erişim süreçlerinin daha kontrollü yönetilmesi

beklenmektedir.

---

## 7. Varsayımlar

Bu proje kapsamında aşağıdaki varsayımlar kullanılmıştır:

* Bankada merkezi bir IAM sistemi bulunmaktadır.
* Çalışanların temel kullanıcı bilgileri bir insan kaynakları sistemi üzerinden alınabilmektedir.
* Bankacılık uygulamaları IAM sistemiyle entegre edilebilir durumdadır.
* Erişim talepleri belirli roller ve kurallar üzerinden değerlendirilmektedir.
* Erişim talepleri için yönetici onayı gerekmektedir.
* Sistemlerde yapılan erişim değişiklikleri loglanmaktadır.

---

## 8. Başarı Kriterleri

Projenin başarılı kabul edilmesi için:

1. Çalışanların erişim talebi oluşturabilmesi,
2. Erişim taleplerinin gerekli onay sürecinden geçmesi,
3. Kullanıcının rolüne göre uygun erişimlerin belirlenebilmesi,
4. Onaylanan erişimin ilgili sisteme aktarılabilmesi,
5. Erişim işlemlerinin kayıt altına alınması,
6. Erişim değişikliklerinin takip edilebilmesi,
7. İşten ayrılan çalışanların erişimlerinin kapatılabilmesi

gerekmektedir.

---

## 9. BA Perspektifi

Bu proje kapsamında Business Analyst olarak temel odak noktası IAM sisteminin teknik olarak geliştirilmesi değil, iş ihtiyacının anlaşılması ve bu ihtiyacın sistem gereksinimlerine dönüştürülmesidir.

BA çalışmaları kapsamında;

* İş probleminin anlaşılması,
* Stakeholder'ların belirlenmesi,
* Mevcut ve hedef süreçlerin analiz edilmesi,
* Gereksinimlerin dokümante edilmesi,
* Business Rule'ların tanımlanması,
* User Story ve Acceptance Criteria oluşturulması,
* Sistem entegrasyonlarının analiz edilmesi,
* Test ve UAT süreçlerinin desteklenmesi

ele alınacaktır.

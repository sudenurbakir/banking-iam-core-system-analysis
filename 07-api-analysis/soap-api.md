# SOAP API Analysis

## 1. SOAP Nedir?

SOAP (Simple Object Access Protocol), farklı yazılım sistemlerinin birbiriyle iletişim kurmasını sağlayan bir mesajlaşma protokolüdür.

SOAP mesajları genellikle **XML** formatında taşınır.

Bu nedenle REST ile temel iletişim mantığı benzer olsa da veri yapısı ve kullanım şekli farklıdır.

Basit olarak:

```text
IAM
 ↓
SOAP Request
 ↓
Core Banking
 ↓
SOAP Response
 ↓
IAM
```

Bu projede SOAP, IAM ile Core Banking gibi kurumsal sistemler arasında iletişim kurulabilecek alternatif bir entegrasyon yöntemi olarak ele alınmıştır.

---

## 2. SOAP ve REST Arasındaki Temel Fark

| Konu            | REST                       | SOAP                                   |
| --------------- | -------------------------- | -------------------------------------- |
| Yapı            | Mimari yaklaşım            | Protokol                               |
| Veri formatı    | Genellikle JSON            | XML                                    |
| Kullanım        | Modern web/API servisleri  | Kurumsal ve legacy sistemler dahil     |
| Yapı            | Daha esnek                 | Daha standart ve kurallı               |
| HTTP Methodları | GET, POST, PUT, DELETE vb. | Genellikle POST kullanımı              |
| Dokümantasyon   | OpenAPI vb. kullanılabilir | WSDL yaygın olarak kullanılır          |
| BA açısından    | Request/response analizi   | XML mesaj ve servis sözleşmesi analizi |

Burada önemli nokta:

> **SOAP kötü, REST iyi** şeklinde düşünmemek gerekir.

Hangi teknolojinin kullanılacağı sistem mimarisine ve mevcut altyapıya bağlıdır.

---

## 3. XML Nedir?

SOAP mesajlarında XML kullanılır.

XML, veriyi etiketler aracılığıyla yapılandırılmış şekilde ifade eder.

Örneğin:

```xml
<Employee>
    <EmployeeId>EMP001</EmployeeId>
    <System>CORE_BANKING</System>
    <Role>CREDIT_OPERATIONS_USER</Role>
    <AccessLevel>TRANSACTION</AccessLevel>
</Employee>
```

Burada:

* `EmployeeId` → Çalışan ID'si
* `System` → Sistem
* `Role` → Rol
* `AccessLevel` → Erişim seviyesi

şeklinde veri taşınmaktadır.

BA olarak XML'i sıfırdan geliştirmekten çok, **hangi alanların gönderildiğini ve ne anlama geldiğini okuyabilmek** önemlidir.

---

## 4. SOAP Mesaj Yapısı

SOAP mesajları belirli bir XML yapısına sahiptir.

Basitleştirilmiş örnek:

```xml
<soap:Envelope>

    <soap:Header>
        <!-- Kimlik doğrulama veya metadata -->
    </soap:Header>

    <soap:Body>

        <CreateAccessRequest>
            <EmployeeId>EMP001</EmployeeId>
            <System>CORE_BANKING</System>
            <Role>CREDIT_OPERATIONS_USER</Role>
            <AccessLevel>TRANSACTION</AccessLevel>
        </CreateAccessRequest>

    </soap:Body>

</soap:Envelope>
```

Buradaki temel bölümler:

### Envelope

SOAP mesajının ana kapsayıcısıdır.

### Header

Kimlik doğrulama veya ek metadata gibi bilgiler bulunabilir.

### Body

Asıl iş isteğinin bulunduğu bölümdür.

BA açısından en önemli bölüm genellikle **Body** içerisindeki business verileridir.

---

## 5. SOAP Request Örneği

IAM, Core Banking sistemine erişim oluşturmak için SOAP request gönderebilir.

Örnek:

```xml
<soap:Envelope>

    <soap:Header>
        <Authorization>Token-Example</Authorization>
    </soap:Header>

    <soap:Body>

        <CreateAccessRequest>

            <EmployeeId>EMP001</EmployeeId>
            <System>CORE_BANKING</System>
            <Role>CREDIT_OPERATIONS_USER</Role>
            <AccessLevel>TRANSACTION</AccessLevel>

        </CreateAccessRequest>

    </soap:Body>

</soap:Envelope>
```

Business anlamı:

> EMP001 çalışanına Core Banking üzerinde Credit Operations User rolünde Transaction erişimi tanımla.

---

## 6. SOAP Response

Core Banking sistemi isteği işledikten sonra SOAP response dönebilir.

### Başarılı Response

```xml
<soap:Envelope>

    <soap:Body>

        <CreateAccessResponse>

            <RequestId>IAM-1001</RequestId>
            <Status>SUCCESS</Status>

        </CreateAccessResponse>

    </soap:Body>

</soap:Envelope>
```

Business anlamı:

> Erişim talebi başarıyla işlendi.

---

## 7. SOAP Hata Yönetimi

SOAP'ta hatalar genellikle **SOAP Fault** yapısıyla ifade edilir.

Örnek:

```xml
<soap:Fault>

    <faultcode>AUTHORIZATION_ERROR</faultcode>

    <faultstring>
        User is not authorized for this operation
    </faultstring>

</soap:Fault>
```

Bu durumda BA olarak şu sorular önemlidir:

* Hata neden oluştu?
* Kullanıcıya bildirim gidecek mi?
* İşlem tekrar denenebilir mi?
* Hata loglanacak mı?
* IT ekibine bildirim gönderilecek mi?

---

## 8. WSDL Nedir?

SOAP servislerinde önemli kavramlardan biri **WSDL**'dir.

WSDL (Web Services Description Language), SOAP servisinin nasıl kullanılacağını tanımlayan bir servis tanımıdır.

Basitleştirilmiş olarak WSDL;

* Servisin ne yaptığını,
* Hangi operasyonların bulunduğunu,
* Hangi request yapısının kullanılacağını,
* Hangi response yapısının döneceğini,
* Veri tiplerini

tanımlayabilir.

BA açısından WSDL, bir SOAP servisinin **teknik sözleşmesini anlamak için incelenebilecek dokümanlardan biridir.**

Örneğin bir WSDL içerisinde:

```text
CreateAccessRequest
GetAccessRequest
RemoveAccessRequest
```

gibi operasyonlar bulunabilir.

BA burada özellikle ilgili business operasyonunun ne yaptığını anlamaya çalışır.

---

## 9. REST ve SOAP Aynı Projede Olabilir mi?

Evet.

Bir sistemin bütün entegrasyonlarının aynı teknolojiyle yapılması zorunlu değildir.

Örneğin:

```text
Employee
    ↓
IAM
    ↓
REST API
    ↓
Modern Access Service
    ↓
SOAP
    ↓
Legacy Core Banking
```

Burada IAM modern bir servisle REST üzerinden iletişim kurarken, eski Core Banking sistemi SOAP kullanıyor olabilir.

Bu nedenle BA'nın bir projede hem REST hem SOAP görmesi mümkündür.

---

## 10. BA SOAP Analizi Yaparken Neleri Sorabilir?

### Business

* SOAP servisi hangi iş ihtiyacını karşılıyor?
* Hangi işlem gerçekleştiriliyor?
* Hangi sistem çağrıyı başlatıyor?

### Request

* Hangi alanlar gönderiliyor?
* Hangi alanlar zorunlu?
* Veri tipleri neler?
* XML yapısı nasıl?

### Response

* Başarılı response nasıl?
* Hangi bilgiler dönüyor?
* Hata response'u nasıl?

### Integration

* Hangi sistemle iletişim kuruluyor?
* Servis adresi nedir?
* Hangi operasyon kullanılacak?
* WSDL mevcut mu?

### Error Handling

* SOAP Fault durumunda ne yapılacak?
* İşlem tekrar denenebilir mi?
* Hata loglanacak mı?
* Kullanıcı bilgilendirilecek mi?

---

## 11. REST ve SOAP'u Nasıl Hatırlamalısın?

Ezberlemek yerine şu şekilde düşün:

### REST

> "HTTP üzerinden API ile veri alışverişi yapıyorum."

Örneğin:

```text
POST /api/access-requests
```

ve JSON:

```json
{
  "employeeId": "EMP001",
  "role": "CREDIT_OPERATIONS_USER"
}
```

### SOAP

> "Tanımlı bir SOAP servisine XML mesaj gönderiyorum."

Örneğin:

```xml
<CreateAccessRequest>
    <EmployeeId>EMP001</EmployeeId>
    <Role>CREDIT_OPERATIONS_USER</Role>
</CreateAccessRequest>
```

İkisinin de temel amacı:

**Sistemlerin iletişim kurmasını sağlamak.**

---

## 12. Business Analyst'in SOAP Konusundaki Rolü

BA'nın SOAP servisini geliştirmesi beklenmez.

BA'nın görevi:

* Servisin business amacını anlamak,
* Request alanlarını analiz etmek,
* Response yapısını anlamak,
* WSDL gibi servis dokümanlarını incelemek,
* Hata senaryolarını belirlemek,
* Entegrasyon gereksinimlerini dokümante etmek,
* Test ekibinin kullanabileceği senaryoları hazırlamaktır.

Örneğin business ihtiyacı:

> "Onaylanan erişim Core Banking sistemine aktarılmalı."

BA bunu şu şekilde analiz edebilir:

```text
Business Requirement
        ↓
IAM → Core Banking entegrasyonu
        ↓
SOAP Service
        ↓
CreateAccessRequest
        ↓
XML Request
        ↓
XML Response
        ↓
Success / SOAP Fault
        ↓
Audit Log
```

Bu şekilde business ihtiyacını teknik ekibin anlayabileceği bir entegrasyon gereksinimine dönüştürür.

# 💼 Accounting System - Modern Muhasebe Web API

<div align="center">

![.NET](https://img.shields.io/badge/.NET-9.0-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)
![C#](https://img.shields.io/badge/C%23-239120?style=for-the-badge&logo=c-sharp&logoColor=white)
![SignalR](https://img.shields.io/badge/SignalR-Real--Time-00ADD8?style=for-the-badge&logo=microsoftazure&logoColor=white)
![Entity Framework](https://img.shields.io/badge/EF%20Core-9.0-512BD4?style=for-the-badge&logo=nuget&logoColor=white)
![SQL Server](https://img.shields.io/badge/SQL%20Server-CC2927?style=for-the-badge&logo=microsoft-sql-server&logoColor=white)

*Gerçek zamanlı bildirimler ve background worker destekli modern muhasebe sistemi*

[Özellikler](#-özellikler) • [Kurulum](#-kurulum) • [Teknolojiler](#-teknolojiler) • [API Dokümantasyonu](#-api-endpoints) • [Mimari](#-mimari-yapı)

</div>

---

## 🎯 Proje Hakkında

Bu proje, **temel muhasebe mantığı** ile hazırlanmış, küçük çaplı ama **gerçek iş mantığına uygun** bir muhasebe yönetim sistemidir. Modern web teknolojileri kullanılarak geliştirilmiş, **gerçek zamanlı bildirimler** ve **otomatik vade kontrolü** özellikleri içerir.

### ✨ Temel Özellikler

- 💰 **Müşteri Yönetimi**: CRUD operasyonları ile tam müşteri yönetimi
- 🧾 **Fatura Yönetimi**: Çoklu kalemli fatura oluşturma ve takip sistemi
- 💳 **Ödeme Takibi**: Gerçek zamanlı borç güncelleme ve ödeme geçmişi
- ⚡ **Vade Kontrolü**: Background worker ile otomatik vadesi geçmiş fatura bildirimleri
- 🔔 **Real-Time Bildirimler**: SignalR ile WebSocket üzerinden anlık güncellemeler
- 🎨 **Demo Frontend**: SignalR test ve gözlem için hazır arayüz

> **Not:** Frontend kısmı yalnızca SignalR bildirimlerini test etmek ve gözlemlemek için oluşturulmuştur.

## 🛠 Teknolojiler

### Backend Stack

| Teknoloji | Versiyon | Kullanım Amacı |
|-----------|----------|----------------|
| **.NET** | 9.0 | Web API Framework |
| **ASP.NET Core** | 9.0 | RESTful API |
| **Entity Framework Core** | 9.0.10 | ORM, Code First |
| **SQL Server** | - | Veritabanı |
| **SignalR** | 1.2.0 | Real-time WebSocket iletişimi |
| **Background Service** | - | Otomatik vade kontrolü (her 1 dakika) |

### Frontend Demo

- HTML5 + Vanilla JavaScript
- SignalR Client Library (CDN)
- Modern CSS3

## 📋 Uygulama ile Yapılabilenler

### 🎯 Temel İşlevler

#### Müşteri İşlemleri
- ✅ Yeni müşteri kaydı oluşturma
- ✅ Müşteri bilgilerini güncelleme
- ✅ Müşteri listesini görüntüleme
- ✅ Müşteri detaylarını ve borç durumunu görüntüleme

#### Fatura İşlemleri
- ✅ Çok kalemli fatura oluşturma
- ✅ Otomatik toplam hesaplama
- ✅ Müşteri borcunu otomatik güncelleme
- ✅ Fatura listesi ve detaylarını görüntüleme

#### Ödeme İşlemleri
- ✅ Faturaya ödeme kaydı ekleme
- ✅ Otomatik borç düşümü
- ✅ Kısmi/tam ödeme desteği
- ✅ Ödeme geçmişini görüntüleme

#### Ürün Yönetimi
- ℹ️ Ürün tanımlama (şu an için veritabanından elle ekleniyor)

### 🔔 SignalR Real-Time Events

Gerçek zamanlı olarak izlenebilen olaylar:

- 🧾 **Yeni Fatura**: Fatura oluşturulduğunda anında bildirim
- 💰 **Yeni Ödeme**: Ödeme alındığında anında bildirim
- 💳 **Borç Güncelleme**: Müşteri borcu değiştiğinde bildirim
- ⚠️ **Vadesi Geçmiş Fatura**: Background worker tarafından her 1 dakikada kontrol edilir ve tespit edildiğinde bildirim gönderilir

## 🚀 Kurulum

### Gereksinimler

- [.NET 9.0 SDK](https://dotnet.microsoft.com/download/dotnet/9.0) ⚡
- [SQL Server](https://www.microsoft.com/sql-server/sql-server-downloads) (LocalDB veya Express) 🗄️
- [Visual Studio 2022](https://visualstudio.microsoft.com/) veya [VS Code](https://code.visualstudio.com/) 💻
- [Git](https://git-scm.com/) 🔧

### Adımlar

#### 1️⃣ Projeyi Klonlayın

```bash
git clone https://github.com/KULLANICI_ADINIZ/accounting-system.git
cd accounting-system
```

#### 2️⃣ Veritabanı Bağlantısını Yapılandırın

`Backend/AccountingSystem/AccountingSystem.WEBAPI/appsettings.json` dosyasını açın ve SQL Server connection string'i düzenleyin:

```json
{
  "ConnectionStrings": {
    "SqlServer": "Data Source=SUNUCU_ADINIZ;Initial Catalog=AccountingSystemDb;Integrated Security=True;Trust Server Certificate=True"
  }
}
```

#### 3️⃣ Migrations ile Veritabanını Oluşturun

```bash
cd Backend/AccountingSystem/AccountingSystem.WEBAPI
dotnet ef database update
```

#### 4️⃣ Backend API'yi Başlatın

```bash
dotnet run
```

API varsayılan olarak `https://localhost:5199` adresinde çalışacaktır.

#### 5️⃣ Frontend Demo'yu Açın (Opsiyonel)

1. `Frontend/index.html` dosyasını düzenleyin
2. Backend URL'sini kontrol edin (satır ~73):
   ```javascript
   .withUrl("http://localhost:5199/hubs/notifications")
   ```
3. HTML dosyasını tarayıcıda açın

## 📡 API Endpoints

### 👥 Customers

| Method | Endpoint | Açıklama |
|--------|----------|----------|
| `GET` | `/api/Customers/GetAll` | Tüm müşterileri listele |
| `GET` | `/api/Customers/GetById/{id}` | Müşteri detayları |
| `POST` | `/api/Customers/Create` | Yeni müşteri ekle |
| `PUT` | `/api/Customers/Update/{id}` | Müşteri güncelle |
| `DELETE` | `/api/Customers/Delete/{id}` | Müşteri sil |

### 🧾 Invoices

| Method | Endpoint | Açıklama |
|--------|----------|----------|
| `GET` | `/api/Invoices/GetAll` | Tüm faturaları listele |
| `GET` | `/api/Invoices/GetById/{id}` | Fatura detayları (kalemlerle birlikte) |
| `POST` | `/api/Invoices/Create` | Yeni fatura oluştur |
| `DELETE` | `/api/Invoices/Delete/{id}` | Fatura sil |

### 💳 Payments

| Method | Endpoint | Açıklama |
|--------|----------|----------|
| `GET` | `/api/Payments/GetAll` | Tüm ödemeleri listele |
| `GET` | `/api/Payments/GetById/{id}` | Ödeme detayları |
| `POST` | `/api/Payments/Create` | Yeni ödeme kaydet |

### 📝 Örnek Request

**Fatura Oluşturma:**

```http
POST /api/Invoices/Create
Content-Type: application/json

{
  "customerId": 1,
  "dueDate": "2025-12-31T00:00:00Z",
  "items": [
    {
      "productId": 1,
      "quantity": 2,
      "unitPrice": 100.00
    },
    {
      "productId": 2,
      "quantity": 1,
      "unitPrice": 250.00
    }
  ]
}
```

## 🏗 Mimari Yapı

### Proje Klasör Yapısı

```
AccountingProject/
├── Backend/
│   └── AccountingSystem/
│       └── AccountingSystem.WEBAPI/
│           ├── BackgroundWorker/        # Arka plan servisleri
│           ├── Context/                 # EF Core DbContext
│           ├── Controllers/             # API Controllers
│           ├── DTOs/                    # Data Transfer Objects
│           ├── Entities/                # Domain Models
│           ├── Hubs/                    # SignalR Hubs
│           ├── Migrations/              # EF Migrations
│           ├── Services/                # Business Logic
│           └── Program.cs
└── Frontend/
    └── index.html                       # SignalR Test Dashboard
```

### Katmanlı Mimari

```
┌─────────────────────────────────────┐
│         Controllers Layer           │  ← HTTP Request Handler
├─────────────────────────────────────┤
│         Services Layer              │  ← Business Logic
├─────────────────────────────────────┤
│         Repository (EF Core)        │  ← Data Access
├─────────────────────────────────────┤
│         Database (SQL Server)       │  ← Data Storage
└─────────────────────────────────────┘

         ┌──────────────┐
         │  SignalR Hub │  ← Real-time Communication
         └──────────────┘
```

## 🗄 Veritabanı Şeması

### Ana Tablolar

- **Customers**: Müşteri bilgileri ve toplam borç
- **Invoices**: Fatura bilgileri (toplam tutar, ödenen tutar, vade tarihi)
- **InvoiceItems**: Fatura kalemleri (ürün, miktar, birim fiyat)
- **Payments**: Ödeme kayıtları
- **Products**: Ürün bilgileri

### İlişkiler

```
Customer (1) ──────< (N) Invoice
Invoice (1) ──────< (N) InvoiceItem
Invoice (1) ──────< (N) Payment
Product (1) ──────< (N) InvoiceItem
```

## 🔌 SignalR Kullanımı

### Hub Bağlantısı

```javascript
const connection = new signalR.HubConnectionBuilder()
  .withUrl("http://localhost:5199/hubs/notifications")
  .withAutomaticReconnect()
  .build();

await connection.start();
```

### Event Dinleme

```javascript
// Yeni fatura bildirimi
connection.on("InvoiceCreated", (data) => {
  console.log("Yeni Fatura:", data);
});

// Ödeme bildirimi
connection.on("PaymentReceived", (data) => {
  console.log("Ödeme Alındı:", data);
});

// Borç güncelleme bildirimi
connection.on("CustomerDebtUpdated", (data) => {
  console.log("Borç Güncellendi:", data);
});

// Vadesi geçmiş fatura bildirimi
connection.on("OverdueInvoiceDetected", (data) => {
  console.log("Vadesi Geçmiş Fatura:", data);
});
```

### Gruplara Katılma

```javascript
// Dashboard grubuna katıl (tüm bildirimleri al)
await connection.invoke("JoinDashboard");

// Belirli müşteri grubuna katıl
await connection.invoke("JoinCustomerGroup", customerId);
```

## 🎨 Özellikler Detayları

### Background Worker

- Her **1 dakikada bir** otomatik olarak çalışır
- Vadesi geçmiş ve ödenmemiş faturaları tarar
- Dashboard grubuna ve ilgili müşteri grubuna bildirim gönderir
- `OverdueInvoiceWorker.cs` içinde implement edilmiştir

### DTO Pattern

Her modül için ayrı DTO'lar:
- `CreateCustomerDto`, `UpdateCustomerDto`, `CustomerListDto`
- `CreateInvoiceDto`, `InvoiceDetailDto`, `InvoiceListDto`
- `CreatePaymentDto`, `PaymentListDto`

### Base Entity

Tüm entity'ler için ortak özellikler:
- `Id` (Primary Key)
- `CreatedDate`
- `UpdatedDate`
- Soft delete desteği için hazır altyapı

## 🚧 Gelecek Geliştirmeler

- [ ] **Authentication & Authorization**: JWT token tabanlı güvenlik
- [ ] **Unit Tests**: XUnit ile test coverage
- [ ] **API Versioning**: Geriye dönük uyumluluk
- [ ] **Docker Support**: Container'laştırma
- [ ] **Logging**: Serilog entegrasyonu
- [ ] **Swagger Documentation**: API dokümantasyonu
- [ ] **Ürün CRUD**: UI üzerinden ürün yönetimi
- [ ] **Fatura Düzenleme**: Fatura güncelleme özelliği
- [ ] **Rapor Modülü**: PDF/Excel export
- [ ] **Toplu İşlemler**: Batch operations

## 🤝 Katkıda Bulunma

1. Fork edin
2. Feature branch oluşturun (`git checkout -b feature/yeniOzellik`)
3. Değişikliklerinizi commit edin (`git commit -m 'Yeni özellik eklendi'`)
4. Branch'inizi push edin (`git push origin feature/yeniOzellik`)
5. Pull Request oluşturun


<div align="center">

⭐ Bu projeyi beğendiyseniz yıldız vermeyi unutmayın!

</div>


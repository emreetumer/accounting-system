Bu proje; temel muhasebe mantığı ile hazırlanmış küçük çaplı ama gerçek iş mantığına uygun bir örnektir.

NOT: Frontend kısmı yalnızca SignalR bildirimlerini test etmek ve gözlemlemek için oluşturulmuştur.

Teknolojiler:

.NET 9 Web API
Entity Framework Core (Code First, MSSQL)
SignalR (WebSocket - real-time bildirim sistemi)
Background Worker (vadesi geçmiş faturalar için)
Frontend (HTML + JS, SignalR client)


Uygulama ile:

Müşteri oluşturulabilir
Fatura oluşturulabilir (otomatik toplam ve borç güncelleme)
Ödeme yapılabilir (borç düşer)
Ürün tanımlanabilir (Şimdilik Db'den elle oluşturuyorum)

SignalR sayesinde gerçek zamanlı olarak:

Yeni fatura
Yeni ödeme
Vadesi geçmiş fatura uyarısı olayları canlı olarak izlenebilir.

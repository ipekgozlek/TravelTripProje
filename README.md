# ✈️ TravelTrip – Seyahat Blogu & Yönetim Paneli

**ASP.NET MVC 5** ve **Entity Framework** ile sıfırdan geliştirdiğim, canlıda yayında olan tam kapsamlı bir web uygulaması. Ziyaretçilere yönelik bir blog sitesi ile içeriklerin yönetildiği, kimlik doğrulamalı bir admin panelinden oluşur.

🌐 **Canlı Demo:** [traveltrip.tryasp.net](http://traveltrip.tryasp.net)
🔐 **Admin Paneli:** [traveltrip.tryasp.net/GirisYap/Login](http://traveltrip.tryasp.net/GirisYap/Login)

<img width="1891" height="899" alt="blog" src="https://github.com/user-attachments/assets/f95a8bef-3d19-412a-bdc6-4b657f9e6f14" />
<img width="1919" height="838" alt="admin" src="https://github.com/user-attachments/assets/67b12271-e856-46e0-bae4-cfcaaedcde94" />
---

## 🎯 Bu Projede Neler Yaptım?

### 🏗️ MVC Mimarisi ile Katmanlı Yapı
- Uygulamayı **Model–View–Controller** desenine göre; sorumlulukları birbirinden ayrılmış 5 controller (`Default`, `About`, `Blog`, `GirisYap`, `Admin`) ile kurguladım.
- Ziyaretçi sitesi ve admin paneli için **iki ayrı Razor layout** (`_MyLayout`, `_AdminLayout`) tasarladım.
- Hazır HTML/CSS şablonlarını **Razor view'larına dönüştürerek** dinamik hâle getirdim.

### 🗄️ Entity Framework 6 – Code First
- Veritabanını **Code First** yaklaşımıyla, C# sınıflarından otomatik oluşturdum.
- **6 tablodan** oluşan ilişkisel bir model tasarladım. Blog ile yorumlar arasında **bire-çok (1–N) ilişki** kurdum (navigation property'ler: `ICollection<Yorumlar>`, `virtual Blog`).
- Şema değişikliklerini **EF Migrations** ile yönettim.
- Verileri **LINQ** sorgularıyla çektim: filtreleme (`Where`), sıralama (`OrderByDescending`), sınırlama (`Take`) ve tekil kayıt sorguları (`FirstOrDefault`, `Find`).

### 🧩 Partial View & ViewModel Kullanımı
- Ana sayfayı, her biri kendi verisini getiren **4 ayrı Partial View** ile (`Html.Action` child action'ları) modüler hâle getirdim.
- Blog detay sayfasında yazı ve yorumları tek bir sayfada göstermek için **ViewModel** (`BlogYorum`) oluşturdum.
- Yorum formunu Partial View olarak ayırıp blog detay sayfasına gömdüm.

### 🔐 Kimlik Doğrulama & Yetkilendirme
- **Forms Authentication** ile admin giriş/çıkış sistemi kurdum.
- Admin sayfalarını **`[Authorize]`** attribute'u ile koruyarak yetkisiz erişimi engelledim.
- Oturum bilgisini **Session** ile yönettim.

### ✏️ Tam CRUD İşlemleri
- Admin panelinden blog yazıları için **ekleme, listeleme, güncelleme ve silme**.
- Yorumlar için **listeleme, güncelleme ve silme** (moderasyon).
- Ziyaretçi tarafında yorum ekleme. Yorumlar ilgili bloga otomatik bağlanır.
- GET/POST ayrımı (`[HttpGet]` / `[HttpPost]`) ve **model binding** ile form işlemleri.

### ☁️ Canlıya Alma (Deployment) & DevOps
- Uygulamayı **MonsterASP.NET** üzerinde, Visual Studio'dan **Web Deploy** ile yayına aldım.
- Yerel SQL Server veritabanını **bulut SQL Server'a taşıdım**: SSMS ile schema + data script'i oluşturup uzak sunucuda çalıştırdım.
- Sunucu tarafında karşılaştığım **uygulama havuzu (.NET Framework / Core) uyumsuzluğu** ve **connection string çözümleme** gibi canlı ortam sorunlarını tespit edip çözdüm.

### 🛡️ Güvenli Konfigürasyon
- Veritabanı şifresini kaynak koddan ayırdım: connection string'leri `configSource` ile **ayrı bir dosyaya** taşıdım ve bu dosyayı `.gitignore` ile **versiyon kontrolünün dışında** tuttum. Böylece hassas bilgiler GitHub'a hiç gitmiyor.
- Yerel ve canlı ortam için farklı bağlantı ayarlarını yönettim.

---

## 🛠️ Teknolojiler

![C#](https://img.shields.io/badge/C%23-239120?style=for-the-badge&logo=csharp&logoColor=white)
![.NET Framework](https://img.shields.io/badge/.NET_Framework_4.8-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)
![ASP.NET MVC](https://img.shields.io/badge/ASP.NET_MVC_5-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)
![SQL Server](https://img.shields.io/badge/SQL_Server-CC2927?style=for-the-badge&logo=microsoftsqlserver&logoColor=white)
![Bootstrap](https://img.shields.io/badge/Bootstrap_5-7952B3?style=for-the-badge&logo=bootstrap&logoColor=white)
![jQuery](https://img.shields.io/badge/jQuery-0769AD?style=for-the-badge&logo=jquery&logoColor=white)

| Alan | Kullanılanlar |
|---|---|
| **Backend** | C#, ASP.NET MVC 5.2.9, .NET Framework 4.8 |
| **Veri Erişimi** | Entity Framework 6.5.2 (Code First, Migrations), LINQ |
| **Veritabanı** | Microsoft SQL Server, SSMS |
| **Frontend** | Razor, HTML5, CSS3, Bootstrap 5, jQuery, W3.CSS |
| **Güvenlik** | Forms Authentication, `[Authorize]`, Session |
| **Yayın** | MonsterASP.NET, Web Deploy |
| **Araçlar** | Visual Studio, Git & GitHub |

---

## 🗄️ Veritabanı Tasarımı

| Tablo | Açıklama | Alanlar |
|---|---|---|
| **Blogs** | Blog yazıları | ID, Baslik, Tarih, Aciklama, BlogImage |
| **Yorumlars** | Bloglara yapılan yorumlar | ID, KullaniciAdi, Mail, Yorum, Blogid **(FK → Blogs)** |
| **Admins** | Yönetici hesapları | ID, Kullanici, Sifre |
| **Hakkimizdas** | Hakkımızda içeriği | ID, FotoUrl, Aciklama |
| **AdresBlogs** | Adres / konum bilgileri | ID, Baslik, Aciklama, AdresAcik, Mail, Telefon, Konum |
| **iletisims** | İletişim mesajları | ID, AdSoyad, Mail, Konu, Mesaj |

```
Blogs (1) ──────< (N) Yorumlars
```

---

## 🗂️ Proje Yapısı

```
TravelTripProje/
├── Controllers/
│   ├── DefaultController.cs     → Ana sayfa + 4 partial view
│   ├── AboutController.cs       → Hakkımızda
│   ├── BlogController.cs        → Blog listesi, detay, yorum yapma
│   ├── GirisYapController.cs    → Login / Logout (Forms Auth)
│   └── AdminController.cs       → Blog & yorum CRUD işlemleri
├── Models/Siniflar/             → Entity sınıfları, DbContext, ViewModel
├── Views/                       → Razor view'lar ve layout'lar
├── Migrations/                  → EF Code First migration ayarları
└── Web.config                   → Uygulama ve kimlik doğrulama ayarları
```

---

## 🚀 Projeyi Kendi Bilgisayarında Çalıştırma

**1. Repoyu klonla**
```bash
git clone https://github.com/ipekgozlek/TravelTripProje.git
```

**2. `ConnectionStrings.config` dosyasını oluştur** (`Web.config` dosyasının yanına)
```xml
<?xml version="1.0" encoding="utf-8"?>
<connectionStrings>
  <add name="Context"
       connectionString="Server=.\SQLEXPRESS;Database=TravelDb;Integrated Security=True;TrustServerCertificate=True;"
       providerName="System.Data.SqlClient" /><img width="1891" height="899" alt="blog" src="https://github.com/user-attachments/assets/ab071a3a-fb66-432b-858a-40bf8599e85c" />

</connectionStrings>
```

**3. Veritabanını oluştur** (Package Manager Console)
```powershell
Update-Database
```

**4. Admin kullanıcısı ekle**
```sql
INSERT INTO Admins (Kullanici, Sifre) VALUES ('admin', '12345');
```

**5. F5 ile çalıştır** 🎉

---

## 🔭 Yol Haritası
Projeyi geliştirmeye devam ediyorum. Planladığım iyileştirmeler:
- [ ] Şifrelerin **hash'lenerek** (BCrypt) saklanması
- [ ] Admin panelinde **İletişim** ve **Hakkımızda** yönetim sayfaları
- [ ] Blog görselleri için **dosya yükleme** desteği
- [ ] **ASP.NET Core**'a taşıma

---

## 👩‍💻 Geliştirici

**İpek Sertel**
[![GitHub](https://img.shields.io/badge/GitHub-ipekgozlek-181717?style=flat&logo=github)](https://github.com/ipekgozlek)

> Yeni fırsatlara ve iş birliklerine açığım. Benimle GitHub üzerinden iletişime geçebilirsin. 👋

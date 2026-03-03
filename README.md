# 💬 Chatter-LiveChat

<div align="center">

![Chatter-LiveChat Logo](icon-192.png)

**Gerçek Zamanlı Sohbet Uygulaması**

[![GitHub stars](https://img.shields.io/github/stars/tda45/Chatter-LiveChat-PC)](https://github.com/tda45/Chatter-LiveChat-PC/stargazers)
[![GitHub license](https://img.shields.io/github/license/tda45/Chatter-LiveChat-PC)](https://github.com/tda45/Chatter-LiveChat-PC/blob/main/LICENSE)
[![GitHub release](https://img.shields.io/github/v/release/tda45/Chatter-LiveChat-PC)](https://github.com/tda45/Chatter-LiveChat-PC/releases/tag/1.0)

[🌐 Web Sitesi](https://tda45.github.io/Chatter-LiveChat-PC-Sitesi/) | 
[📥 İndir](https://tda45.github.io/Chatter-LiveChat-PC-Sitesi/1.0.0-surum.html) | 
[📚 Geliştirme Rehberi](kitap.html) | 
[🐛 Hata Bildir](https://github.com/tda45/Chatter-LiveChat-PC/issues)

</div>

## ✨ Özellikler

- ⚡ **Gerçek Zamanlı** - Supabase Realtime ile anlık mesajlaşma
- 🛡️ **Küfür Filtresi** - Otomatik kelime engelleme
- 👥 **Aktif Kullanıcılar** - Kimler çevrimiçi görün
- ✏️ **Yazıyor Bildirimi** - Karşı taraf yazarken haberin olsun
- 📊 **İstatistikler** - `/stats` komutu ile sohbet analizi
- 🎨 **Gece Kırmızı Tema** - Göz yormayan özel tasarım

## 🚀 Hızlı Başlangıç

### Windows için
```bash
# 1. ZIP'i indir
# 2. Çıkart
# 3. ChatterLiveChat.exe'yi çalıştır

Geliştiriciler için

# Repoyu klonla
git clone https://github.com/tda45/Chatter-LiveChat-PC.git
cd Chatter-LiveChat-PC

# Windows Forms uygulamasını çalıştır
dotnet run --project ChatterLiveChat

📱 Platformlar
Platform	Durum	İndir
Windows	✅ Kararlı	EXE
Android	🚧 Geliştirme Aşamasında	-
iOS	🚧 Planlanıyor	-
Linux	📝 Araştırılıyor	-
📖 Dokümantasyon
📘 Geliştirme Rehberi - Sıfırdan uygulama geliştirme

🔧 API Referansı - Supabase entegrasyonu

🤝 Katkıda Bulunma - Projeye nasıl katkı sağlarsın

❓ SSS - Sıkça sorulan sorular

🏗️ Mimari

graph TD
    A[Windows Forms] --> C[Supabase HTTP Client]
    B[.NET MAUI] --> C
    C --> D[(Supabase Backend)]
    D --> E[PostgreSQL]
    D --> F[Realtime]

📦 Sürüm Geçmişi
v1.0.0 (2026-02-28)
✅ İlk kararlı sürüm

✅ Temel sohbet özellikleri

✅ Giriş/Çıkış mesajları

✅ Küfür filtresi

📄 Lisans
Bu proje MIT lisansı ile lisanslanmıştır. Detaylar için LISANS.md dosyasına bakın.

🙏 Teşekkürler
Supabase - Harika backend hizmeti

.NET MAUI - Çapraz platform desteği

Tüm katkıda bulunanlar ❤️

<div align="center"> Made with ❤️ by tda45 </div> ```

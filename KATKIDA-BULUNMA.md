# 🤝 Katkıda Bulunma Rehberi

Chatter-LiveChat projesine katkıda bulunmak istediğin için teşekkürler! ❤️ Her türlü katkıya açığız: hata düzeltmeleri, yeni özellikler, dokümantasyon iyileştirmeleri ve daha fazlası.

## 📋 İçindekiler

- [Başlamadan Önce](#başlamadan-önce)
- [İlk Adımlar](#ilk-adımlar)
- [Branch Stratejisi](#branch-stratejisi)
- [Geliştirme Ortamı](#geliştirme-ortamı)
- [Kod Standartları](#kod-standartları)
- [Commit Mesajları](#commit-mesajları)
- [Test](#test)
- [Pull Request Süreci](#pull-request-süreci)
- [Kontrol Listesi](#kontrol-listesi)
- [Önerilen Katkı Alanları](#önerilen-katkı-alanları)
- [İletişim](#i̇letişim)

## 🚀 Başlamadan Önce

Projeye katkıda bulunmadan önce şunları yapmanı öneririz:

1. [GitHub](https://github.com) hesabın olduğundan emin ol
2. Projenin [README.md](README.md) dosyasını oku
3. [SIK-SORULAN-SORULAR.md](SIK-SORULAN-SORULAR.md) dosyasını incele
4. Varsa [açık issue'ları](https://github.com/tda45/Chatter-LiveChat-PC/issues) kontrol et

## 🌱 İlk Adımlar

```bash
# 1. Projeyi fork et (GitHub web arayüzünden)

# 2. Forkladığın projeyi bilgisayarına klonla
git clone https://github.com/KULLANICI_ADIN/Chatter-LiveChat-PC.git
cd Chatter-LiveChat-PC

# 3. Ana repoyu upstream olarak ekle
git remote add upstream https://github.com/tda45/Chatter-LiveChat-PC.git

# 4. Güncellemeleri almak için
git fetch upstream
git checkout main
git merge upstream/main
🌿 Branch Stratejisi
Projemizde şu branch yapısını kullanıyoruz:

Branch	Amaç
main	Kararlı sürüm. Production'a hazır kod.
develop	Geliştirme branch'i. Yeni özellikler burada birleşir.
feature/*	Yeni özellikler için (örn: feature/yaziyor-bildirimi)
bugfix/*	Hata düzeltmeleri için (örn: bugfix/login-hatasi)
docs/*	Dokümantasyon güncellemeleri için (örn: docs/api-guncelleme)
Yeni Branch Oluşturma
bash
# Önce develop branch'ini güncelle
git checkout develop
git pull upstream develop

# Yeni feature branch'i oluştur
git checkout -b feature/ekleyecegin-ozellik
💻 Geliştirme Ortamı
Gereksinimler
.NET 8.0 SDK (zorunlu)

Visual Studio 2022 (önerilen) veya VS Code

Git

Node.js (web sitesi için)

Android SDK (mobil geliştirme için)

Projeyi Çalıştırma
bash
# Bağımlılıkları yükle
dotnet restore

# Projeyi derle
dotnet build

# Windows Forms uygulamasını çalıştır
dotnet run --project ChatterLiveChat

# MAUI uygulamasını çalıştır
dotnet run --project "Chatter-LiveChat Mobile"
Web Sitesini Çalıştırma
bash
cd Chatter-LiveChat-PC-Sitesi
# Basit bir HTTP sunucusu başlat
python -m http.server 8000
# veya
npx http-server
📐 Kod Standartları
C# Kod Standartları
Microsoft C# Kodlama Kuralları'nı takip edin

İsimlendirme:

PascalCase - Sınıf, metot, property isimleri

_camelCase - Private field'lar

camelCase - Yerel değişkenler, parametreler

using'ler: Alfabetik sırada ve gereksiz using'ler olmasın

✅ Doğru:

csharp
public class ChatService
{
    private readonly SupabaseHttpService _httpService;
    private string _currentUser;
    
    public async Task<bool> LoginAsync(string username)
    {
        // kodlar
    }
}
❌ Yanlış:

csharp
public class chatService
{
    private SupabaseHttpService httpService;
    private String CurrentUser;
}
XAML Standartları
Elementleri hizalayın

Property'leri alfabetik sırayla yazın

Event handler'ların sonunda olmasına dikkat edin

✅ Doğru:

xml
<Button x:Name="LoginButton"
        BackgroundColor="#B42828"
        Clicked="OnLoginClicked"
        CornerRadius="10"
        FontSize="18"
        HeightRequest="50"
        Text="Giriş Yap"
        TextColor="White" />
HTML/CSS Standartları
İndentasyon için 4 boşluk kullanın

Sınıf isimleri için kebap-case kullanın

CSS özelliklerini mantıksal gruplara ayırın

📝 Commit Mesajları
Commit mesajlarımız Conventional Commits standardını takip eder.

Format: <type>(<scope>): <description>

Type (Tür)
Type	Açıklama
feat	Yeni özellik
fix	Hata düzeltme
docs	Dokümantasyon değişiklikleri
style	Kod formatı (kod çalışmasını etkilemeyen değişiklikler)
refactor	Kod iyileştirme (yeni özellik eklemeyen)
perf	Performans iyileştirmeleri
test	Test ekleme veya düzeltme
chore	Yapılandırma, bağımlılık güncellemeleri
Scope (Kapsam) (opsiyonel)
Scope	Açıklama
winforms	Windows Forms uygulaması
maui	MAUI mobil uygulaması
web	Web sitesi
api	API/Supabase entegrasyonu
docs	Dokümantasyon
Örnekler
✅ İyi Commit Mesajları:

text
feat(chat): yazıyor bildirimi eklendi
fix(login): kullanıcı adı kontrolü düzeltildi
docs(readme): kurulum adımları güncellendi
style(winforms): kod formatı düzenlendi
test(api): mesaj gönderme testi eklendi
❌ Kötü Commit Mesajları:

text
güncelleme
düzeltme
bug fix
asdasd
🧪 Test
Test yazmak zorunlu değil ama çok değerli. Eğer test ekleyebilirsen harika olur!

Test Projesini Çalıştırma
bash
# Testleri çalıştır
dotnet test

# Belirli bir test filtresiyle çalıştır
dotnet test --filter "FullyQualifiedName~LoginTests"
Test Örneği
csharp
[TestClass]
public class ChatServiceTests
{
    [TestMethod]
    public async Task Login_ValidUsername_ReturnsTrue()
    {
        // Arrange
        var service = new ChatService();
        
        // Act
        var result = await service.LoginAsync("testuser");
        
        // Assert
        Assert.IsTrue(result);
    }
}
🔀 Pull Request Süreci
Adım Adım
Branch'ini güncelle

bash
git checkout develop
git pull upstream develop
git checkout feature/ozelligin
git rebase develop
Değişikliklerini test et

bash
dotnet build
dotnet test
Commit ve push yap

bash
git add .
git commit -m "feat: harika bir özellik eklendi"
git push origin feature/ozelligin
GitHub'da Pull Request aç

Base branch: develop

Head branch: feature/ozelligin

Açıklayıcı bir başlık ve açıklama ekle

Review sürecini bekle

En az bir maintainer onayı gerekli

CI testleri geçmeli

Gerekirse değişiklik isteklerini uygula

PR Şablonu
markdown
## 📝 Açıklama
Bu PR ile neler değişiyor? Kısaca açıklayın.

## 🔗 İlgili Issue
Fixes #123

## 🎯 Değişiklik Türü
- [ ] Yeni özellik (feat)
- [ ] Hata düzeltme (fix)
- [ ] Dokümantasyon (docs)
- [ ] Kod iyileştirme (refactor)
- [ ] Test (test)

## ✅ Kontrol Listesi
- [ ] Kod standartlarına uygun
- [ ] Kendi kodumu test ettim
- [ ] Dokümantasyonu güncelledim
- [ ] CHANGELOG.md güncellendi
- [ ] Conflict yok

## 📸 Ekran Görüntüleri
(Varsa ekleyin)

## 💬 Ek Notlar
(Varsa ekleyin)
✅ Kontrol Listesi
Pull Request göndermeden önce:

Kod standartlarına uygun mu?

Projeyi derleyip test ettin mi?

Yeni özellik eklediysen dokümantasyonu güncelledin mi?

Test ekledin mi? (mümkünse)

Commit mesajları kurallara uygun mu?

Branch'in güncel mi?

Conflict var mı?

README veya diğer dokümanlar güncellendi mi?

🎯 Önerilen Katkı Alanları
🐛 Hata Düzeltmeleri
GitHub Issues'daki bug etiketli işler

Kendi bulduğun hatalar

✨ Yeni Özellikler
Mobil uygulama geliştirme (Android/iOS)

Sesli mesaj desteği

Emoji desteği

Dosya paylaşımı

Özel mesajlaşma

Tema seçenekleri

📚 Dokümantasyon
README iyileştirmeleri

API dokümantasyonu

Kurulum rehberleri

Kod içi yorumlar

🌐 Web Sitesi
Yeni sayfalar

Tasarım iyileştirmeleri

Performans optimizasyonu

Mobil uyumluluk

🔧 Test
Birim testleri ekleme

Entegrasyon testleri

UI testleri

📞 İletişim
Soruların mı var? Çekinmeden ulaş!

GitHub Issues: Yeni issue aç

GitHub Discussions: Tartışmalara katıl

E-posta: tahadikbas45@gmail.com

🙏 Teşekkürler!
Katkıda bulunmayı düşündüğün için şimdiden teşekkürler! Her katkı, projeyi daha iyi bir yer yapıyor. ❤️

<div align="center"> <b>Haydi, başlayalım! 🚀</b> </div> ```
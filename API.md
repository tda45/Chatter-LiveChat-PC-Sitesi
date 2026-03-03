# 📡 Chatter-LiveChat API Referansı

Bu doküman, Chatter-LiveChat uygulamasının Supabase backend API'sini açıklar. Tüm istekler Supabase üzerinden yapılır.

## 📋 İçindekiler

- [Genel Bilgiler](#genel-bilgiler)
- [Kimlik Doğrulama](#kimlik-doğrulama)
- [Hata Kodları](#hata-kodları)
- [Mesajlar](#mesajlar)
- [Aktif Kullanıcılar](#aktif-kullanıcılar)
- [Realtime](#realtime)
- [Örnekler](#örnekler)
- [Postman Koleksiyonu](#postman-koleksiyonu)

## 🌐 Genel Bilgiler

| Özellik | Değer |
|---------|-------|
| Base URL | `https://zsspdxeovynnzrjalvvy.supabase.co/rest/v1` |
| Realtime URL | `wss://zsspdxeovynnzrjalvvy.supabase.co/realtime/v1` |
| API Format | REST + WebSocket |
| Veri Formatı | JSON |

## 🔑 Kimlik Doğrulama

Tüm REST isteklerinde `apikey` header'ı gönderilmelidir. Ayrıca `Authorization` header'ı da aynı değerle eklenebilir.

### Headers

```http
apikey: eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
Content-Type: application/json
Prefer: return=representation  // opsiyonel, eklenen kaydı döndürür
API Anahtarı
javascript
const supabaseUrl = 'https://zsspdxeovynnzrjalvvy.supabase.co';
const supabaseKey = 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJzdXBhYmFzZSIsInJlZiI6Inpzc3BkeGVvdnlubnpyamFsdnZ5Iiwicm9sZSI6ImFub24iLCJpYXQiOjE3NzIyODU5NzMsImV4cCI6MjA4Nzg2MTk3M30.9ahmXDGGbGNwvcaSEE40tXLb0A5_37UgdwiBWQyiAs8';
🚨 Hata Kodları
Kod	Açıklama
200	Başarılı
201	Kayıt oluşturuldu
400	Geçersiz istek
401	Yetkisiz (API anahtarı geçersiz)
404	Kaynak bulunamadı
406	Geçersiz format
500	Sunucu hatası
💬 Mesajlar
Mesaj Nesnesi
json
{
    "id": 1,
    "content": "Merhaba dünya!",
    "username": "ali",
    "created_at": "2026-03-03T12:00:00Z"
}
Alan	Tip	Açıklama
id	integer	Otomatik artan birincil anahtar
content	string	Mesaj içeriği
username	string	Mesajı gönderen kullanıcı
created_at	timestamp	Mesajın oluşturulma zamanı (UTC)
Mesaj Gönderme
Endpoint: POST /messages

İstek:

http
POST /messages HTTP/1.1
apikey: YOUR_ANON_KEY
Content-Type: application/json
Prefer: return=representation

{
    "content": "Merhaba!",
    "username": "ahmet",
    "created_at": "2026-03-03T12:00:00Z"
}
Başarılı Yanıt (201):

json
{
    "id": 42,
    "content": "Merhaba!",
    "username": "ahmet",
    "created_at": "2026-03-03T12:00:00Z"
}
Mesajları Listeleme
Endpoint: GET /messages

Parametreler:

Parametre	Açıklama	Örnek
select	Hangi alanların döneceği	select=* veya select=id,content
order	Sıralama	order=created_at.desc
limit	Maksimum kayıt sayısı	limit=50
offset	Atlanacak kayıt sayısı	offset=10
created_at	Tarih filtresi	created_at=gt.2026-03-01
Örnek İstek:

http
GET /messages?select=*&order=created_at.desc&limit=10 HTTP/1.1
apikey: YOUR_ANON_KEY
Yanıt (200):

json
[
    {
        "id": 42,
        "content": "Merhaba!",
        "username": "ahmet",
        "created_at": "2026-03-03T12:00:00Z"
    },
    {
        "id": 41,
        "content": "Selam",
        "username": "mehmet",
        "created_at": "2026-03-03T11:55:00Z"
    }
]
Belirli Tarihten Sonraki Mesajlar
Endpoint: GET /messages?created_at=gt.{tarih}

Örnek:

http
GET /messages?select=*&created_at=gt.2026-03-03T10:00:00Z&order=created_at.asc
Kullanıcının Mesajları
Endpoint: GET /messages?username=eq.{kullanıcı}

Örnek:

http
GET /messages?select=*&username=eq.ahmet&order=created_at.desc
👥 Aktif Kullanıcılar
Aktif Kullanıcı Nesnesi
json
{
    "username": "ali",
    "last_seen": "2026-03-03T12:00:00Z"
}
Alan	Tip	Açıklama
username	string	Kullanıcı adı (birincil anahtar)
last_seen	timestamp	Son görülme zamanı
Kullanıcı Ekleme (Giriş)
Endpoint: POST /active_users

İstek:

http
POST /active_users HTTP/1.1
apikey: YOUR_ANON_KEY
Content-Type: application/json

{
    "username": "ayşe",
    "last_seen": "2026-03-03T12:05:00Z"
}
Başarılı Yanıt (201):

json
{
    "username": "ayşe",
    "last_seen": "2026-03-03T12:05:00Z"
}
Kullanıcı Silme (Çıkış)
Endpoint: DELETE /active_users?username=eq.{kullanıcı}

Örnek:

http
DELETE /active_users?username=eq.ayşe HTTP/1.1
apikey: YOUR_ANON_KEY
Aktif Kullanıcıları Listeleme
Endpoint: GET /active_users?last_seen=gt.{zaman}

Örnek (son 10 saniye):

http
GET /active_users?select=username&last_seen=gt.2026-03-03T12:04:50Z
Yanıt (200):

json
[
    { "username": "ahmet" },
    { "username": "mehmet" }
]
LastSeen Güncelleme
Endpoint: PATCH /active_users?username=eq.{kullanıcı}

Örnek:

http
PATCH /active_users?username=eq.ahmet HTTP/1.1
apikey: YOUR_ANON_KEY
Content-Type: application/json

{
    "last_seen": "2026-03-03T12:10:00Z"
}
Eski Kullanıcıları Temizleme
Endpoint: DELETE /active_users?last_seen=lt.{zaman}

Örnek (10 saniyeden eski):

http
DELETE /active_users?last_seen=lt.2026-03-03T12:04:50Z
🔄 Realtime
Realtime bağlantısı WebSocket üzerinden yapılır.

Bağlantı Kurma
javascript
const ws = new WebSocket('wss://zsspdxeovynnzrjalvvy.supabase.co/realtime/v1');

ws.onopen = () => {
    console.log('Bağlantı kuruldu');
    
    // Kanala abone ol
    ws.send(JSON.stringify({
        type: 'channel_join',
        channel: 'messages'
    }));
};

ws.onmessage = (event) => {
    const data = JSON.parse(event.data);
    console.log('Yeni mesaj:', data);
};
Kanala Abone Olma
json
{
    "type": "channel_join",
    "channel": "messages",
    "payload": {
        "config": {
            "broadcast": { "self": true }
        }
    }
}
Yeni Mesaj Bildirimi
json
{
    "type": "broadcast",
    "event": "message",
    "channel": "messages",
    "payload": {
        "id": 43,
        "content": "Yeni mesaj",
        "username": "zeynep",
        "created_at": "2026-03-03T12:15:00Z"
    }
}
💻 Örnekler
C# ile Mesaj Gönderme
csharp
using System;
using System.Net.Http;
using System.Text;
using Newtonsoft.Json;

public async Task SendMessageAsync(string content, string username)
{
    using var client = new HttpClient();
    
    client.DefaultRequestHeaders.Add("apikey", supabaseKey);
    client.DefaultRequestHeaders.Add("Authorization", $"Bearer {supabaseKey}");
    
    var message = new
    {
        content = content,
        username = username,
        created_at = DateTime.UtcNow
    };
    
    var json = JsonConvert.SerializeObject(message);
    var httpContent = new StringContent(json, Encoding.UTF8, "application/json");
    
    var response = await client.PostAsync($"{supabaseUrl}/rest/v1/messages", httpContent);
    
    if (response.IsSuccessStatusCode)
    {
        Console.WriteLine("Mesaj gönderildi!");
    }
}
JavaScript ile Aktif Kullanıcıları Listeleme
javascript
async function getActiveUsers() {
    const tenSecondsAgo = new Date(Date.now() - 10000).toISOString();
    
    const response = await fetch(
        `${supabaseUrl}/rest/v1/active_users?select=username&last_seen=gt.${tenSecondsAgo}`,
        {
            headers: {
                'apikey': supabaseKey,
                'Authorization': `Bearer ${supabaseKey}`
            }
        }
    );
    
    const users = await response.json();
    console.log('Aktif kullanıcılar:', users.map(u => u.username));
}
Python ile Mesajları Okuma
python
import requests
import json

url = "https://zsspdxeovynnzrjalvvy.supabase.co/rest/v1/messages"
headers = {
    "apikey": "YOUR_ANON_KEY",
    "Authorization": "Bearer YOUR_ANON_KEY"
}
params = {
    "select": "*",
    "order": "created_at.desc",
    "limit": 10
}

response = requests.get(url, headers=headers, params=params)
messages = response.json()

for msg in messages:
    print(f"[{msg['created_at']}] {msg['username']}: {msg['content']}")
cURL ile Test
bash
# Son 10 mesajı getir
curl -X GET "https://zsspdxeovynnzrjalvvy.supabase.co/rest/v1/messages?select=*&order=created_at.desc&limit=10" \
  -H "apikey: YOUR_ANON_KEY" \
  -H "Authorization: Bearer YOUR_ANON_KEY"

# Yeni mesaj gönder
curl -X POST "https://zsspdxeovynnzrjalvvy.supabase.co/rest/v1/messages" \
  -H "apikey: YOUR_ANON_KEY" \
  -H "Authorization: Bearer YOUR_ANON_KEY" \
  -H "Content-Type: application/json" \
  -H "Prefer: return=representation" \
  -d '{"content": "cURL ile test", "username": "testuser", "created_at": "'$(date -u +"%Y-%m-%dT%H:%M:%SZ")'"}'
📮 Postman Koleksiyonu
API'yi test etmek için Postman koleksiyonu:

https://run.pstmn.io/button.svg

Environment Değişkenleri
Değişken	Değer
supabase_url	https://zsspdxeovynnzrjalvvy.supabase.co
supabase_key	eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
api_url	{{supabase_url}}/rest/v1
📊 Rate Limit
Supabase'in belirli bir rate limit'i yoktur ancak aşırı kullanım durumunda:

Anlık çok fazla istek atılırsa 429 Too Many Requests hatası alınabilir

İstekler arasında en az 100ms bırakılması önerilir

Polling için 2 saniye idealdir

📝 Değişiklik Geçmişi
Tarih	Versiyon	Değişiklik
2026-03-03	1.0	İlk versiyon
2026-03-01	0.9	Beta sürüm
<div align="center"> <b>📚 Daha fazla bilgi için <a href="BELGELER.md">BELGELER.md</a> dosyasını inceleyin</b> </div> ```
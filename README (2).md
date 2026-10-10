# 🏆 SoruLig

Soru çözdükçe rank atla. League of Legends tarzı lig sistemi (Demir → Challenger), animasyonlu fantastik çerçeveler,
başarım rozetleri, aylık sezonlar ve arkadaş grubuyla canlı liderlik tablosu.

Tek dosya (`index.html`), GitHub Pages'te ücretsiz yayınlanır. Arkadaş tablosu için ücretsiz Supabase kullanır.

---

## 1) Supabase kurulumu (ücretsiz, ~5 dk)

1. https://supabase.com adresinde hesap aç → **New project** (ücretsiz plan yeter, bölge: Frankfurt).
2. Proje hazır olunca soldan **SQL Editor → New query** aç, `supabase.sql` dosyasının içeriğini yapıştır, **RUN**'a bas.
3. **Authentication → Sign In / Providers** (eski adıyla *Providers*) bölümünde **"Allow anonymous sign-ins"** seçeneğini **aç**.
   (Kullanıcılar e-posta/şifre girmeden, tarayıcıya bağlı gizli bir kimlikle girer.)
4. **Project Settings → API Keys** sayfasından şunları kopyala:
   - **Project URL** (`https://xxxx.supabase.co`), bu bilgi **Project Settings → Data API** sayfasında da yazar
   - **Publishable key** (`sb_publishable_...`). Eski projelerdeki `anon` anahtarı da çalışır.

   Bu anahtar herkese açık olabilir, güvenliği az önce kurduğun RLS kuralları sağlar.
   **Secret key** (`sb_secret_...`) veya `service_role` anahtarını **asla** koyma.
5. `index.html` dosyasında en üstteki `CONFIG` bölümünü doldur:

```js
const CONFIG={
  SUPABASE_URL:"https://xxxx.supabase.co",
  SUPABASE_ANON_KEY:"sb_publishable_..."
};
```

## 2) GitHub Pages ile yayınlama

1. GitHub'da yeni bir repo aç (örn. `sorulig`), `index.html` ve `README.md` dosyalarını yükle.
2. Repo → **Settings → Pages** → *Source:* **Deploy from a branch** → *Branch:* `main` / `(root)` → **Save**.
3. 1–2 dakika sonra siten şurada olur: `https://KULLANICIADIN.github.io/sorulig/`
4. Linki arkadaşlarına gönder.

## 3) Arkadaşlarla kullanma

- İlk açılışta herkes **takma ad** ve **grup kodu** yazar. Aynı grup kodunu yazanlar birbirini görür
  (örn. `sinif-12a`). Kodu bilmeyen biri tabloyu göremez.
- Grup kodunu liderlik tablosunun altındaki **Kopyala** butonuyla paylaşabilirsin.
- Herkes sadece kendi skorunu değiştirebilir.

## Nasıl çalışıyor?

| Özellik | Detay |
|---|---|
| Puan | 1 soru = 1 puan, toplam sorun rank'ını belirler |
| Ligler | Demir, Bronz, Gümüş, Altın, Platin, Zümrüt, Elmas (her biri IV→I), Usta, Grandmaster, Challenger |
| Çerçeve | Her ligin kendine özel animasyonlu çerçevesi var (kanat, taç, alev, kristal, yörünge) |
| Başarımlar | 26 rozet: toplam soru, tek gün rekoru, seri, hedef, lig, sezon |
| Sezon | Her ay sıfırlanır. 300/600/1000 soruda Bronz/Gümüş/Altın kupa. Ay sonunda 1. olan 👑 taşır |
| Veri | Sadece tarih ve soru sayısı tutulur. Tarayıcı verisini silersen kimliğin sıfırlanır (aşağıya bak) |

## Bilmen gerekenler

- **Cihaz değiştirme:** Kimlik tarayıcıya bağlıdır. Telefon ve bilgisayardan ayrı girersen iki ayrı oyuncu olursun.
  Tek cihazdan kullanmanı öneririm. İstersen sonra e-posta ile giriş ekleyebiliriz.
- **Hile:** Arkadaş grubu için tasarlandı. Birisi tarayıcı konsolundan kendi skorunu elle değiştirebilir.
- **Ücretsiz plan:** Supabase ücretsiz projeleri 1 hafta hiç kullanılmazsa durdurabilir. Dashboard'dan tek tıkla geri açılır.
- Çevrimdışı mod: `CONFIG` boşsa uygulama sadece o cihazda çalışır (liderlik tablosu olmaz).

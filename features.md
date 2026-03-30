# Features (Kod Bazlı)

Bu belge, repodaki mevcut kodun sağladığı işlevleri **dosyalara dayanarak** özetler.

## 1) Uygulama / Teknoloji Özeti

- **Frontend:** React + Vite
- **AI:** Groq SDK (`groq-sdk`) (client-side)
- **Auth + Veri:** Supabase (`@supabase/supabase-js`)
- **Hava durumu:** Open‑Meteo (geocoding + current + 7 günlük tahmin)

## 2) Çalıştırma (Script’ler)

`package.json`:
- `npm run dev` (Vite dev server)
- `npm run build` (prod build)
- `npm run preview` (build preview)
- `npm run lint` (ESLint)

## 3) Uygulama Giriş Noktaları

- `src/main.jsx`
  - React root render
  - `App` bileşenini mount eder.

- `src/App.jsx`
  - Uygulamadaki hemen hemen tüm ekranlar, state’ler ve iş akışları burada.

## 4) Ekranlar / Routing Mantığı (Tek Sayfa State ile)

`App.jsx` içinde `ekran` state’i ile yönetilir:
- `loader`
  - Açılış loader ekranı (dönen dünya).
- `karsilama`
  - Giriş/Kayıt ekranı.
- `anasayfa`
  - Ana menü + analiz kartları + hava tahmini + üst bar.
- `giris`
  - Analiz için metin + opsiyonel lab değerleri formu.
- `yukleniyor`
  - Analiz yapılırken bekleme ekranı.
- `sonuc`
  - AI analiz sonucu ekranı.
- `gecmis`
  - Kullanıcı geçmiş analiz listesi.
- `forum`
  - Supabase destekli forum ekranı (liste + paylaşım).
- `sifreYenile`
  - Şifre yenileme (recovery) ekranı.
- `ayarlar`
  - Profil ayarları ekranı.

Not: Ekran geçişleri state ile yapılır; ayrı router yok.

## 5) Kimlik Doğrulama (Supabase Auth)

### Giriş/Kayıt/Çıkış
- **Kayıt:** `supabase.auth.signUp`
  - Kayıt sırasında kullanıcı metadata’sına bazı profil alanları yazılır.
  - Ayrıca `profiles` tablosuna `upsert` denenir.
- **Giriş:** `supabase.auth.signInWithPassword`
- **Çıkış:** `supabase.auth.signOut`
  - Çıkış event’inde `ekran` zorla `karsilama` yapılır.

### Oturum bootstrap + auth event dinleme
- `supabase.auth.getSession()` ile açılışta session bootstrap.
- `supabase.auth.onAuthStateChange(...)` ile auth event’leri yakalanır.

### Şifre Sıfırlama / Recovery
- Reset mail isteme: `supabase.auth.resetPasswordForEmail`
- Recovery linkinden giriş:
  - URL’de `code` varsa `supabase.auth.exchangeCodeForSession(code)`.
- Şifre güncelleme:
  - `supabase.auth.updateUser({ password })`

## 6) Misafir Modu

- `guestMode` state ile yönetilir.
- Misafir modda ana sayfa incelenebilir; bazı aksiyonlar login gerektirebilir.

## 7) Profil Bilgileri (Şehir / Bölge / Gizlilik / Telefon)

### Profil kaynağı
- Öncelik:
  - `profiles` tablosu (varsa)
  - Supabase `user_metadata` fallback

### Şehir/Bölge hesaplama
- `BOLGELER` sözlüğü
- `getBolge(sehir)` fonksiyonu

### Gizlilik (forumda şehir gösterimi)
- `gizlilik` boolean
  - Forumda şehir/ilçe gösteriminde davranışı etkiler.

## 8) Ayarlar Ekranı

`ekran === "ayarlar"`:
- **Şehir seçimi** (`SEHIRLER` listesinden)
- **Telefon (opsiyonel)**
- **"Şehrim bölgemle birlikte gözüksün"** checkbox
  - Kodda `gizlilik` ile ilişkilendirilir.

Kaydet:
- `supabase.auth.updateUser({ data: ... })` ile `user_metadata` güncellenir.
- `profiles` tablosuna `upsert` denenir.

## 9) Forum (Supabase)

- Liste çekme: `supabase.from("forum_posts").select(...).order("created_at", { ascending: false }).limit(50)`
- Mesaj gönderme: `supabase.from("forum_posts").insert({...})`
- Şu an sıralama:
  - **Kronolojik** (en yeni üstte).

Forum ekranı:
- Login olmayan kullanıcı:
  - Okuma serbest, paylaşım için giriş teşviki.
- Login olan kullanıcı:
  - Textarea + Paylaş butonu.

## 10) AI Analiz Asistanı

Analiz türleri:
- Toprak
- Sulama suyu
- Bitki hastalığı / zararlı

Girdi:
- Serbest metin
- (Toprak/su için) opsiyonel lab değerleri

Çalışma:
- `Groq` SDK ile model çağrısı
- Prompt içine:
  - Kullanıcının şehir/bölgesi
  - Mevcut hava durumu notu
  - Temkinli dil / IPM vurgusu (hastalık akışında)

Çıktı:
- JSON formatında sonuç beklenir.
- Sonuç ekranında parametre kartları + aksiyon listesi gösterilir.

## 11) Hava Durumu + Risk Etiketleri

- Kullanıcı şehir seçmişse:
  - Open‑Meteo geocoding ile enlem/boylam
  - Current weather + daily forecast çekilir
- 7 günlük kartlarda risk etiketleri:
  - Don
  - Aşırı sıcak
  - Şiddetli yağış
  - Fırtına

## 12) Geçmiş Analizler

- Analiz sonrası sonuç `gecmis` listesine eklenir.
- Persist:
  - Kullanıcı bazlı localStorage key ile saklanır.
- Geçmiş ekranında listeleme + tüm geçmişi temizleme.

## 13) UI/UX Detayları

- Basılma hissi:
  - `pressable` class’ı ile butonlarda aktif/press davranışı.
- Loader:
  - `globeSpin` animasyonu ile dönen dünya.
- Hata/başarı mesajları:
  - Auth ve recovery akışlarında kullanıcıya mesaj gösterimi.

## 14) Konfigürasyon / Ortam Değişkenleri

- Supabase (`src/supabaseClient.js`):
  - `VITE_SUPABASE_URL`
  - `VITE_SUPABASE_ANON_KEY`

- Groq:
  - `VITE_GROQ_API_KEY`

## 15) Firebase (Kullanılmıyor)

- `src/firebase.js` bir stub dosyası:
  - `isFirebaseReady = false`
  - `app/auth/db = null`

Bu repo şu an Firebase kullanmıyor.

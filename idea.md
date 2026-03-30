# TarlaSor

## Problem

Türkiye'deki küçük ve orta ölçekli çiftçiler, tarlalarında gördükleri sorunları — sararan yapraklar, kuruyan bitkiler, verimsizleşen toprak — ne olduğunu, neden olduğunu ve ne yapmaları gerektiğini bilmeden yaşıyor. Tarım uzmanına ulaşmak zaman alıyor, pahalı veya her bölgede mümkün değil. Lab sonucu olan çiftçi ise elindeki pH, EC, SAR gibi değerlerin ne anlama geldiğini yorumlayamıyor.

## Kullanıcı

Türkiye'de küçük ve orta ölçekli araziye sahip çiftçiler. Akıllı telefonu var ancak teknik tarım bilgisi yok. İki farklı şekilde uygulamaya gelebilir:

- **Belirti ile gelenler:** "Yapraklarım sararıyor", "sulama yaptıkça daha da kötüleşiyor" gibi gözlemlerini anlatır veya fotoğraf çeker.
- **Lab sonucu ile gelenler:** Elinde toprak veya su test raporu var ama pH, EC, SAR gibi değerlerin ne anlama geldiğini bilmiyor, değerleri girer.

## AI'ın Rolü

Kullanıcının anlattığı belirtileri, çektiği fotoğrafı veya girdiği test değerlerini — ya da bunların kombinasyonunu — analiz ederek sade Türkçeyle üç soruyu yanıtlar:

1. **Ne oluyor?** — Toprağında veya bitkinde büyük ihtimalle şu problem var.
2. **Neden oluyor?** — Sebebi bu.
3. **Ne yapmalısın?** — Bu hafta şunu yap. Ucuz, erişilebilir, uygulanabilir adımlar.

Teknik terim yok. Sensör gerekmez. Kağıt zorunluluğu yok. Sadece telefon yeterli.

## Rakip Durum

| Rakip | Ne Yapıyor | Eksikliği |
|---|---|---|
| Soilo | AI toprak analizi, gübre önerisi | Donanım bağımlı, Türkçe yok |
| Soil Test Pro | Lab entegrasyonu, hassas tarım | ABD odaklı, belirti girişi yok |
| KETOS | Su kalitesi izleme | Kurumsal, pahalı donanım gerektirir |
| SQAPP | Harita tabanlı toprak analizi | Konum bazlı, kullanıcı girişi yok |

**Farkımız:** Hiçbir rakip Türkçe olarak hem belirti anlatımını  Hem de lab sonucunu birleştirip sade bir eylem önerisi sunmuyor. TarlaSor'da donanım, abonelik veya teknik bilgi gerekmez — çiftçi ne biliyorsa onu anlatır, AI geri kalanını yapar.

## Başarı Kriteri

Türkiye'deki bir çiftçi, tarlasında gördüğü sorunu telefona anlatarak veya fotoğraf çekerek 1 dakika içinde "büyük ihtimalle şu problem var, şunu yap" cevabını alabiliyorsa proje başarılıdır.

# InterviewHub MVP Görev Listesi

## 0. Tanım ve Başarı Kriteri
- [ ] `prd.md`’deki akışı ve MVP kapsamını netleştir (şirket/pozisyon/deneyim filtresi -> simülasyon -> rapor).
- [ ] “Hatasaız simülasyon başlatma” için zorunlu alanlar ve doğrulama kuralları belirle.
- [ ] “AI geri bildirimi” için raporda görünecek asgari bölümleri (güçlü/zayıf yönler, somut gelişim önerileri) yaz.

## 1. Proje Kurulumu (İskelet)
- [ ] Tech stack için karar ver (ör. Next.js/React + API katmanı veya tek uygulama).
- [ ] Proje klasör yapısını ve modülleri oluştur (UI, API/client, veri, entegrasyonlar).
- [ ] `.env.example` ekle (Gemini API key, ortam URL’leri vb.).
- [ ] Lovable/GitHub yayın akışını MVP düzeyinde hazırlamaya uygun hale getir (build komutları, environment mapping).

## 2. Veri Modeli: Soru Havuzu
- [ ] Dinamik soru havuzu için şema tasarla:
  - Şirket adı, pozisyon, deneyim seviyesi
  - Soru metni
  - İdeal cevap(lar) ve değerlendirme ölçütleri (rubric) (en az MVP için 1 set)
- [ ] MVP için başlangıç veri kaynağı seç (JSON/seed dosyası ile başlat; sonra DB’ye geçişi planla).
- [ ] `seed` verisi ekle (en az 1 şirket + 1 rol + 2-3 soru senaryosu).

## 3. Filtreleme ve Soru Seçimi
- [ ] Kullanıcının seçtiği filtrelere göre soru havuzundan listeleme mantığı kur.
- [ ] Her simülasyon için soru seçimini deterministik/yarı deterministik yap (örn. rastgele ama tekrar etmeyen seçim).
- [ ] “Filtre -> simülasyon başlasın” için boş sonuç senaryolarını ele al (kullanıcıya mesaj, fallback seed).

## 4. Backend API (Önerilen Minimum)
- [ ] API uç noktalarını tanımla ve uygula:
  - `POST /api/simulations/start` (filtreler + session id)
  - `POST /api/questions/next` (son mesaja göre sıradaki soru)
  - `POST /api/grade/response` (kullanıcı yanıtı + ideal/rubric -> skor + geri bildirim)
  - `POST /api/reports/finalize` (tüm oturumun özeti)
- [ ] Request/response şemalarını netleştir (frontend ile uyum).

## 5. Gemini Entegrasyonu (AI Sohbet)
- [ ] Gemini için `system prompt` tasla (mülakat atmosferi, rol, değerlendirme hedefleri, dil/tone).
- [ ] Soru üretimi için prompt yaklaşımını belirle:
  - Şirket/pozisyona uygun
  - Kullanıcının seviyesine uygun zorluk
  - Tek tek sorular (chat akışına uyumlu)
- [ ] Yanıt değerlendirmesi için prompt yaklaşımını belirle:
  - İdeal cevap/rubric ile karşılaştırma
  - Güçlü/zayıf yönler
  - Somut “bir dahaki sefere şunu yap” önerileri
- [ ] Hata yönetimi ekle (rate limit, geçersiz filtre, Gemini timeouts).

## 6. UI: Kullanıcı Akışı Ekranları
- [ ] `Home/Start` ekranı:
  - Şirket adı, pozisyon, deneyim seviyesi seçimi
  - Validasyon ve “Simülasyonu Başlat” butonu
- [ ] `Interview Chat` ekranı:
  - AI tarafından gelen sorular ve kullanıcı mesajları
  - Sıradaki soru akışı (kullanıcı yanıtından sonra otomatik)
  - Oturum durumu (başlatıldı / bitiyor)
- [ ] MVP için “yazılı yanıt”ı tamla; sesli giriş gerekiyorsa ayrı görev olarak işaretle (sonradan).

## 7. Oturum Durumu ve Veri Toplama
- [ ] Her simülasyon için session state yönet:
  - kullanıcı mesajları
  - AI soruları
  - her yanıtın ara skorları
- [ ] Simülasyon bitiş koşulu belirle:
  - örn. N soru sonunda raporu üret
- [ ] “Restart/yeniden başlat” opsiyonunu MVP’ye eklemeyi değerlendir.

## 8. Raporlama (Final Screen)
- [ ] Rapor tasla (en az MVP):
  - Genel performans özeti (kısa)
  - Güçlü yönler (madde madde)
  - Zayıf yönler / gelişim alanları (madde madde)
  - Somut öneriler (ör. STAR yaklaşımı, teknik derinlik, örnek yapı)
- [ ] Raporu AI sonuçlarından üret ve UI’da düzgün formatla.
- [ ] İçerik tutarlılığı için aynı dili/tonu koru.

## 9. Test ve Kalite Güvencesi
- [ ] Soru filtreleme için birim test (boş sonuç, fallback, doğruluk).
- [ ] Gemini entegrasyonu için “prompt format” testleri (mock ile).
- [ ] E2E akış testi:
  - filtreleri gir -> sim başlasın -> en az 1-2 soru/yanıt turu -> rapor ekranı gelsin
- [ ] Üretim kullanımına yönelik temel loglama (hata yakalama, session id).

## 10. Deployment / Yayınlama
- [ ] Gemini API key ve ortam değişkenlerini üretim ortamına bağla.
- [ ] Lovable/GitHub yayın adımlarını tamamla (build, start, domain).
- [ ] Basit bir demo senaryosu hazırlayıp doğrula (örnek filtre seti).

## 11. MVP Sonrası (Opsiyonel, Sonraya Bırak)
- [ ] Topluluktan “ideal cevap” toplama (upload formu / admin paneli).
- [ ] Rubric ve ideal cevap kalitesini artırmak için moderasyon/versiyonlama.
- [ ] Sesli yanıt (speech-to-text) entegrasyonu.
- [ ] Kullanıcı profili ve geçmiş simülasyonlar (history).

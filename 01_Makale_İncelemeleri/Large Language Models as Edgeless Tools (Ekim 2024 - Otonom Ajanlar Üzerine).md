---
tarih: 12-05-2026
yazarlar: Microsoft Research / Carnegie Mellon University
konu: otonom ajanlar
okunma_durumu: Tamamlandı
makale_linki: https://arxiv.org/abs/2410.12345
github: https://github.com/microsoft/autogen
---

# 📄 [Large Language Models as Edgeless Tools (Ekim 2024 - Otonom Ajanlar Üzerine)]

## TL;DR (1 Dakikalık Özet)
- LLM'ler ile gerçek dünyada bir etki tepki mekanizması kurarak LLM'lerin gerçek dünyada işler yapabilmesini sağlıyor.
- Genel olarak LLM'lere  çeşitli araçları kullandırtmayı öğretiyoruz,  bu araçlar bi robot kolu da olabilir bir banka API'si de olabilir 


---

## 1. Çözülen Problem (Neden Çıktı?)
- LLM ler birer chatbot olarak kulanılıyordu ama aslında bu chatbotlar kendi çıktılarını analiz ederek bazı sorunları çözebilirdi .
- Robotlar sensörleri kolları ile gerçek dünyada hata yapabilir ama düşünemezler llm'ler ise düşünebilir ama bu düşünceyi uygulayabilecekleri kolları uzuvları yoktur.
- Tam da bu iki parçayı birleştirme sayesinde robotlara beyin olarak llm leri eklersek robotlar daha akıllı hameleler yapabilirler bu makale temelde bunu çözüyor
- Bu makalede fiziksel olarak anlaşılması kolay olsun diye robot kullanılmış  ama temel olarak burda amaç LLM'e araç kullandırtmak bu API de olabilir .
![[Pasted image 20260512125247.png]]


## 2. Mimari ve Benim Anladıklarım
Model nasıl çalışıyor? 
-  Robotun hareketleri sonucu sensörler veri kaydeder, sensör loglarını yada verilerini arka planda  [[DOM ağacını)]] ile okuyoruz ve  LLM'e yorumlatıyoruz , eğer robot bir hata  yaparsa onu düzeltmek için yada yapması gereken bir işlem varsa onu llm ortaya çıkarıyor ve bunu robota sensörler motorlar aracılığıyla yaptırıyor.
- Eğer bu işlem sonucunda bir hata oluşursa sistem döngü olarak algılama-yorumlama-aksiyon işlemlere döngüsel olarak devam ediyor .
- Örneğin kullanıcı elindeki kırmızı topu mavi potaya at dediği zaman robotun kamerasından gelen veriyi LLM analiz ediyor ve kırmızı topu  mavi potaya atmak için topu sağa doğru atması gerektiğine karar veriyor ve bunu da robota bildiriyor , diyelim ki robot da topu attı ama top potaya girmedi bu durumda da DOM ile izleyip yeni durum değerlendirirliyor ve istenen karşılanana kadar işlemler bu sıra ile devam ettiriliyor.
- Aslında bunu geleneksel yöntemde if-else ile yapabilirdik ama gerçek dünyada zorlu ortamlarda tüm durumları önceden bilemeyiz.
- Matematiksel olarak ise *seçilen eylem* ,*robotun uzuvlarına* ,*sistemin o anki durumuna*, *ulaşılmak istenen hedefe*  *geçmişte yapılan hareketlere tecrübelere* ve *LLM in kendisine bağlıdır formülde bunlar yer alır *

- ![[Pasted image 20260512121720.png]]

- Robot bir adım atmadan önce seçenekleri değerlendirir ($\arg\max$). Kameranın gördüklerini ($s_t$), amacı ($G$) ve az önce duvara çarptığı bilgisini ($H_t$) modele (LLM - $\theta$) veririz. Model de bize, en yüksek başarı ihtimali olan yeni motor/API komutunu ($a_t$) döndürür.
## 3. Pratik Entegrasyon (Nerede Kullanırım?)
Bu yöntemi kendi projelerimde nasıl kullanabilirim? Kodlanabilir mi?
- **Senaryo:**genel olarak gecikme süreçlerinin çok da önemli olmadığı ama olasılıkların tek tek belirlemenin zor olduğu durumlarda kullanılabilir
- Örneğin bir e ticaret sitesine gelen iade süreçlerini yönetme işleminde  ajan talebi alır  arka planda veritabanı APİ'sine bağlanır sipariş numarasını bulur ,kargo firmasına bağlanıp iade kodu üretir son olarak banka apisi ile para iadesini başlatır ve müşteriye açıklamalı geri dönüş sağlar bu tarz işlerde kullanılabilir 

## 4. Eleştiri ve Zayıf Yönler

- Normalde hata çözme işi milisaniyeler içinde olmalıdır ama LLM den cevap gelmesi bunların uygulanması gibi işlemlerle muhtemelen bu çok fazla gecikme yaratır .ama eğer [[DeepSeek-V3 Technical Report (Aralık 2024)]] gibi çok daha hızlı modeller geliştirir ve üstüne ağ gecikmelerini de 5G ile azaltabilirsek bu sistem daha verimli olabilir.
- Yada şu da olabilir , LLM kötü niyetli olursa bazı zararlara yol açabilir burda çok sıkı bir güvenlik sağlanmalı LLM den çıkan her cevap uygulanmamalı yada LLM bu tarz sonuçlar üretmemli.

---
**İlgili Kavramlar:** #yapayzeka #makale
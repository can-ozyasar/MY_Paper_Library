---
tarih: 11-05-2026
yazarlar: DeepSeek-AI
konu:
okunma_durumu: Tamamlandı
makale_linki: arXiv:2412.19437
github kod: deepseek-ai/DeepSeek-V3
---

# 📄 [DeepSeek-V3 Technical Report]

## 💡 TL;DR (1 Dakikalık Özet)
- Bu makale neyi çözüyor? 
- Öncelikle ilk çıktığı zaman çok büyük bir etki yaratmıştı bunun en temel sebebi ise çok düşük maliyetlere çok iyi işler çıkaran bir model olarak karşımıza çıkmasıydı. 
- Daha iyi modeller rakiplerinde vardı ama bu inanılmaz düşük bütçe ile geliştirilmiş modeldi kısacası fiyat performans oranı çok iyiydi bu modelin rakipleri aynı modeli çok daha pahalıya yapabiliyorlardı
- Temelde 2 şeyi çözdü  bunlardan ilki rakipleri gibi tüm parametrelerini gereksiz kullanmıyordu ikinciside bağlamı saklama yöntemini daha verimli hale getirdi 5.5 milyon dolara yapabildi normalde 100 milyonlarca dolar civarı ederdi .

---

## 🎯 1. Çözülen Problem (Neden Çıktı?)
- Temelde iki büyük sorun vardı rakiplerde;
- Bunlardan ilki bir promt girince her kelime için klasik yöntemde modeldeki tüm sinir ağları çalışıyordu bu da ekstra gereksiz yere işlemci gücü (gpu) sarfiyatı demekti
- İkinci sorun ise modeleller uzun konuşmalarda bağlamı hatırlamak için herşeyi büyük matrislerle tutuyorlardı ve buda hem çokça bellek gerektiriyordu birde olan bellek hemen doluyordu bu da diğer bir kısıttı


## 🏗️ 2. Mimari ve Benim Anladıklarım
Model nasıl çalışıyor? 
- ilk başta girdiğimiz promt  [embeding] işlemi sonucu matematiksel vektörlere dönüşür
- vektörler standart [attention] mekanizması yerine [MLA (Multi-head Latent Attention)] burada tüm geçmişi devasa matrisler yerine gizli bir sıkıştırma alanıında [latent space]  tutulur ve bu sayede yer kazanılır.
- sonraki adımda [DeepSeekMoE] katmanında modelin içinde yüzlerce uzman kelimeleri çalışması gereken ağlara aktararır sadece seçilen o uzmanlar çalışır.diğer kısımlar gereksiz çalışmamış olur
- fark yaratan detay normalde yük dengeleme ile router hep aynı zeki uzmanlara işi vermek ister bu da diğer ağları tembelleştirir klasik yöntemde ek kayıp cezası  verirlirdi ki model en zekiye gitmeyi kessin bu da modelin başarısını azaltır modele gürültü eklediğimiz için. ama deepseek v3 de [Auxiliary-Loss-Free" (Ek Kayıpsız)] yöntemi ile dinamik atama yapıyor ve belli bir uzmana yüklenmeyi engelliyor bu da ceza vermeye gerek bırakmıyor.
- temel olarak mimaride normalde kaç parametrelik bir modeliniz varsa girdiğiniz promt sonucu tüm sinir ağları çalışıyordu Deepseek v3 te ise [Mixture-of-Experts" (MoE - Uzmanların Karışımı)]  mimarisi  içinde yüzlerce küçük uzman ağ vardır ve bunlar bi yönlendirici gibi gelen promttaki o anki kelimenin hangi sinir ağlarına gideceğine karar verir her kelime için sadece gerekli ve ilintili 37 milyar parametre aktif çalışıyor.

![[Pasted image 20260511210653.png]]


## 💻 3. Pratik Entegrasyon (Nerede Kullanırım?)
Bu yöntemi kendi projelerimde nasıl kullanabilirim? Kodlanabilir mi?
- **Senaryo:**
- örneğin bir projede bir girişi için tüm kaynakları kullanılmasını istemezsek ve bunu kullanmak gereksiz kaynak israfı ise bu problemin çözümüne benzer bir yönlendirme işlemi kullanabiliriz.
- **Araçlar:**

## ⚠️ 4. Eleştiri ve Zayıf Yönler
bu mantık gerçekten zamanında çok ses getirmişti ve ende projelerimde bu mantık yaklaşımını kullanacağım şuan nasıl bir zayıf yönü var emin değilim

---
**İlgili Kavramlar:** #yapayzeka #makale #DeepSeekV3 #hafizaProblemi #sinirliGPU #kaynakPAylasimi 
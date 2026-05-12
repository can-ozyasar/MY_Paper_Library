---
tarih: 12-05-2026
yazarlar: Stanford University / Meta AI
konu:
okunma_durumu: Tamamlandı
makale_linki: https://arxiv.org/pdf/2501.05678
---

# 📄 [Scaling Laws for Precision: Reasoning at the Edge (Ocak 2025)]

## TL;DR (1 Dakikalık Özet)
- Bu makale neyi çözüyor? 
- Modeller her token için aynı bellek miktarını kullanır örneğin FP16 da her token 16 bit ile ifade ediyordu bu da bazı kelimeler için gereğinden fazla bellek kullanmak demekti
- Makale genel olarak LLM lerin iot cihazlarında yada telefonlarda çalışması için bu bellek kullanımını aynı oranda sıkıştırmada LLM in bazı karmaşık işlerde performans kaybetmesi problemine odaklandılar
- Bunu da aynı insanın merhaba nasılsın kelimesi ile ail şuan x yaşındadır babası ona y tl verirse ... diye başlayan mantıksal cümleleri anlamak için beyninin sarfettiği o yakıtı ayarlaması mantığını LLM lere uyarladılar .
- Basit işlerde az bellek karmaşık işlerde yeterli bellek kullanarak çözdüler .


---

## 1. Çözülen Problem (Neden Çıktı?)
Promblem tam olarak şuydu LLM'leri düşük gereksinimli cihazlarda kullanmak istediğimizde bellek yetmiyordu sonra farkedildi ki bazı kelimeler için gereksiz bellek kullanıyoruz.bu makaledeki temel çözülen  probem buydu

## 2. Mimari ve Benim Anladıklarım
Model nasıl çalışıyor? 
- Kullanıcının yazdığı promt tokenlere bölünür bu tokenler o kelimenin tüm anlamsal derinliğini içeren matrisler halinde tutulur 
- Model bu matrislere bakarak sıkıştırma işlemini daha değersiz kelimelere az bellek daha önemli kelimelere ise daha fazla bellek vererek bu işlemleri optimize eder.
- Temelde tüm kelimelere yüksek bellek verme hatasına düşmemesi için sisteme bir ceza veririz ve hangi kelimeye he kadar bellek veremesi gerktiğini öğrenir .

## 3. Pratik Entegrasyon (Nerede Kullanırım?)
Düşük güçlü cihazlarda kullanılması için tasarlanmış bir optimizasyon yöntemidir bu alanlarda kullanılabilir. Veri gizliliği için telefonda model çalıştırmak isteyebiliriz.

## 4. Eleştiri ve Zayıf Yönler
- Modelleri her ne kadar edge cihazlarda kullanmak için INT2 gibi değerlere küçültsek de model temel konularda belki pek gözle görülür bir kayıp yaşamayabilir ama zorlu matematik mantık gibi alanlarda performansı çok fazla düşer  
- Telefonlarda bu işlemleri yapacak yani bir kelimeye int2 diğerine int8 verecek kadar hızlı stabil işlemciler geliştirmek gerekecek .
- Belkide en önemlisi bellek normalde tek tip veir ile dolacakken şuanda int2 int8 gibi değerlerle parçalı olarak kalacak bu da karmaşıklık yaratacak.
---
**İlgili Kavramlar:** #yapayzeka #EdgeCihaz #ModelSıkıstırma
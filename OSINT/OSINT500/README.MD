# eni kalbimin ortasından vurdun Pelinsu - OSINT 500


Sorunun son adımına çok erken ulaşmamıza rağmen ilk flagi bulan olamadık. Son adım biraz üzdü.

# Part 1: Exiftool önemli tabi

İlk olarak bir resim verildi.

![Alt text](kelebek.jpg)

Hemen aklımıza cicada3301'i getirdi. Daha önceden cicada 2014ü incelemiştim. Benzer adımlar çıkcağını bekleyerek çözmeye başladık.

Resimi indirdikten sonra exiftool attığımızda karşımıza bir link çıktı ```https://www.dkhos.com/m/missingpdf.jpg```
Linke gittiğimizde bu görselle karşılaştık

![Alt text](missingpdf.jpg)

# Part 2: Yav iyi güzel de Metin nerde

Ve direkt ampüller kafamızda belirdi. Cicada'daki gibi sayılar paragraf:kelime:harf numaralarına tekabül ediyordu. Alttaki soğan resmide .onion uzantısıydı.
Fakat elimizde harfleri alacağımız bir metin yoktu.
Hemen indirdiğimiz resime de bir exiftool attık.

Bu sefer Description ve Artist kısmı gözümüze çarptı. `Delft, Netherlands` ve `X9WG+8F`. Google mapse attıktan sonra çevredeki yerlerin reviewlerini incelemeye başladık.

![Alt text](rew.png)

```https://www.dkhos.com/m/delfthockey.pdf```

Exiftool atmaya o kadar alışmıştıkki daha onion linkini hesaplamadan buna da attık.

Daha önce başka ctflerde karşılaştığım için bunun bitcoin etherium vs bir hesap hashi olduğunu anladım.
Bir yere not ettik ve onion linkini hesapladık.

dkhosweozgoqjxxh.onion

![Alt text](onion.png)

# Part 3: I2P de neymiş yav

wallet_pass.zip isimli bir zip dosyası indirdik. Ancak "parola" isteniyordu. Önce hashi direk girmeyi denedik ama olmadı. Hemen bitcoin adresine gittik. Bir tane transaction vardı.

![Alt text](btc.png)


Bu sefer gönderilen hesabın hashini  `1DKHoSv7sTMJkCZPWn87dpBQFxw8rsTaH3` denedik ve zip açıldı.
İçinden hamata.zip.torrent isimli bir dosya çıktı.

İçgüdüsel olarak qbittorente yolladık hemen. Ancak dosya inmiyordu. Acaba teknik bi sorunmu diye düşündük.

![Alt text](i2p.png)

Torrentin trackerlarını incelemeye başladım.
i2p uzantısı farklı geldi ve google arattım.

https://geti2p.net/en/

Protokolün nasıl çalıştığını tam anlamasakta hemen kurduk.

![](torent.png)

![](ss.png)

Şimdiye kadar indirdiğimiz en hızlı torrentti sanırım :)

Zipin içinden 5 resim çıktı. Daha resimleri açmadan exiftool çaktık. Kordinat bilgilerini aldık ve tek tek  yazdık.

# Part 4: Aha da kalp

52°9'15.58"N 25°4'29.87"E

56°9'15.58"N 13°4'29.87"E

56°9'15.58"N 21°4'29.87"E

40°9'15.58"N 17°4'29.87"E

52°9'15.58"N 9°4'29.87"E

![Alt text](map.jpeg)

Kordinatları çok spesifik sayılardı.

Kağıda çizip düşünmeye başladık...

![Alt text](paper.jpeg)

Sorunun başlığını tekrar okuyunca orta noktaları hesapladık. Önce 56-40, 9,21 ikililerinin tam ortasını; 48,17'yi bulduk. O kordinata gittik. Çevredeki yerlerin reviewlerine baktık baktık ancak birşey çıkmadı. Street view'e geçtik ilginç bişeyler
varmı diye kolaçan ettik. Bir sonuca ulaşamadık. Acaba başka bir yoldan mı hesaplamamız gerekiyordu diye düşündük. Şekli Katı bir cisim gibi düşünüp ağırlık noktalarını çıkartmaya çalıştık.

(51.2,17) , (52,17) tek tek denedik hiç ilginç bir şeyle karşılaşmadık. Akşama doğru bizim çizdiğimiz şekle çok benzer şekilde bir ipucu yayınlandı. Anladık ki ilk hesapladığımız noktada bir yerde.
Reviewlerde olmadığına göre tek çare street viewdi. Tam o kordinatta  etrafınıza baktığınızda bir bina görüyorsunuz. Meğer o binanın üstündeki yazıymış.

![Alt text](al.png)

Flagde `Allexis` imiş. Son adım her ne kadar kafamızı duvarlara vurdurtsada çok büyük keyif aldık çözerken.

## Bu soruyu biz çözmüş olmayıp reponun amacı write-pack olmasindan dolayı eklenmiştir.

## Orjinal repo: https://github.com/eybisi/DKHOS/blob/master/CINT500.md

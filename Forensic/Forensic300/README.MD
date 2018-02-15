# Hadi hoppala vede cuppala - Forensic 300

```
Mahmut Pelinsu'nun eski bozuk harddisklerinden birine analiz çalışması yapar. Disk'in belirli bölümünden elde ettiği veriyi anlamlandırmaya çalışacaktır.
```
[Dosyayı Indir](./b8245152dfb2eb33ef32fbcf1c5af7ea6f6833f9)

Dosyaya `file` ile baktigimizda data diyordu bu yüzden dosyayı hex editor ile açmak durumunda kaldık


```
00000000  D9 1E BC AF 27 1C 00 04 49 15 DF 99 90 00 00 00  |Ù.¼¯'...I.ß.....|
00000010  00 00 00 00 00 00 00 00 00 00 00 00 25 F4 6E 69  |............%ôni|
00000020  F6 65 58 11 89 59 61 8D F6 13 2B 59 18 3E 0F 7B  |öeX..Ya.ö.+Y.>.{|
00000030  FE F0 C4 39 B4 10 46 DA 43 37 20 AE 9F 3A A2 8D  |þðÄ9´.FÚC7 ®.:¢.|
00000040  06 3A 02 64 98 84 6D E1 B2 E5 D3 F6 20 EE AD FC  |.:.d..má²åÓö î.ü|
00000050  03 56 52 00 91 B8 C2 BF 04 F5 02 7E 33 C7 E8 FC  |.VR..¸Â¿.õ.~3Çèü|
00000060  06 76 5E 93 D2 59 A9 D8 8B 4C CB C9 B9 CF 5E D5  |.v^.ÒY©Ø.LËÉ¹Ï^Õ|
00000070  DC 74 46 48 65 A0 EA D8 D9 1E 1D D8 E8 79 C1 C1  |ÜtFHe êØÙ..ØèyÁÁ|
00000080  49 FE FE 13 4D 78 57 AC 35 A4 30 79 CA 49 ED 4D  |Iþþ.MxW¬5¤0yÊIíM|
00000090  5F 99 9D 9D 69 C6 E5 76 9C FB D4 9F 75 54 17 DB  |_...iÆåv.ûÔ.uT.Û|
000000A0  85 D7 C7 93 BC 48 07 5C 5D 00 4B EB 8C DB B1 DC  |.×Ç.¼H.\].Kë.Û±Ü|
000000B0  17 06 20 01 09 70 00 07 0B 01 00 01 24 06 F1 07  |.. ..p......$.ñ.|
000000C0  01 0A 53 07 6B 7A A8 74 CD D4 2D 40 0C 6A 0A 01  |..S.kz¨tÍÔ-@.j..|
000000D0  AD 4D A3 8B 00 00                                |.M£...|
```
Burada birşey dikkatimizi çekti. `BC AF 27 1C` kısmı çok tanıdıktı google amcaya sorduk ve bize `7zip`'e ait olduğunu söyledi.

```
00: 6 bytes: 37 7A BC AF 27 1C        - Signature
06: 2 bytes: 00 04                    - Format version
```
Ve [böyle](http://www.7-zip.org/recover.html) bir link bulduk ve burada nasıl dosyayı kurtaracağımızı anlatıyordu. Hemen işe koyulduk. Signature kısmındaki `D9 1E BC AF 27 1C`'yı `37 7A BC AF 27 1C` olarak düzelttik. Ama dosya hala çalışmıyordu `00 04`'den sonra ki ( ilk `8` byte'tan sonraki ) 24 bytelık kısmı 0 lıyoruz

``` hexdump
00000000  37 7A BC AF 27 1C 00 04 00 00 00 00 00 00 00 00  |7z¼¯'...........|
00000010  00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00  |................|
00000020  F6 65 58 11 89 59 61 8D F6 13 2B 59 18 3E 0F 7B  |öeX..Ya.ö.+Y.>.{|
00000030  FE F0 C4 39 B4 10 46 DA 43 37 20 AE 9F 3A A2 8D  |þðÄ9´.FÚC7 ®.:¢.|
00000040  06 3A 02 64 98 84 6D E1 B2 E5 D3 F6 20 EE AD FC  |.:.d..má²åÓö î.ü|
00000050  03 56 52 00 91 B8 C2 BF 04 F5 02 7E 33 C7 E8 FC  |.VR..¸Â¿.õ.~3Çèü|
00000060  06 76 5E 93 D2 59 A9 D8 8B 4C CB C9 B9 CF 5E D5  |.v^.ÒY©Ø.LËÉ¹Ï^Õ|
00000070  DC 74 46 48 65 A0 EA D8 D9 1E 1D D8 E8 79 C1 C1  |ÜtFHe êØÙ..ØèyÁÁ|
00000080  49 FE FE 13 4D 78 57 AC 35 A4 30 79 CA 49 ED 4D  |Iþþ.MxW¬5¤0yÊIíM|
00000090  5F 99 9D 9D 69 C6 E5 76 9C FB D4 9F 75 54 17 DB  |_...iÆåv.ûÔ.uT.Û|
000000A0  85 D7 C7 93 BC 48 07 5C 5D 00 4B EB 8C DB B1 DC  |.×Ç.¼H.\].Kë.Û±Ü|
000000B0  17 06 20 01 09 70 00 07 0B 01 00 01 24 06 F1 07  |.. ..p......$.ñ.|
000000C0  01 0A 53 07 6B 7A A8 74 CD D4 2D 40 0C 6A 0A 01  |..S.kz¨tÍÔ-@.j..|
000000D0  AD 4D A3 8B 00 00                                |.M£...|
```

ve açmaya çalışıyoruz

```
~/foren300$ 7z x  b8245152dfb2eb33ef32fbcf1c5af7ea6f6833f9

7-Zip [64] 9.20  Copyright (c) 1999-2010 Igor Pavlov  2010-11-18
p7zip Version 9.20 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,4 CPUs)

Processing archive: b8245152dfb2eb33ef32fbcf1c5af7ea6f6833f9

Enter password (will not be echoed) :

```

tabiki şifre karşılıyoruz. DKHOS ta kolay birşey olur mu ve bruteforce yaptik ( tabi ki `rockyou` ile ) sifre `piggies` çıktı flagımız ;


```
DKHOS_{DKHOS_{4l_G1rd1n_g1rd1n}}
```

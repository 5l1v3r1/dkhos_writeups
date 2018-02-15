# Hafıza kaybı - Forensic 400

```

Pelinsu'nun odasında kilitli dolabı açan Mahmut sonunda Pelinsu'nun makinasına erişmiştir. Makina açıkken aldığı imaj üzerinde yeni ipuçları bulmak için çalışmaya koyulacaktır.

https://mega.nz/#!JhwU3ZrD!F2d3YoZ2O90S67qpIG5p5qO0sXox-EB6nXMR4pQ2H6E
```

Ram imaji oldugunu bildigimiz icin direk `volatility` araci ile imaja daldik.

`volatility -f for400.img  imageinfo` ile alakali profile baktik
```
~/Downloads$ volatility -f for400.img  imageinfo
Volatility Foundation Volatility Framework 2.5
INFO    : volatility.debug    : Determining profile based on KDBG search...
          Suggested Profile(s) : Win7SP0x86, Win7SP1x86
                     AS Layer1 : IA32PagedMemoryPae (Kernel AS)
                     AS Layer2 : FileAddressSpace (/home/th3-j4ck4l/Downloads/for400.img)
                      PAE type : PAE
                           DTB : 0x185000L
                          KDBG : 0x8296bc28L
          Number of Processors : 1
     Image Type (Service Pack) : 1
                KPCR for CPU 0 : 0x8296cc00L
             KUSER_SHARED_DATA : 0xffdf0000L
           Image date and time : 2018-01-29 08:42:45 UTC+0000
     Image local date and time : 2018-01-29 11:42:45 +0300

```
Alakali profil `Win7SP0x86` olarak önerildi `--profile Win7SP0x86` diyip işe koyulduk

`volatility -f for400.img --profile Win7SP0x86` pslist ile imajin processlerine baktik
```
Offset(V)  Name                    PID   PPID   Thds     Hnds   Sess  Wow64 Start                          Exit                          
---------- -------------------- ------ ------ ------ -------- ------ ------ ------------------------------ ------------------------------
0x8413a920 System                    4      0     86      488 ------      0 2018-01-29 08:22:12 UTC+0000                                 
0x8565ad40 smss.exe                268      4      2       29 ------      0 2018-01-29 08:22:12 UTC+0000                                 
0x85ea89e8 csrss.exe               352    340      9      468      0      0 2018-01-29 08:22:13 UTC+0000                                 
0x860fcd40 wininit.exe             404    340      3       74      0      0 2018-01-29 08:22:13 UTC+0000                                 
0x860fd5d8 csrss.exe               412    396     10      270      1      0 2018-01-29 08:22:13 UTC+0000                                 
0x86413d40 winlogon.exe            460    396      5      113      1      0 2018-01-29 08:22:13 UTC+0000                                 
0x86429a00 services.exe            504    404      7      210      0      0 2018-01-29 08:22:13 UTC+0000                                 
0x8643a780 lsass.exe               512    404      6      553      0      0 2018-01-29 08:22:14 UTC+0000                                 
0x86436ae0 lsm.exe                 520    404     10      145      0      0 2018-01-29 08:22:14 UTC+0000                                 
0x8646a510 svchost.exe             628    504     12      359      0      0 2018-01-29 08:22:14 UTC+0000                                 
0x864765a0 vmacthlp.exe            688    504      3       53      0      0 2018-01-29 08:22:14 UTC+0000                                 
0x861057d8 svchost.exe             720    504      8      271      0      0 2018-01-29 08:22:14 UTC+0000                                 
0x8575f260 svchost.exe             772    504     20      459      0      0 2018-01-29 08:22:14 UTC+0000                                 
0x8645d4e0 svchost.exe             888    504     13      304      0      0 2018-01-29 08:22:14 UTC+0000                                 
0x864bf030 svchost.exe             928    504     45     1226      0      0 2018-01-29 08:22:14 UTC+0000                                 
0x86507030 svchost.exe            1032    504     14      276      0      0 2018-01-29 08:22:14 UTC+0000                                 
0x8651ad40 svchost.exe            1100    504     17      478      0      0 2018-01-29 08:22:14 UTC+0000                                 
0x855d1d40 spoolsv.exe            1240    504     13      297      0      0 2018-01-29 08:22:14 UTC+0000                                 
0x8658f958 svchost.exe            1276    504     18      318      0      0 2018-01-29 08:22:14 UTC+0000                                 
0x865d8030 taskhost.exe           1444    504      8      185      1      0 2018-01-29 08:22:15 UTC+0000                                 
0x865f21d0 VGAuthService.         1468    504      3       86      0      0 2018-01-29 08:22:15 UTC+0000                                 
0x86575790 vmtoolsd.exe           1504    504      9      289      0      0 2018-01-29 08:22:15 UTC+0000                                 
0x866166f8 dwm.exe                1568    888      3       77      1      0 2018-01-29 08:22:15 UTC+0000                                 
0x8661d030 explorer.exe           1584   1540     29      883      1      0 2018-01-29 08:22:15 UTC+0000                                 
0x8551b510 vmtoolsd.exe           1792   1584      7      166      1      0 2018-01-29 08:22:15 UTC+0000                                 
0x866f75d8 TPAutoConnSvc.         1972    504      9      130      0      0 2018-01-29 08:22:16 UTC+0000                                 
0x865f4b90 WmiPrvSE.exe           1308    628     10      195      0      0 2018-01-29 08:22:16 UTC+0000                                 
0x86716030 SearchIndexer.         2220    504     14      627      0      0 2018-01-29 08:22:21 UTC+0000                                 
0x86809628 TPAutoConnect.         2440   1972      3      111      1      0 2018-01-29 08:22:26 UTC+0000                                 
0x86807030 conhost.exe            2448    412      1       33      1      0 2018-01-29 08:22:26 UTC+0000                                 
0x866f4030 svchost.exe            3776    504     11      134      0      0 2018-01-29 08:24:15 UTC+0000                                 
0x85704c58 sppsvc.exe             3808    504      4      144      0      0 2018-01-29 08:24:16 UTC+0000                                 
0x865cec18 svchost.exe            3844    504     14      345      0      0 2018-01-29 08:24:16 UTC+0000                                 
0x8677a030 msdtc.exe              3692    504     12      144      0      0 2018-01-29 08:32:39 UTC+0000                                 
0x843b0cb0 mscorsvw.exe           2400    504      5       75      0      0 2018-01-29 08:32:46 UTC+0000                                 
0x84357548 form.exe               2420   1584      5      132      1      0 2018-01-29 08:33:32 UTC+0000                                 
0x86721430 audiodg.exe            2940    772      6      132      0      0 2018-01-29 08:39:23 UTC+0000                                 
0x8677d958 svchost.exe            2944    504      5       62      0      0 2018-01-29 08:39:43 UTC+0000                                 
0x864a2c28 cmd.exe                2140   1584      1       18      1      0 2018-01-29 08:42:26 UTC+0000                                 
0x84348640 conhost.exe            2972    412      2       49      1      0 2018-01-29 08:42:26 UTC+0000                                 
0x85818168 dllhost.exe            2620    628      6       84      1      0 2018-01-29 08:42:45 UTC+0000                                 
0x8431c030 dllhost.exe            1672    628      6       81      0      0 2018-01-29 08:42:45 UTC+0000                                 
0x842f1c78 Memoryze.exe           4068   2364      2       97      1      0 2018-01-29 08:42:45 UTC+0000                                 
0x86466030 conhost.exe            3596    412      2       49      1      0 2018-01-29 08:42:45 UTC+0000                                 

```

Burada `form.exe` dikkatimizi çekti.
```
0x84357548 form.exe               2420   1584      5      132      1      0 2018-01-29 08:33:32 UTC+0000                                 
```

`volatility -f for400.img --profile=Win7SP0x86 filescan | grep form.exe` dosya yollari icerisinden  `form.exe` yi aradik

```
Volatility Foundation Volatility Framework 2.5
0x000000003fd2d298      7      0 R--r-d \Device\HarddiskVolume1\Users\home\Desktop\form.exe
```

`volatility -f for400.img --profile Win7SP0x86 dumpfiles -Q  0x000000003fd2d298 --dump-dir form/` ile form.exe'yi `form` klasörünün içine dump ettik.
```
Volatility Foundation Volatility Framework 2.5
ImageSectionObject 0x3fd2d298   None   \Device\HarddiskVolume1\Users\home\Desktop\form.exe
```

`binwalk` ile dosya içine bakmaya karar verdik
```
~/Downloads/form$ binwalk ./file.None.0x86415ca0.img

DECIMAL       HEXADECIMAL     DESCRIPTION
--------------------------------------------------------------------------------
13031         0x32E7          Copyright string: "CopyrightAttribute"
26819         0x68C3          Copyright string: "Copyright (c)  2018"
30080         0x7580          RAR archive data, first volume type: MAIN_HEAD

```
İçerşde bir rar dosyası olduğunu gördük ve `binwalk ./file.None.0x86415ca0.img  -e` ile çıkardık, fakat cikan `RAR` şifreliydi

```
~/Downloads/form/_file.None.0x86415ca0.img.extracted$ unrar x 7580.rar

UNRAR 5.30 beta 2 freeware      Copyright (c) 1993-2015 Alexander Roshal

Extracting from 7580.rar
Enter password (will not be echoed) for flag.txt:
```

Bizde imaja geri dönüp clipboard ve screenshootslara bakalım dedik belki birşey çıkar dedik

```
volatility -f for400.img --profile Win7SP0x86 clipboard
Volatility Foundation Volatility Framework 2.5
Session    WindowStation Format                 Handle Object     Data                                              
---------- ------------- ------------------ ---------- ---------- --------------------------------------------------
         1 WinSta0       0xc009L              0x34008b 0xfe4fee88                                                   
         1 WinSta0       CF_UNICODETEXT       0x4901f3 0xfe957520 OaX81_Nlrn                                        
         1 WinSta0       0xc013L              0x2402d5 0xfe5f6168                                                   
         1 WinSta0       CF_LOCALE            0x1f015d 0xfe9e1268                                                   
         1 WinSta0       CF_TEXT                   0x1 ----------                                                   
         1 WinSta0       CF_OEMTEXT                0x1 ----------
```
`OaX81_Nlrn` şifresidir diyip denedik  ve rardan flag.txt çıktı.

ve  flagimiz
```
DKHOS_{its_N0t_A_BuG_it_is_a_featuret}
```

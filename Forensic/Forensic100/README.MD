# Karanlıkta Arayış Başlar - Forensic 100

```
Pelinsu'nun kaybolmasının ardından Mahmut'un hayatı kararmıştı. Hiç zaman kaybetmeden düştüğü bu çaresiz durumda kendine gelmeli ve araştırmalarına başlamalıydı. Kaybedecek tek bir saniyesi yoktu ...
```
[Dosyayı Indir](./26b8351bdd03ce6d1d683bc38786aa3ea2432d45.mp4)

`grep` ile dosyanin içine baktık.

```
Forensic100$ grep -nai "flag" 26b8351bdd03ce6d1d683bc38786aa3ea2432d45.mp4
132:      stRef:filePath="flag.jpg"
```
sonra 132'ci satira gittik

```xml
<xmpMM:Ingredients>
 <rdf:Bag>
  <rdf:li
   stRef:instanceID="02d17d1d-c0c1-217d-4084-957400000068"
   stRef:documentID="4b1048e0-b00c-3347-ffa0-80860000003b"
   stRef:fromPart="time:0"
   stRef:toPart="time:3984383208960000f254016000000d10160640000f254016000000"
   stRef:filePath="flag.jpg"
   stRef:maskMarkers="None"/>
  <rdf:li
   stRef:instanceID="91d02011-6d0d-77cb-990e-54530000006a"
   stRef:documentID="5795f2a9-2a50-6d49-2fb8-c9000000003d"
   stRef:fromPart="time:0"
   stRef:toPart="time:0d1999766361600000f254016000000"
   stRef:filePath="black.jpg"
   stRef:maskMarkers="None"/>
  <rdf:li
   stRef:instanceID="91d02011-6d0d-77cb-990e-54530000006a"
   stRef:documentID="5795f2a9-2a50-6d49-2fb8-c9000000003d"
   stRef:fromPart="time:0"
   stRef:toPart="time:1999766361600000f254016000000d1984616847360000f254016000000"
   stRef:filePath="black.jpg"
   stRef:maskMarkers="None"/>
  <rdf:li
   stRef:instanceID="91d02011-6d0d-77cb-990e-54530000006a"
   stRef:documentID="5795f2a9-2a50-6d49-2fb8-c9000000003d"
   stRef:fromPart="time:0"
   stRef:toPart="time:3984393369600000f254016000000d3119316480000f254016000000"
   stRef:filePath="black.jpg"
   stRef:maskMarkers="None"/>
  <rdf:li
   stRef:instanceID="91d02011-6d0d-77cb-990e-54530000006a"
   stRef:documentID="5795f2a9-2a50-6d49-2fb8-c9000000003d"
   stRef:fromPart="time:0"
   stRef:toPart="time:3987512686080000f254016000000d1508143795200000f254016000000"
   stRef:filePath="black.jpg"
   stRef:maskMarkers="None"/>
 </rdf:Bag>
</xmpMM:Ingredients>

```

Zamanı belirtmişlerdi alakalı zamana gidince`3984383208960000f254016000000d10160640000f254016000000` flag karşımızdaydı

![](flag.png)
```
DKHOS{f1krim1n_1nc3_gulu}
```

> **Want to see 42 Quebec in 3D?**  
> **:arrow_right: https://mini42qc.vercel.app/ :arrow_left:**

# NetPractice Rehberi

![netpractice logo](img/NetPractice.png)
ceviri: emre akdik
<div id="top"></div>

## Diğer Diller

[Korean](README.ko.md)
<br>
[French](README.fr.md)
<br>
[English](README.md)

## İçerik Tablosu

- [Önemli Konseptler](#important-concepts)
  - [TCP](#tcp-transport-layer)
  - [IP address](#ip-address-network-layer)
  - [Subnet mask](#subnet-mask)
  - [Switch](#switch)
  - [Router](#router)
- [Leveller](#levels)

---

## Önemli Konseptler

### TCP: Transport Layer/Transfer Katmanı

</br>
<p align="center">
  <img src="./img/tcp-ip-stack.png" height=300 width=200 alt="mask">
</p>
</br>

TCP, **İletim Kontrol Protokolü anlamına gelir**. Bu uygulamaların ve cihazların bir ağda iletişim kurmalarını sağlayan bir standarttır. İnternet üzerinden paket gönderilmesini sağlar.

TCP, bir ağ üzerinden iletilen verilerin bütünlüğünü garanti eder.
Data teslim için gönderilmeden önce, TCP kaynak ve hedef arasında bir bağlantı oluşturur. Daha sonra bağlantı başlar ve TCP büyük paketleri küçük paketlere dönüştürerek uçtan uca teslim eder. Bunun sayesinde herhangi bir paket kaybı yaşanmaz.

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

---

### IP Address: Network Layer/Ağ Katmanı

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/ip1.png?raw=true" height=250 alt="mask"></kbd>
</p>
</br>

IP, iletim kontrol protokolünü de içeren bir internet protokol paketinin parçasıdır. Bu parçalar birlikte TCP/IP olarak bilinirler. İnternet protokol paketi, ağlar üzerinden verinin paketlenmesi, adreslenmesi, iletilmesi, yönlendirilmesi ve alınmasına ilişkin kuralları yönetir.

IP adreslemeyi basitçe, bir ağdaki bir cihaza IP ataması yapılması olarak açıklayabiliriz. İnternete bağlı olan her cihazın kendisine özgü bir IP adresine sahip olması zorunludur.

Bir IP adresinin iki parçası vardır; parçalardan biri cihazı yani host'u tanımlar, diğer parça ise bu cihazın ait olduğu ağı tanımlar. TCP/IP bu parçaları ayrıştırabilmek için [subnet mask/alt ağ maskesi](#subnet-mask) kullanır.
</br>
</br>

#### IPv4 vs. IPv6

IP adresleri iki versiyona sahiptir. Bunlar IPv4 ve IPv6 versiyonlarıdır.
<br>

<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/ip_version.png?raw=true" height=100 alt="ip_versions"></kbd>
</p>
<br>

Internet Protokolü versiyon 4 (IPv4) 32-bitlik sayılar ile tanımlanır. Fakat internetin büyümesi ile birlikte ve IPv4'teki müsait IP adresi sayısının tükenmeye başlaması ile birlikte, yeni bir versiyon olan ve 128 bit kullanan IPv6 adreslemesi 1998'de standartlaştırılmıştır. Bu konuya değinmiş olsakta, NetPractice projesinde sadece IPv4 kullanılıyor.
</br>
</br>

#### Public Address vs. Private Address

Public IP adresi, doğrudan internet üzerinden erişilebilen ve internet servis sağlayıcınız (mesela TTNET) tarafından ağ yönlendiricinize/modeminize atanan bir IP adresidir. Public address/Açık adres, evimizdeki lokal ağımızdan internete bağlanmamızı sağlayan IP adresidir.

Private address/Özel Adres yönlendiricimizin/modemimizin bize kendi ağımız içerisinde atadığı özel IP adresimizdir. Aynı ağdaki her cihaz kendisine özgü bir IP adresine sahiptir (bazen özel ağ adresi olarak geçebilir) - bunun sayesinde aynı ağın içindeki cihazlar birbirleriyle iletişim kurabiliyorlar.

Bir ağ internete bağlandığında özel/private IP adresleri için ayrılmış/rezerve edilmiş IP adreslerini kullanamazlar. Aşağıdaki IP aralıkları private IP adresleri için rezerve edilmiştir:

```
192.168.0.0 – 192.168.255.255 (65,536 IP addresses)
172.16.0.0 – 172.31.255.255   (1,048,576 IP addresses)
10.0.0.0 – 10.255.255.255     (16,777,216 IP addresses)
```

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

---

### Subnet Mask

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/mask1.png?raw=true" height=250 alt="mask"></kbd>
</p>
</br>

Subnet Mask yani alt ağ maskesi, bir IP adresindeki ağ adresini ve host adresini ayrıştırmak için kullanılan 32 bitten oluşan bir adrestir. Bir ağda veya alt ağda tanımlanabilecek IP adresi aralığını tanımlar.
</br>
</br>

#### Network/Ağ Adresini Bulmak

 _Interface A1_ aşağıdaki özelliklere sahiptir:

```
IP Adresi | 104.198.241.125
Maske       | 255.255.255.128
```

IP adresinin hangi bölümünün ağ adresi olduğunu belirlemek için IP adresine maske uygulamamız gerekir. Önce maskeyi ikili forma dönüştürelim:

```
Maske | 11111111.11111111.11111111.10000000
```

Bitlerdeki 1 olan kısımlar ağ adresinin temsil edildiği kısımlardır, geriye kalan 0'lar ise host adresinin temsil edildiği kısımlardır. Şimdi IP adresini ikili forma dönüştürelim:

```
IP address | 01101000.11000110.11110001.01111101
Mask       | 11111111.11111111.11111111.10000000
```

Şimdi ağ adresini bulabilmek için [bitwise AND](https://en.wikipedia.org/wiki/Bitwise_operation#AND) işlemi ile IP adresine maskeyi uygulayabiliriz:

```
Network address | 01101000.11000110.11110001.00000000
```

Bu işlem sonrası ağ adresi şu şekildedir: `104.198.241.0`.
</br>
</br>

#### Host Adreslerinin Aralığını Bulmak

Ağımızda hangi host adreslerini kullanabileceğimizi belirlemek için IP adresimizin host adresine ayrılmış bitlerini belirlememiz gerekir. Önceki kullandığımız IP adresimizi ve maskemizi kullanalım:

```
IP address | 01101000.11000110.11110001.01111101
Mask       | 11111111.11111111.11111111.10000000
```

Kullanmamız mümkün olan host adresı aralığı, maskedeki 0 olan son 7 bit olarak görünüyor. Öyleyse, host adresi aralığı aşağıdaki gibidir:

```
BINARY  | 0000000 - 1111111
DECIMAL | 0 - 127
```

Kullanılması mümkün olan IP adresi aralığını ortaya çıkarmak için ağ adresimize IP adresi aralığını ekleriz. Sonuç olarak mümkün olan IP adresi aralığımız şu şekilde sonuçlanır: `104.198.241.0 - 104.198.241.127`.

<ins>ANCAK</ins>, aralığın bazı kısımları özel olarak ayrılmıştır ve arayüzlere/cihazlara atanamaz:

```
104.198.241.0   | Ağ adresini tanımlamak için özel olarak ayrılmıştır.
104.198.241.127 | Ağdaki tüm cihazlara iletim yapılabilmesi için kullanılan broadcast adresi için özel olarak ayrılmıştır.
```

Böylelikle, gerçek IP adresi aralığımız `104.198.241.1 - 104.198.241.126` haline gelir, [IP calculator](https://www.calculator.net/ip-subnet-calculator.html) ile birlikte kolayca bu hesaplamalara ulaşabilirsiniz.
</br>
</br>

#### CIDR Notation (/24)

Maskeleme aynı zamanda Classless Inter-Domain Routing (CIDR) ile de gösterilebilir. Bu form "/" ile başlar ve sonrasında ağ adresi olarak tanımlanan bitlerin sayısıyla devam eder ve bu şekilde kullanılır.

Şöyle ki, `255.255.255.128` maskesinin, CIDR Notatıon karşılığı `/25`tir, yani bu 32 bitten 25 tanesinin 1 olduğunu ve ağ adresini tanımladığını söyler.

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

---

### Switch

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/switch1.png?raw=true" height=150 alt="switch"></kbd>
</p>
</br>

Bir switch bir ağın içindeki birden fazla cihazı birbirine bağlamaya yarar. Router'ın tersine switch herhangi bir arayüze sahip değildir, bir lokal ağ üzerinde paket dağıtımı yapar ve direkt olarak kendi başına internete bağlanamaz.

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

---

### Router

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/route1.png?raw=true" height=200 alt="router"></kbd>
</p>
</br>
router: yönlendirici

Switch birden fazla cihazı birbirine bağlarken, router birden fazla ağı birbirine bağlar. Router ona bağlanan her ağ için bir arayüze/interface sahiptir.

Router farklı ağları ayırdığından, arayüzlerinden birindeki olası IP adreslerinin aralığı diğer arayüzlerin aralığıyla çakışmamalıdır. IP adresi aralığındaki bir çakışma, arayüzlerin aynı ağ üzerinde olduğu anlamına gelir.
</br>
</br>

#### Routing Table

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/routing_table1.png?raw=true" height=150 alt="routing_table"></kbd>
</p>
</br>
routing table: yönlendirme tablosu

Yönlendirme tablosu, bir yönlendiricide veya host bilgisayarında saklanan ve belirli ağ hedeflerine giden adresleri listeleyen bir veri tablosudur. NetPractice'te yönlendirme tablosu 2 öğeden oluşur:
- **Destination**: Hedef (Destination), gönderilecek verinin hedefindeki hostun olduğu ağ adresini tanımlar. Default/Varsayılan veya `0.0.0.0/0` rotası hedef IP adress rotasından başka rota yoksa durumu etkilemez. Varsayılan rota, paketleri belirli bir hedef vermeden rotalarına göndermek için sonraki next-hope/atlama adresini kullanacaktır. Varsayılan rota herhangi bir ağ ile eşleşecektir.

- **Next hop**: Next hop, ağ içinde bir sonraki yönlendirici/router'ın adresini tutar. Her router yönlendirme tablosunu bir sıradaki router'a kadar olan hostlar ile sınırlar.

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

## Levels

<details>
  <summary>Level 1</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level1_paint.png?raw=true" alt="level1">  
  <br>
  <br>

**1.** Client _A_ ve Client _B_ aynı ağda oldukları için, IP adresleri subnet maskesi ile birlikte aynı ağı temsil etmelidir.
<br>
_255.255.255.0_, IP adresinin 3 byte'ının ağ adresini, 1 byte'ının ise host adresini gösterdiğini söyleyen bir subnet maskesidir. Aynı ağda olunduğu sürece sadece host kısmı değişebilir.
<br>
Çözüm, **104.96.23.0 - 104.96.23.255** aralığında olacaktır:

- **104.96.23.0:** Aralığın ilk adresi, ağ adresini temsil eder ve hostlara tanımlanamaz.
- **104.96.23.255:** Aralığın son adresi, broadcast adresi olarak tanımlıdır ve hostlara tanımlanamaz.
- **104.96.23.12:** Bu adres zaten _Client B_ hostuna tanımlanmıştır.

**2.** _1._ ile aynı mantık, ancak bu durumda alt ağ maskesi _255.255.0.0_'dır. IP adresinin ilk 2 baytı ağ adresini temsil edecektir; ve son 2 bayt,host adresidir.
<br>
Çözüm, **211.191.0.0 - 211.191.255.255** aralığındaki herhangi bir IP adresi olacaktır; ancak aşağıdakiler hariç:

- **211.191.0.0:** Ağ adresini temsil eder.
- **211.191.255.255:** Broadcast adresini temsil eder.
- **211.191.89.75:** Zaten _Client C_ hostu tarafından alınmış.

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Level 2</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level2_paint.png?raw=true" alt="level2">
  <br>
  <br>

**1.** _Client B_ ve _Client A_ aynı ağ içerisinde olduklarından, aynı subnet mask tanımlanmalıdır.
<br>
Çözüm ise sadece  **255.255.255.224** olabilir.

**2.** _255.255.255.224_ alt ağını anlamak için ikili formda inceleyelim, IP olarak ise _Client B_'nin _192.168.20.222_ IP adresini kullanalım:

<center>

```
MASK: 11111111.11111111.11111111.11100000
IP:   11000000.10101000.00010100.11011101
```

</center>
Gördüğümüz üzere ilk 27 bit ağ adresini tanımlarken, son 5 bit host adresini tanımlamaktadır.<br>
Tüm bu 27 bit ağ adresini tanımladığı için bu kısım aynı ağın içinde aynı kalmak zorundadır. Diğer bir deyişle sadece son 5 biti değiştirebiliriz.
<br>
<br>
Kullanılabilecek aralık ise:

```
BIN:  11000000.10101000.00010100.11000000 - 11000000.10101000.00010100.11011111
or
DEC:  192.168.20.192 - 192.168.20.223
```

Aşağıdakiler hariç:
<br>

- **11000000.10101000.00010100.11000000:** Ağ adresi için ayrılmıştır (son 5 bitin sıfır olduğuna dikkat edin).
- **11000000.10101000.00010100.11011111:** Broadcast ağını temsil etmektedir (son 5 bitin sıfır olduğuna dikkat edin).
- **11000000.10101000.00010100.11011110:** _Client B_ tarafından kullanılan IP adresi.

**3.** _Interface D1_'in alt ağ maskesi üzerinden slash kullandıgımız notasyonu anlamaya çalışalım. _/30_ olarak gösterilen bir alt ağ maskesi IP adresindeki 30 bitin ağ adresini temsil ettiği anlamına gelir ve geriya kalan 2 bit host adresi için değiştirilebilir.

<center>

```
Mask /30: 11111111.11111111.11111111.11111100
```

</center>

Yukarıdaki ikili formun onluk (decimal) gösteriminin  _255.255.255.252_ olduğunu görebiliriz ve bu  _Interface C1_'de gördüğümüz alt ağ maskesidir.
<br>
<br>
Cevaplar aşağıdaki koşullara uyduğu sürece herhangi bir adres olabilir:

- Ağ adresi (ilk 30 bit) _Client D_ ve _Client C_ için aynı olmalıdır.
- Host bitlerinin ikiside 1 ya da ikiside 0 olamaz.
- _Client D_ ve _Client C_ aynı IP adreslerine sahip olamaz.

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Level 3</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level3_paint.png?raw=true" alt="level3">
  <br>
  <br>

Bu egezersiz **switch** kullanımını dahil etmektedir(_Switch S_ b örnekte switch'i temsil eder). Switch aynı ağdaki birden fazla hostu birbirine bağlar.
<br>
<br>

**1.** _Client A_, _Client B_, ve _Client C_ hostlarının hepsi aynı ağdadır. Bu yüzden hepsinin alt ağ maskesi aynı olmalıdır. _Client C_ zaten _255.255.255.128_ maskesine sahiptir, _Interface B1_ ve for _Interface A1_ içinde alt ağ maskesi _255.255.255.128_ olacaktır (ya da _/25_).
<br>
<br>
T_Interface B1_ ve _Interface C1_ hostlarının IP adresleri _Client A_ gibi alt ağ maskesinin aralığında olmalıdır.

  <center>

```
104.198.241.0 - 104.198.241.128
```

  </center>
Tabii ki broadcast ve ağ adresi hariç.
  <div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Level 4</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level4_paint.png?raw=true" alt="level4">
  <br>
  <br>

Bu egzersizde **router** kulanımınıda öğrenecegiz. Router, birden fazla ağı birbirine bağlamak için kullanılır ve bunu birden fazla arayüz ile gerçekleştirir.(_Interface R1_, _Interface R2_,  _Interface R3_).
<br>
<br>

**1.** _Interface B1_, _Interface A1_, ve _Interface R1_ arayüzlerinde halihazırda sabitlenmiş bir alt ağ maskesi olmadığı için kendi alt ağ maskemizi seçebiliriz. **/24** ideal bir alt ağ maskesidir çünkü, hesaplamalar için ikili forma gerek kalmaz ve 4. byte'ın hepsini host adresi için bırakır.<br>
<br>
_Interface B1_ ve _Interface R1_, _Interface A1_ ile aynı ağ adresine sahip olmalıdır. _/24_, alt ağ maskesi ile mümkün olan adres aralığı:

  <center>

```
85.17.5.0 - 85.17.5.255
```

  </center>
  Broadcast adresi ve ağ adresi hariç.
  <br>
  <br>

Router'ımızın _Interface R2_ ve _Interface R3_, arayüzleriyle o taraflar ile bir bağlantı kurmaya çalışmadığımız için ilgilenmediğimizi dikkate alın.

  <div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Level 5</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level5_paint.png?raw=true" alt="level5">
  <br>
  <br>

Bu egzersizde **routes** konusuna giriş yapıyoruz. Bir rota/route'un iki alanı vardır, ilki gönderilecek paketlerin hedefi/**destination** , ikincisi ise gönderilecek paketlerin ikinci durağı/**next hop**.
<br>


 **Destination** _default_ olunca  _0.0.0.0/0_'a eşittir ve bu durumda paketleri ayrım yapmaksızın karşılaştığı ilk ağ adresine gönderecektir. Destination adresi olan _122.3.5.3/24_ IP adresi, paketi _122.3.5.0_ adresine gönderecektir.

  <br>
  
   Sıradaki durak/**next hop** sıradaki router'ın adresidir.
  <br>
  <br>

**1.** _Client A_ paketlerini gönderebileceği sadece 1 route'a sahip. Bu noktada destination değerini özelleştirmeye gerek yok. Destination değeri _default_ olarak kalabilir.
<br>
<br>
Bir sonraki durak/next hop, paketlerin yolundaki bir sonraki yönlendiricinin arayüzünün IP adresi olmalıdır. Sonraki arayüz, _54.117.30.126_ IP adresine sahip _Arayüz R1_'dir. Bir sonraki arayüzün, gönderenin kendi arayüzü olduğundan, _Arabirim A1_ olmadığını unutmayın.

  <div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Level 6</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level6_paint.png?raw=true" alt="level6">
  <br>
  <br>

Bu egzersizde **internet** konusuna giriş yapıyoruz. İnternet, router gibi davranmaktadır. Bir arayüz internete direkt ya da dolaylı olarak bağlıysa aşağıdaki IP adresi aralıklarını kullanamaz:

```
192.168.0.0 - 192.168.255.255 (65,536 IP addresses)
172.16.0.0 - 172.31.255.255   (1,048,576 IP addresses)
10.0.0.0 - 10.255.255.255     (16,777,216 IP addresses)
```

**1.**  İnternetin **next hop**'u halihazırda ayarlanmış ve _Interface R2_'nin IP adresi ile uyuşuyor. Burada sadece internetin destination değeri ile ilgileneceğiz.
<br>
<br>
İnternet paketlerini _Client A_'ya göndermeli. O zaman, internetin destination değerindeki IP adresi _Client A_'nın ağ adresi ile uyuşmalıdır. _Client A_'nın ağ adresini bulalım:
<br>
_Client A_'nın alt ağ maskesi _255.255.255.128_, yani _/25_.Bu demek oluyor ki IP adresinin 25 bit'i ağ adresidir.O zaman ilk 3 byte'ın ağ adresine dahil olduğunu biliriz:

  <center>

```
40.178.145.?
```

  </center>

Sadece 25. bitin 1 mi 0 mı olduğunu bulmamız gerekiyor.
<br>
227 sayısını ikili forma çevirirsek `11100011` karşılığını alır. bu bize 25. bitin 1 olduğunu gösterir. Bu bize sadece 25.bitten sonrasını host olarak değiştirebileceğimiz gösterir ve 25. bitin 1 olmasının karşılığı ise 128'dir.
<br>
<br>
Sonuç olarak ağ adresi:

  <center>

```
40.178.145.128
```

  </center>

_40.178.145.129 - 40.178.145.254_ aralığı ise host adresinindir.
<br>
<br>
Böylelikle **40.178.145.128** adresini internetin destination değerine yazabiliriz. Devamına yazılan **/25** ise alt ağ maskesini tanımlamaktadır.
<br>
<br>
 _40.178.145.227/25_ hedefinin destination adresi _40.178.145.128/25_'dir, alt ağ maskesinin _/25_ olması kalan tüm bitlerin 0 olmasını sağlar.

  <div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Level 7</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level7_paint.png?raw=true" alt="level7">
  <br>
  <br>

Bu egzersiz **overlaps** içeriğine giriş yapmamızı sağlar. Bir ağın IP adresleri aralığı, ayrı bir ağın IP adresleri aralığıyla örtüşmemelidir. Ağlar yönlendiricilerle ayrılır.
<br>
<br>

**1.** 3 adet ayrılmış ağımız vardır:
<br>

1. _Client A_ ve _Router R1_ arası.
2. _Router R1_ ve _Router R2_ arası.
3. _Router R2_ ve _Client C_ arası.

_Interface A1_ için, _Interface R11_'in IP'si zaten girilmiş olduğundan IP adresimizi serbestçe seçemiyoruz. Ayrıca _/24_ maskesini verirsek, IP adres aralığı zaten girilmiş olan _Interface R12_ aralığıyla örtüşecektir. Her ikisi de _93.198.14.0 - 93.198.14.255_ aralığında olacaktır.
<br>
<br>

3 ayrı ağ için adreslere ihtiyacımız olduğundan, adresin son baytlarını 4 veya daha fazla adres aralığına bölmek uygundur. Bunu _/26_ veya daha yüksek bir maske kullanarak yapıyoruz. Örneğin _/28_ maskesi bize 16 aralık verecektir ve bunlardan aşağıdaki 3'ü kullanacağız:
```
93.198.14.1 - 93.198.14.14    (Client A to Router R1)
93.198.14.65 - 93.198.14.78   (Router R1 to Router R2)
93.198.14.241 - 93.198.14.254 (Router R2 to Client C)
```

Mümkün olan ağ maskelerini hesaplamak için:
<br>
https://www.calculator.net/ip-subnet-calculator.html?cclass=any&csubnet=28&cip=93.198.14.2&ctype=ipv4&printit=0&x=97&y=13

  <div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Level 8</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level8_paint.png?raw=true" alt="level8">
  <br>
  <br>

**1.****1.** _Client C_ ve _Client D_ ana bilgisayarları internete paket gönderecek, ardından internet, paketleri ilk göndericiye geri göndererek yanıt verecektir. Bu paketleri göndermek için internet, paketleri `49.175.13.0 - 49.175.13.63` aralığındaki ağlara göndermek için _49.175.13.0/26_ hedefini kullanır.
<br>
<br>
Tüm alıcı ağlar birbiriyle örtüşmeden bu aralıkta olmalıdır.
<br>
<br>

**2.** _Interface R23_ and _Interface R22_ arayüzlerinde hedef adresinden _/26_ aralığını uygun şekilde 4 ayrı aralığa böl k için. _255.255.255.240_ maskesini kullanırız (ya da _/28_). Üst üste gelmemesi gereken aşağıdaki 3 ağa sahip olduğumuz için 4'ün ayrılması gereklidir:
<br>

1. _Router R1_  -> _Router R2_.
2. _Router R2_  -> _Client C_.
3. _Router R2_  -> _Client D_.

Bu ağların her birine daha sonra _/28_ maskesiyle aşağıdaki IP aralıklarından biri atanabilir:

```
49.175.13.0 - 49.175.13.15
49.175.13.16 - 49.175.13.31
49.175.13.32 - 49.175.13.47
49.175.13.48 - 49.175.13.63
```

Ağ adresinin (ilk) ve yayın adresinin (sonuncu) her aralıktan hariç tutulması gerektiğini unutmayın.
<br>
<br>

**3.** İnternet için destination ve next hop zaten girilmiştir. Yalnızca _Interface R21_ üzerindeki IP olan _Router R2_ için bir sonraki hop'a girmemiz gerekiyor.

<div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Level 9</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level9_paint.png?raw=true" alt="level9">
  <br>
  <br>

İnternet başlangıçta paketlerini belirli bir ağa göndermediğinden bu seviye oldukça basittir. Bu nedenle ayrı ağların ortak bir adres aralığını paylaşmasına gerek yoktur. Seviye tamamlanana kadar seviyedeki 6 hedefi tek tek takip etmenizi öneririm.
<br>
<br>
Ayrılmış özel IP aralıklarındaki ağ adreslerini kullanmamayı unutmayın.
<br>
<br>

**1.** **Hedef 3**, _meson_'u _internet_'e bağlamamız gerektiğini belirtir. Daha sonra _internet_'in _meson_'a yanıt vermesi gerekecek, bu nedenle _internet'in_ hedefine _meson'un_ ağ adresini giriyoruz.
<br>
<br>
**Hedef 6**, _cation_'ı _internet_'e bağlamamız gerektiğini belirtiyor, bu nedenle _cation'ın_ ağ adresini _internet'in_ hedefine giriyoruz.
<br>
<br>
_İnternet_'in 3. hedefi ve _Router R1'in_ hedefi için boş bir alanın olması normaldir. Yönlendirme tablolarının tüm alanlarının doldurulması gerekmez.

  <div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Level 10</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level10_paint.png?raw=true" alt="level10">
  <br>
  <br>

Bu levelde 4 adet ayrı ağımız bulunmaktadır.
<br>

1. _Router R1_ -> _Switch S1_
2. _Router R1_ -> _Router R2_
3. _Router R2_ -> _Client H4_
4. _Router R2_ -> _Client H3_
   <br>

**1.** İnternet, paketlerini tüm hostlara gönderebilmelidir, dolayısıyla hedefi, tüm hostların ağ aralığını kapsamalıdır.
<br>
<br>

_Arayüz R11_ ve _Arayüz R13_ zaten girilmiş bir IP adresine sahip. Bu IP adresi yalnızca son baytında farklılık gösterir. _Interface R11_ son bayt için **1** içerir ve _Interface R13_ son bayt için **254** içerir. Bu geniş IP adres aralığını kapsamak amacıyla, _internetin_ hedefi için **/24** maskesini alıyoruz. Bu hedef "70.101.30.0 - 70.101.30.255" aralığını kapsayacaktır.

  <br>
  <br>

**2.** IP adreslerini seçerken 2 şeyden emin olmalıyız:
<br>

1. IP adresi _internet_ hedefi kapsamındadır.
2. Çeşitli ağların IP adresi aralığı çakışmıyor.
    <br>

Zaten girilen IP adresleri (gri renkte) ile çeşitli ağların kapsadığı aralıkları inceleyelim:
<br>

1. _Router R1_ - _Switch S1_ - **70.101.30.0 - 70.101.30.127** aralığını kapsar (maske /25).
2. _Router R2_ - _Client H4_ - **70.101.30.128 - 70.101.30.191** aralığını kapsar (maske /26).
3. _Router R1_ ila _Router R2_ - **70.101.30.252 - 70.101.30.255** aralığını kapsar (maske /30).
4. _Router R2_'den _Client H3_'e - ??? (maske ???).

"Router R2'den Client H3'e" ağı için kalan tek IP adresleri **70.101.30.192 - 70.101.30.251**'dir. _Interface R22_ ve _Interface R31_'e koymak için bu aralıktan 2 IP adresi almamıza izin verecek herhangi bir maskeyi seçebiliriz.

  <div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

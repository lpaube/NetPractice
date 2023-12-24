> **Want to see 42 Quebec in 3D?**  
> **:arrow_right: https://mini42qc.vercel.app/ :arrow_left:**

# NetPractice Rehberi

![netpractice logo](img/NetPractice.png)

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
104.198.241.127 | Ağdaki tüm cihazlara iletim yapılabilmesi için kullanılan broadcast adresi için özeö olarak ayrılmıştır.
```

Böylelikle, gerçek IP adresi aralığımız `104.198.241.1 - 104.198.241.126` haline gelir, [IP calculator](https://www.calculator.net/ip-subnet-calculator.html) ile birlikte kolayca bu hesaplamalara ulaşabilirsiniz.
</br>
</br>

#### CIDR Notation (/24)

Maskeleme aynı zamanda Classless Inter-Domain Routing (CIDR) ile de gösterilebilir. Bu form "/" ile başlar ve sonrasında ağ adresi olarak tanımlanan bitlerin sayısıyla devam eder ve bu şekilde kullanılır.

Şöyle ki, `255.255.255.128` maskesinin, CIDR Notatıon karşılığı `/25`tir, yani bu 32 bitten 25 tanesinin ağ adresini tanımladığını söyler.

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

**1.** Client _A_ ve Client _B_ aynı ağda oldukları için, IP adresleri subnet maskesi ile birlikte aynı ağır temsil etmelidir.
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

This level introduces the **internet**. The internet behaves like a router. However, if an interface is connected directly or indirectly to the internet, it **cannot** have an IP address in the following reserved private IP ranges:

```
192.168.0.0 - 192.168.255.255 (65,536 IP addresses)
172.16.0.0 - 172.31.255.255   (1,048,576 IP addresses)
10.0.0.0 - 10.255.255.255     (16,777,216 IP addresses)
```

**1.** The **next hop** of the internet is already entered, and matches the IP address of the _Interface R2_. Therefore we only need to bother with the destination of the internet.
<br>
<br>
The internet must send its packets to _Client A_. To do so, the internet's destination must match the network address of _Client A_. Let's find the network address of _Client A_:
<br>
_Client A_'s mask is _255.255.255.128_, which is equivalent to _/25_. This means that the first 25 bits of its IP address are its network address. We know then that the first 3 bytes (24 bits) of its IP address make part of its network address:

  <center>

```
40.178.145.?
```

  </center>

We now only need to find out if the 25th bit is a 1 or a 0.
<br>
If we convert the number 227 to binary, we get `11100011`. The first digit, which corresponds to the 25th bit, is a 1. Since only the 25th bit is part of the network address and not the remaining 7 bits, we get `10000000` for the last byte of the network address, which is 128 in decimal.
<br>
<br>
The full network address is:

  <center>

```
40.178.145.128
```

  </center>

With a range of _40.178.145.129 - 40.178.145.254_ for its host addresses.
<br>
<br>
We can now put this address of **40.178.145.128** in the Internet destination. The **/25** following the destination address represents the mask applied to its address.
<br>
<br>
A destination of _40.178.145.227/25_ is equivalent to the destination address _40.178.145.128/25_, since the mask of _/25_ will turn all the bits after the 25th to 0 to get the destination's network address.

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

This level introduces the concept of **overlaps**. The range of IP addresses of a network must not overlap the range of IP addresses of a separate network. Networks are separated by routers.
<br>
<br>

**1.** We have 3 separate networks:
<br>

1. Between _Client A_ and _Router R1_.
2. Between _Router R1_ and _Router R2_.
3. Between _Router R2_ and _Client C_.

For _Interface A1_, we cannot choose our IP address freely since the IP of _Interface R11_ is already entered. Also, if we give it a mask of _/24_, the IP address range will overlap with the range of _Interface R12_, which is already entered. They would both be in the range of _93.198.14.0 - 93.198.14.255_.
<br>
<br>

Since we need addresses for 3 separate networks, it is convenient to split the last bytes of the address into 4 or more address ranges. We do this by using a mask of _/26_ or higher. The mask of _/28_ for example will give us 16 ranges, from which we use the following 3:

```
93.198.14.1 - 93.198.14.14    (Client A to Router R1)
93.198.14.65 - 93.198.14.78   (Router R1 to Router R2)
93.198.14.241 - 93.198.14.254 (Router R2 to Client C)
```

To calculate the possible ranges of a mask:
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

**1.** The hosts _Client C_ and _Client D_ will send packets to the internet, then the internet will respond by sending packets all the way back to the initial sender. To send these packets, the internet uses the destination _49.175.13.0/26_ to send the packets to the networks in the range of `49.175.13.0 - 49.175.13.63`.
<br>
<br>
All the receiving networks must be in this range, without overlapping each other.
<br>
<br>

**2.** On _Interface R23_ and _Interface R22_ we use the mask _255.255.255.240_ (or _/28_), to conveniently split the range of _/26_ from the destination address, into 4 separate ranges. This separation of 4 is necessary since we have the following 3 networks that must not overlap:
<br>

1. _Router R1_ to _Router R2_.
2. _Router R2_ to _Client C_.
3. _Router R2_ to _Client D_.

Each of these networks can then be attributed one of the following IP ranges with a mask of _/28_:

```
49.175.13.0 - 49.175.13.15
49.175.13.16 - 49.175.13.31
49.175.13.32 - 49.175.13.47
49.175.13.48 - 49.175.13.63
```

Note that the network address (first) and the broadcast address (last) must be excluded from each range.
<br>
<br>

**3.** The destination and next hop for the internet are already entered. We only need to enter the next hop for the _Router R2_, which is the IP on the _Interface R21_.

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

This level is quite straightforward since the internet does not initially send its packets to a specific network. Therefore, the separate networks do not need to share a common address range. I would suggest simply following the 6 goals of the level one by one until the level is completed.
<br>
<br>
Remember not to use the network addresses from the reserved private IP ranges.
<br>
<br>

**1.** **Goal 3** states that we must connect _meson_ with the _internet_. The _internet_ will then have to respond to _meson_, so we enter _meson's_ network address in the _internet's_ destination.
<br>
<br>
**Goal 6** states that we must connect _cation_ with the _internet_, so we enter _cation's_ network address in the _internet's_ destination.
<br>
<br>
It is normal to have an empty field for the 3rd destination of the _internet_, and in _Router R1's_ destination. Not all fields of the routing tables need to be filled.

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

At this level, there are 4 different networks:
<br>

1. _Router R1_ to _Switch S1_
2. _Router R1_ to _Router R2_
3. _Router R2_ to _Client H4_
4. _Router R2_ to _Client H3_
   <br>

**1.** The internet must be able to send its packets to all the hosts, so its destination must cover the range of networks of all the hosts.
<br>
<br>

_Interface R11_ and _Interface R13_ already have an IP address entered. This IP address only differs in its last byte. _Interface R11_ has for last byte **1**, and _Interface R13_ has for last byte **254**. To cover this wide range to IP addresses, we take a mask of **/24** for the _internet's_ destination. This destination will cover a range of `70.101.30.0 - 70.101.30.255`.

  <br>
  <br>

**2.** When choosing the IP addresses, we must make sure of 2 things:
<br>

1. The IP address is covered by the _internet_ destination.
2. The IP address range of the various networks does not overlap.
   <br>

With the IP addresses already entered (greyed out), let's examine the ranges covered by the various networks:
<br>

1. _Router R1_ to _Switch S1_ - Covers the range **70.101.30.0 - 70.101.30.127** (mask /25).
2. _Router R2_ to _Client H4_ - Covers the range **70.101.30.128 - 70.101.30.191** (mask /26).
3. _Router R1_ to _Router R2_ - Covers the range **70.101.30.252 - 70.101.30.255** (mask /30).
4. _Router R2_ to _Client H3_ - ??? (mask ???).

The only IP addresses left for the network "Router R2 to Client H3" are **70.101.30.192 - 70.101.30.251**. We can pick any mask that will let us take 2 IP addresses from that range to put in _Interface R22_ and _Interface R31_.

  <div align="right">
  <b><a href="#top">↥ back to top</a></b>
</div>
</br>

</details>

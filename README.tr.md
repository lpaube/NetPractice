> **42 Quebec'i 3D olarak görmek ister misiniz?**  
> **:arrow_right: https://mini42qc.vercel.app/ :arrow_left:**

# NetPractice Kılavuzu

![netpractice logo](img/NetPractice.png)

<div id="top"></div>

## Diğer Diller

[Korean](README.ko.md)
<br>
[French](README.fr.md)
<br>
[English](README.md)

## İçindekiler

- [Önemli Kavramlar](#önemli-kavramlar)
  - [TCP](#tcp-i̇letim-katmanı)
  - [IP adresi](#ip-adresi-ağ-katmanı)
  - [Alt Ağ Maskesi](#alt-ağ-maskesi)
  - [Anahtar](#anahtar)
  - [Yönlendirici](#yönlendirici)
- [Bölümler](#bölümler)

---

## Önemli Kavramlar

### TCP: İletim Katmanı

</br>
<p align="center">
  <img src="./img/tcp-ip-stack.png" height=300 width=200 alt="mask">
</p>
</br>

TCP, **İletim Kontrol Protokolü** anlamına gelir. Uygulama programlarının ve cihazların ağ üzerinden mesaj alışverişi yapmasını sağlayan bir iletişim standardıdır. İnternet üzerinden paket göndermek için kullanılır.

TCP, bir ağ üzerinden iletilen verilerin bütünlüğünü garanti eder. Verileri iletmeden önce TCP, kaynak ile hedef arasında iletişim başlayana kadar aktif kalan bir bağlantı kurar. Daha sonra büyük miktarda veriyi daha küçük paketlere bölerek herhangi bir veri kaybı olmadan uçtan uca teslimatı sağlar.

<div align="right">
  <b><a href="#top">↥ Başa dön</a></b>
</div>
</br>

---

### IP Adresi: Ağ Katmanı

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/ip1.png?raw=true" height=250 alt="mask"></kbd>
</p>
</br>

IP, iletim kontrol protokolünü de içeren bir internet protokol paketinin parçasıdır. Bu ikisi birlikte TCP/IP olarak bilinir. İnternet protokol paketi, ağlar üzerinden verinin paketlenmesi, adreslenmesi, iletilmesi, yönlendirilmesi ve alınmasına ilişkin kuralları yönetir.

IP adresleme, ağdaki cihazlara adres atamanın mantıksal bir yoludur. İnternete bağlanan her cihazın benzersiz bir IP adresi olması gerekir.

Bir IP adresinin iki bölümü vardır; bir kısım bilgisayar veya başka bir cihaz gibi ana bilgisayarı tanımlarken, diğer kısım ait olduğu ağı tanımlar. TCP/IP bunları ayırmak için bir [alt ağ maskesi](#alt-ağ-maskesi) kullanır.
</br>
</br>

#### IPv4 vs. IPv6

IP adreslerinin 2 sürümü vardır: IPv4 ve IPv6:
<br>

<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/ip_version.png?raw=true" height=100 alt="ip_versions"></kbd>
</p>
<br>

İnternet Protokolü sürüm 4 (IPv4), IP adresini 32 bitlik bir sayı olarak tanımlar. Ancak İnternet'in büyümesi ve mevcut IPv4 adreslerinin tükenmesi nedeniyle, IP adresi için 128 bit kullanan yeni bir IP sürümü (IPv6) 1998'de standartlaştırıldı. Ancak NetPractice'te yalnızca IPv4 adresleri kullanılıyor.
</br>
</br>

#### Genel Adresler vs. Özel Adresler

Genel IP adresi, doğrudan internet üzerinden erişilebilen ve internet servis sağlayıcınız (ISS) tarafından ağ yönlendiricinize atanan bir IP adresidir. Genel (veya harici) bir IP adresi, ağınızın içinden ve ağınızın dışından internete bağlanmanıza yardımcı olur.

Özel IP adresi, ağ yönlendiricinizin cihazınıza atadığı bir adrestir. Aynı ağdaki her cihaza benzersiz bir özel IP adresi (bazen özel ağ adresi olarak da adlandırılır) atanır; bu, aynı dahili ağdaki cihazların birbirleriyle nasıl konuştuğudur.

Bir ağ internete bağlandığında, ayrılmış özel IP adreslerinden bir IP adresini kullanamaz. Aşağıdaki aralıklar özel IP adresleri için ayrılmıştır:

```
192.168.0.0 – 192.168.255.255 (65,536 IP adres)
172.16.0.0 – 172.31.255.255   (1,048,576 IP adres)
10.0.0.0 – 10.255.255.255     (16,777,216 IP adres)
```

<div align="right">
  <b><a href="#top">↥ Başa dön</a></b>
</div>
</br>

---

### Alt Ağ Maskesi

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/mask1.png?raw=true" height=250 alt="mask"></kbd>
</p>
</br>

Alt ağ maskesi, IP adresindeki bir ağ adresi ile ana bilgisayar adresini birbirinden ayırmak için kullanılan 32 bitlik (4 bayt) bir adrestir. Bir ağda veya alt ağda kullanılabilecek IP adresi aralığını tanımlar.
</br>
</br>

#### Ağ adresini bulma

Yukarıdaki _Arayüz A1_ aşağıdaki özelliklere sahiptir:

```
IP address | 104.198.241.125
Mask       | 255.255.255.128
```

IP adresinin hangi bölümünün ağ adresi olduğunu belirlemek için IP adresine maske uygulamamız gerekir. Önce maskeyi ikili forma dönüştürelim:

```
Mask | 11111111.11111111.11111111.10000000
```

Maskenin 1 olan bitleri ağ adresini temsil ederken, maskenin 0 olan geri kalan bitleri ana bilgisayar adresini temsil eder. Şimdi IP adresini ikili forma dönüştürelim:

```
IP address | 01101000.11000110.11110001.01111101
Mask       | 11111111.11111111.11111111.10000000
```

Artık IP'nin ağ adresini bulmak için maskeyi [bitwise AND](https://en.wikipedia.org/wiki/Bitwise_operation#AND) aracılığıyla IP adresine uygulayabiliriz:

```
Network address | 01101000.11000110.11110001.00000000
```

Bu, `104.198.241.0` ağ adresine karşılık gelir.
</br>
</br>

#### Kullanılabilir IP adresi aralığını bulma

Ağımızda hangi ana bilgisayar adreslerini kullanabileceğimizi belirlemek için IP adresimizin ana bilgisayar adresine ayrılmış bitlerini kullanmamız gerekir. Önceki IP adresimizi ve maskemizi kullanalım:

```
IP address | 01101000.11000110.11110001.01111101
Mask       | 11111111.11111111.11111111.10000000
```

Ana bilgisayar adreslerimizin olası aralığı, maskenin tümü 0 olan son 7 biti aracılığıyla ifade edilir. Bu nedenle, ana bilgisayar adreslerinin aralığı şöyledir:

```
BINARY  | 0000000 - 1111111
DECIMAL | 0 - 127
```

Ağımız için olası IP adresleri aralığını elde etmek için, ana bilgisayar adresleri aralığını ağ adresine ekliyoruz. Olası IP adresi aralığımız `104.198.241.0 - 104.198.241.127` olur.

<ins>ANCAK</ins>, aralığın uçları (başı ve sonu) belirli kullanımlar için ayrılmıştır bu yüzden bir arayüze verilemez:

```
104.198.241.0   | Ağ adresini temsil etmek için ayrılmıştır.
104.198.241.127 | Yayın adresi (Broadcast) olarak ayrılmıştır; Bir ağın tüm ana bilgisayarlarına paket göndermek için kullanılır.
```

Bu nedenle, gerçek IP aralığımız `104.198.241.1 - 104.198.241.126` olur ve bu, bir [IP hesaplayıcı](https://www.calculator.net/ip-subnet-calculator.html) kullanılarak bulunabilir.
</br>
</br>

#### CIDR Notasyonu (/24)

Maske aynı zamanda Sınıfsız Etki Alanları Arası Yönlendirme (CIDR) ile de temsil edilebilir. Bu form, maskeyi eğik çizgi `/` ve ardından ağ adresi olarak görev yapan bit sayısını temsil eder.

Bu nedenle, yukarıdaki `255.255.255.128` örneğindeki maske, CIDR gösterimini kullanan `/25` maskesine eşdeğerdir, çünkü 32 bitin 25 biti ağ adresini temsil eder.

<div align="right">
  <b><a href="#top">↥ Başa dön</a></b>
</div>
</br>

---

### Anahtar

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/switch1.png?raw=true" height=150 alt="switch"></kbd>
</p>
</br>

Bir anahtar birden fazla cihazı tek bir ağda birbirine bağlar. Yönlendiriciden farklı olarak anahtarın herhangi bir arabirimi yoktur, çünkü paketleri yalnızca yerel ağına dağıtır ve kendi dışındaki bir ağla doğrudan konuşamaz.

<div align="right">
  <b><a href="#top">↥ Başa dön</a></b>
</div>
</br>

---

### Yönlendirici

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/route1.png?raw=true" height=200 alt="router"></kbd>
</p>
</br>

Anahtarın birden fazla cihazı tek bir ağa bağlaması gibi, yönlendirici de birden fazla ağı birbirine bağlar. Yönlendiricinin bağlandığı her ağ için bir arayüzü vardır.

Yönlendirici farklı ağları ayırdığından, arayüzlerinden birindeki olası IP adreslerinin aralığı diğer arayüzlerin aralığıyla çakışmamalıdır. IP adresi aralığındaki bir çakışma, arayüzlerin aynı ağ üzerinde olduğu anlamına gelir.
</br>
</br>

#### Yönlendirme Tablosu

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/routing_table1.png?raw=true" height=150 alt="routing_table"></kbd>
</p>
</br>

Yönlendirme tablosu, bir yönlendiricide veya ağ ana bilgisayarında saklanan ve belirli ağ hedeflerine giden yolları listeleyen bir veri tablosudur. NetPractice'te yönlendirme tablosu 2 öğeden oluşur:

- **Varış noktası**: Hedef, paketlerin son hedefinin bir ana bilgisayar olduğu bir ağ adresini belirtir. `default` veya `0.0.0.0/0` rotası, bir IP hedef adresi için başka bir rota bulunmadığında etkili olan rotadır. Varsayılan rota, paketleri belirli bir hedef vermeden yollarına göndermek için sonraki atlama adresini kullanacaktır. Varsayılan rota herhangi bir ağla eşleşecektir.

- **Sonraki atlama noktası**: Bir sonraki atlama noktası, bir paketin geçebileceği bir sonraki en yakın yönlendiriciyi ifade eder. Paketin yolundaki bir sonraki yönlendiricinin IP adresidir. Her bir yönlendirici, yönlendirme tablosunu bir sonraki atlama adresiyle korur.

<div align="right">
  <b><a href="#top">↥ Başa dön</a></b>
</div>
</br>

## Bölümler

<details>
  <summary>Bölüm 1</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level1_paint.png?raw=true" alt="level1">  
  <br>
  <br>

**1.** _Client A_ ve _Client B_ aynı ağda olduğundan, IP adreslerinin alt ağ maskesine uygun olarak aynı ağı temsil etmesi gerekir.
<br>
Alt ağ maskesi _255.255.255.0_'dır; bu, IP adresinin ilk 3 baytının ağı, 4. baytının da ana bilgisayarı temsil ettiği anlamına gelir. Aynı ağda olduğumuz için sadece host değişebilir.
<br>
Çözüm, aşağıdaki 3'ü hariç **104.96.23.0 - 104.96.23.255** aralığındaki herhangi bir şey olacaktır:

- **104.96.23.0:** Ana bilgisayar aralığındaki ilk sayı (bu durumda 0) ağı temsil eder ve bir ana bilgisayar tarafından kullanılamaz.
- **104.96.23.255:** Ana bilgisayar aralığındaki son sayı (bu durumda 255) yayın adresini temsil eder.
- **104.96.23.12:** Bu adres zaten _Client B_ ana bilgisayarı tarafından kullanılıyor.

**2.** _1._ ile aynı mantık, ancak bu durumda alt ağ maskesi _255.255.0.0_'dır. IP adresinin ilk 2 baytı ağı temsil edecektir; ve son 2 bayt, ana bilgisayar adresi.
<br>
Çözüm, **211.191.0.0 - 211.191.255.255** aralığındaki herhangi bir şey olacaktır; ancak aşağıdakiler hariç:

- **211.191.0.0:** Ağ adresini temsil eder.
- **211.191.255.255:** Yayın adresini temsil eder.
- **211.191.89.75:** Zaten _Client C_ ana bilgisayarı tarafından alınmış.

<div align="right">
  <b><a href="#top">↥ Başa dön</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Bölüm 2</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level2_paint.png?raw=true" alt="level2">
  <br>
  <br>

**1.** _Client B_, _Client A_ ile aynı özel ağda olduğundan, tam olarak aynı alt ağ maskesine sahip olmaları gerekir.
<br>
Çözüm yalnızca **255.255.255.224** olabilir.

**2.** _255.255.255.224_ alt ağ maskesini anlamak için, buna _Client B_'nin _192.168.20.222_ IP'siyle birlikte ikili biçimde bakalım:

<center>

```
MASK: 11111111.11111111.11111111.11100000
IP:   11000000.10101000.00010100.11011101
```

</center>
Gördüğümüz gibi ilk 27 bit IP adresini temsil ederken, yalnızca son 5 bit ana bilgisayar adresini temsil ediyor.
<br>
Ağı temsil eden bu 27 bitin tamamının, aynı ağdaki ana bilgisayarların IP adreslerinde aynı kalması gerekir. Cevabı almak için yalnızca son 5 biti değiştirebiliriz.
<br>
<br>
Cevap şu aralıktadır:

```
İKİLİK (BIN):  11000000.10101000.00010100.11000000 - 11000000.10101000.00010100.11011111
or
ONDALIK (DEC):  192.168.20.192 - 192.168.20.223
```

Bunlar hariç:
<br>

- **11000000.10101000.00010100.11000000:** Ağ adresini temsil eder (son 5 bitteki tüm 0'lara dikkat edin).
- **11000000.10101000.00010100.11011111:** Yayın adresini temsil eder (son 5 bitteki 1'in tümüne dikkat edin).
- **11000000.10101000.00010100.11011110:** _Client B_ bu adrese zaten sahip.

**3.** Burada _Interface D1_'deki alt ağ maskesi için eğik çizgi "/" gösterimini tanıttık. _/30_ alt ağ maskesi, IP adresinin ilk 30 bitinin ağ adresini, geri kalan 2 bitinin ise ana bilgisayar adresini temsil ettiği anlamına gelir:

<center>

```
Alt Ağ Maskesi (Mask) /30: 11111111.11111111.11111111.11111100
```

</center>

Bu ikili sayının _255.255.255.252_ ondalık sayıya karşılık geldiğini görebiliriz, dolayısıyla _Interface C1_'de bulunan maskeyle aynıdır.
<br>
<br>
Cevaplar, aşağıdaki şartları karşıladıkları sürece herhangi bir adres olabilir:

- Ağ adresi (ilk 30 bit) _Client D_ ve _Client C_ için aynı olmalıdır.
- Ana bilgisayar bitlerinin (son 2 bit) tamamı 1 veya tamamı 0 olamaz.
- _Client D_ ve _Client C_ aynı IP adreslerine sahip değil.

<div align="right">
  <b><a href="#top">↥ Başa dön</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Bölüm 3</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level3_paint.png?raw=true" alt="level3">
  <br>
  <br>

Bu alıştırmada **anahtarın** (bu örnekte _Switch S_) kullanımı anlatılmaktadır. Anahtar, aynı ağdaki birden fazla ana bilgisayarı birbirine bağlar.
<br>
<br>

**1.** _Client A_, _Client B_ ve _Client C_'nin tümü aynı ağ üzerindedir. Bu nedenle hepsinin aynı alt ağ maskesine sahip olması gerekir. _Client C_ zaten _255.255.255.128_ maskesine sahip olduğundan, _Interface B1_ ve _Interface A1_ için maske de _255.255.255.128_ olacaktır (veya eğik çizgi gösteriminde: _/25_).
<br>
<br>
_Interface B1_ ve _Interface C1_'in IP adresi, _Client A_'nın IP'si ile aynı ağ aralığında olmalıdır. Bu aralık:

  <center>

```
104.198.241.0 - 104.198.241.128
```

  </center>
  Elbette ağ adresi ve yayın adresi hariç.

  <div align="right">
  <b><a href="#top">↥ Başa dön</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Bölüm 4</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level4_paint.png?raw=true" alt="level4">
  <br>
  <br>

Bu alıştırmada **yönlendirici** tanıtılmaktadır. Yönlendirici birden fazla ağı birbirine bağlamak için kullanılır. Bunu birden çok arabirimin kullanımıyla yapar (bu örnekte _Interface R1_, _Interface R2_ ve _Interface R3_).
<br>
<br>

**1.** _Interface B1_, _Interface A1_ ve _Interface R1_ üzerindeki maskelerin hiçbirine girilmediğinden, kendi alt ağ maskemizi seçmekte özgürüz. **/24** maskesi idealdir çünkü bize ana bilgisayar adresi için 4. baytın tamamını bırakır ve olası ana bilgisayar adresleri aralığını bulmak için ikili hesaplamalar gerektirmez.
<br>
<br>
_Interface B1_ ve _Interface R1_'in IP adresi, _Interface A1_'nin IP adresiyle aynı ağ adresine sahip olmalıdır. _/24_ alt ağıyla olası aralık şöyledir:

  <center>

```
85.17.5.0 - 85.17.5.255
```

  </center>
  Ağ adresi ve yayın adresi hariç.
  <br>
  <br>

İletişimlerimizin hiçbirinin yönlendiricinin bu taraflarına ulaşması gerekmediğinden, _Interface R2_ ve _Interface R3_ yönlendiricileriyle etkileşimde bulunmadığımızı unutmayın.

  <div align="right">
  <b><a href="#top">↥ Başa dön</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Bölüm 5</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level5_paint.png?raw=true" alt="level5">
  <br>
  <br>

Bu seviyede **rotalar** tanıtılmaktadır. Bir rota 2 alan içerir; ilki giden paketlerin **hedefi**, ikincisi ise paketlerin **sonraki atlama noktasıdır**.
<br>

**hedef** _default_, _0.0.0.0/0_'ye eşdeğerdir; bu, paketleri ayrım gözetmeksizin karşılaştığı ilk ağ adresine gönderir. _122.3.5.3/24_ hedef adresi, paketleri _122.3.5.0_ ağına gönderecektir.

  <br>
  **Sonraki atlama noktası**, mevcut makinenin arayüzünün paketlerini göndermesi gereken bir sonraki yönlendirici (veya internet) arayüzünün IP adresidir.
  <br>
  <br>

**1.** _Client A_'nın paketlerini gönderebileceği yalnızca 1 rotası vardır. Numaralandırılmış bir hedef belirlemenin faydası yoktur. Hedef _default_, paketleri mevcut tek yola gönderecektir.
<br>
<br>
Bir sonraki atlama noktası, paketlerin yolundaki bir sonraki yönlendiricinin arayüzünün IP adresi olmalıdır. Sonraki arayüz, _54.117.30.126_ IP adresine sahip _Interface R1_'dir. Bir sonraki arayüzün, gönderenin kendi arayüzü olduğundan, _Interface A1_ olmadığını unutmayın.

  <div align="right">
  <b><a href="#top">↥ Başa dön</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Bölüm 6</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level6_paint.png?raw=true" alt="level6">
  <br>
  <br>

Bu seviye **internet**'i tanıtır. İnternet bir yönlendirici gibi davranır. Ancak, bir arayüz doğrudan veya dolaylı olarak internete bağlıysa, aşağıdaki ayrılmış özel IP aralıklarında bir IP adresine **sahip olamaz**:

```
192.168.0.0 - 192.168.255.255 (65,536 IP adres)
172.16.0.0 - 172.31.255.255   (1,048,576 IP adres)
10.0.0.0 - 10.255.255.255     (16,777,216 IP adres)
```

**1.** İnternetin **sonraki atlama noktası** zaten girilmiştir ve _Interface R2_'nin IP adresiyle eşleşir. Bu nedenle sadece internetin hedefiyle uğraşmamız gerekiyor.
<br>
<br>
İnternet, paketlerini _Client A_'a göndermelidir. Bunu yapmak için internetin hedefinin _Client A_'ın ağ adresiyle eşleşmesi gerekir. _Client A_'ın ağ adresini bulalım:
<br>
_Client A_'nın maskesi _255.255.255.128_'dir ve bu, _/25_'ye eşdeğerdir. Bu, IP adresinin ilk 25 bitinin ağ adresi olduğu anlamına gelir. O halde IP adresinin ilk 3 baytının (24 bit) ağ adresinin bir parçasını oluşturduğunu biliyoruz:

  <center>

```
40.178.145.?
```

  </center>

Şimdi sadece 25. bitin 1 mi yoksa 0 mı olduğunu bulmamız gerekiyor.
<br>
227 sayısını ikiliye çevirirsek `11100011` elde ederiz. 25. bit'e karşılık gelen ilk rakam 1'dir. Geriye kalan 7 bit değil, yalnızca 25. bit ağ adresinin bir parçası olduğundan, ağ adresinin son baytı için 128 olan `10000000` değerini alırız. ondalık olarak.
<br>
<br>
Tam ağ adresi:

  <center>

```
40.178.145.128
```

  </center>

Ana bilgisayar adresleri için _40.178.145.129 - 40.178.145.254_ aralığı.
<br>
<br>
Artık **40.178.145.128** adresini İnternet hedefine koyabiliriz. Hedef adresin ardından gelen **/25**, adrese uygulanan maskeyi temsil eder.
<br>
<br>
_40.178.145.227/25_ hedefi, _40.178.145.128/25_ hedef adresine eşdeğerdir, çünkü _/25_ maskesi, hedefin ağ adresini almak için 25'ten sonraki tüm bitleri 0'a çevirecektir.

  <div align="right">
  <b><a href="#top">↥ Başa dön</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Bölüm 7</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level7_paint.png?raw=true" alt="level7">
  <br>
  <br>

Bu bölüm **örtüşmeler** kavramını tanıtır. Bir ağın IP adresleri aralığı, ayrı bir ağın IP adresleri aralığıyla örtüşmemelidir. Ağlar yönlendiriciler sayesinde ayrılır.
<br>
<br>

**1.** 3 ayrı ağımız var:
<br>

1. _Client A_ ve _Router R1_ arasında.
2. _Router R1_ ve _Router R2_ arasında.
3. _Router R2_ ve _Client C_ arasında.

_Interface A1_ için, _Interface R11_'in IP'si zaten girilmiş olduğundan IP adresimizi serbestçe seçemiyoruz. Ayrıca _/24_ maskesini verirsek, IP adres aralığı zaten girilmiş olan _Interface R12_ aralığıyla örtüşecektir. Her ikisi de _93.198.14.0 - 93.198.14.255_ aralığında olacaktır.
<br>
<br>

3 ayrı ağ için adreslere ihtiyacımız olduğundan, adresin son baytlarını 4 veya daha fazla adres aralığına bölmek uygundur. Bunu _/26_ veya daha yüksek bir maske kullanarak yapıyoruz. Örneğin _/28_ maskesi bize 16 aralık verecektir ve bunlardan aşağıdaki 3'ü kullanacağız:

```
93.198.14.1 - 93.198.14.14    (Client A'dan Router R1'e)
93.198.14.65 - 93.198.14.78   (Router R1'den Router R2'ye)
93.198.14.241 - 93.198.14.254 (Router R2'den Client C'ye)
```

Bir maskenin olası aralıklarını hesaplamak için:
<br>
https://www.calculator.net/ip-subnet-calculator.html?cclass=any&csubnet=28&cip=93.198.14.2&ctype=ipv4&printit=0&x=97&y=13

  <div align="right">
  <b><a href="#top">↥ Başa dön</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Bölüm 8</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level8_paint.png?raw=true" alt="level8">
  <br>
  <br>

**1.** _Client C_ ve _Client D_ ana bilgisayarları internete paket gönderecek, ardından internet, paketleri ilk göndericiye geri göndererek yanıt verecektir. Bu paketleri göndermek için internet, paketleri '49.175.13.0 - 49.175.13.63' aralığındaki ağlara göndermek için _49.175.13.0/26_ hedefini kullanır.
<br>
<br>
Tüm alıcı ağlar birbiriyle örtüşmeden bu aralıkta olmalıdır.
<br>
<br>

**2.** _Interface R23_ ve _Interface R22_'de, hedef adresinden _/26_ aralığını uygun şekilde 4 ayrı aralığa bölmek için _255.255.255.240_ (veya _/28_) maskesini kullanırız. Üst üste gelmemesi gereken aşağıdaki 3 ağa sahip olduğumuz için 4'ün bu şekilde ayrılması gereklidir:
<br>

1. _Router R1_'deb _Router R2_'ye.
2. _Router R2_'den to _Client C_'ye.
3. _Router R2_'den to _Client D_'ye.

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

**3.** İnternet için hedef ve sonraki atlama noktası zaten girilmiştir. Yalnızca _Interface R21_ üzerindeki IP olan _Router R2_ için bir sonraki atlama noktasına girmemiz gerekiyor.

<div align="right">
  <b><a href="#top">↥ Başa dön</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Bölüm 9</summary>
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

**1.** **Goal 3**, _meson_'u _internet_'e bağlamamız gerektiğini belirtir. Daha sonra _internet_'in _meson_'a yanıt vermesi gerekecek, bu nedenle _internet'in_ hedefine _meson'un_ ağ adresini giriyoruz.
<br>
<br>
**Goal 6**, _cation_'ı _internet_'e bağlamamız gerektiğini belirtiyor, bu nedenle _cation'ın_ ağ adresini _internet'in_ hedefine giriyoruz.
<br>
<br>
_İnternet_'in 3. hedefi ve _Router R1'in_ hedefi için boş bir alanın olması normaldir. Yönlendirme tablolarının tüm alanlarının doldurulması gerekmez.

  <div align="right">
  <b><a href="#top">↥ Başa dön</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Bölüm 10</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level10_paint.png?raw=true" alt="level10">
  <br>
  <br>

Bu bölümde 4 farklı ağ vardır:
<br>

1. _Router R1_'den _Switch S1_'e
2. _Router R1_'den _Router R2_'ye
3. _Router R2_'den to _Client H4_'e
4. _Router R2_'den to _Client H3_'e
   <br>

**1.** İnternet, paketlerini tüm ana bilgisayarlara gönderebilmelidir, dolayısıyla hedefi, tüm ana bilgisayarların ağ aralığını kapsamalıdır.
<br>
<br>

_Interface R11_ ve _Interface R13_ zaten girilmiş bir IP adresine sahip. Bu IP adresi yalnızca son baytında farklılık gösterir. _Interface R11_ son bayt için **1** içerir ve _Interface R13_ son bayt için **254** içerir. Bu geniş IP adres aralığını kapsamak amacıyla, _internetin_ hedefi için **/24** maskesini alıyoruz. Bu hedef `70.101.30.0 - 70.101.30.255` aralığını kapsayacaktır.

  <br>
  <br>

**2.** IP adreslerini seçerken 2 şeyden emin olmalıyız:
<br>

1. IP adresi _internet_ hedefi kapsamındadır.
2. Çeşitli ağların IP adresi aralığı örtüşmüyor.
   <br>

Zaten girilen IP adresleri (gri renkte olan) ile çeşitli ağların kapsadığı aralıkları inceleyelim:
<br>

1. _Router R1_'den _Switch S1_'e - **70.101.30.0 - 70.101.30.127** aralığını kapsar (maske /25).
2. _Router R2_'den _Client H4_'e - **70.101.30.128 - 70.101.30.191** aralığını kapsar (maske /26).
3. _Router R1_'den _Router R2_'ye - **70.101.30.252 - 70.101.30.255** aralığını kapsar (maske /30).
4. _Router R2_'den _Client H3_'e - ??? (maske ???).

"Router R2'den Client H3'e" ağı için kalan tek IP adresleri **70.101.30.192 - 70.101.30.251**'dir. _Interface R22_ ve _Interface R31_'e koymak için bu aralıktan 2 IP adresi almamıza izin verecek herhangi bir maskeyi seçebiliriz.

  <div align="right">
  <b><a href="#top">↥ Başa dön</a></b>
</div>
</br>

</details>

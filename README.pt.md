# Guia do NetPractice

![logótipo netpractice](img/NetPractice.png)

<div id="top"></div>

## Outros idiomas

[Coreano](README.ko.md)
<br>
[Francês](README.fr.md)
<br>
[Espanhol](README.es.md)
<br>
[Inglês](README.md)

## Índice

- [Conceitos importantes](#conceitos-importantes)
  - [TCP](#tcp-camada-de-transporte)
  - [Endereço IP](#endereço-ip-camada-de-rede)
  - [Máscara de sub-rede](#máscara-de-sub-rede)
  - [Switch](#switch)
  - [Router](#router)
- [Níveis](#níveis)

---

## Conceitos importantes

### TCP: camada de transporte

</br>
<p align="center">
  <img src="./img/tcp-ip-stack.png" height=300 width=200 alt="mask">
</p>
</br>

TCP significa **Transmission Control Protocol** (Protocolo de Controlo de Transmissão). É um padrão de comunicações que permite a programas e dispositivos trocar mensagens através de uma rede. É usado para enviar pacotes pela Internet.

O TCP garante a integridade dos dados comunicados através de uma rede. Antes de transmitir dados, o TCP estabelece uma ligação entre uma origem e o seu destino, que se mantém ativa até a comunicação começar. Em seguida, divide grandes quantidades de dados em pacotes mais pequenos, garantindo a entrega de extremo a extremo sem perda de dados.

<div align="right">
  <b><a href="#top">↥ voltar ao topo</a></b>
</div>
</br>

---

### Endereço IP: camada de rede

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/ip1.png?raw=true" height=250 alt="mask"></kbd>
</p>
</br>

O IP faz parte de um conjunto de protocolos da Internet, que inclui também o protocolo de controlo de transmissão. Juntos, estes dois são conhecidos como TCP/IP. O conjunto de protocolos da Internet define as regras para empacotar, endereçar, transmitir, encaminhar e receber dados através de redes.

O endereçamento IP é uma forma lógica de atribuir endereços a dispositivos numa rede. Cada dispositivo ligado à Internet precisa de um endereço IP único.

Um endereço IP tem duas partes: uma identifica o host, como um computador ou outro dispositivo, e a outra identifica a rede a que pertence. O TCP/IP usa uma [máscara de sub-rede](#máscara-de-sub-rede) para as separar.
</br>
</br>

#### IPv4 vs. IPv6

Os endereços IP existem em 2 versões — IPv4 e IPv6:
<br>

<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/ip_version.png?raw=true" height=100 alt="ip_versions"></kbd>
</p>
<br>

O Internet Protocol version 4 (IPv4) define um endereço IP como um número de 32 bits. No entanto, devido ao crescimento da Internet e ao esgotamento dos endereços IPv4 disponíveis, uma nova versão do IP (IPv6), que usa 128 bits para o endereço IP, foi normalizada em 1998. No NetPractice, porém, só se usam endereços IPv4.
</br>
</br>

#### Endereço público vs. endereço privado

Um endereço IP público é um endereço IP que pode ser acedido diretamente através da Internet e que é atribuído ao router da tua rede pelo fornecedor de serviços de Internet (ISP). Um endereço IP público (ou externo) permite ligar à Internet a partir do interior da tua rede, para o exterior da tua rede.

Um endereço IP privado é um endereço que o router da tua rede atribui ao teu dispositivo. A cada dispositivo dentro da mesma rede é atribuído um endereço IP privado único (por vezes chamado endereço de rede privada) — é assim que os dispositivos na mesma rede interna comunicam entre si.

Quando uma rede está ligada à Internet, não pode usar um endereço IP dos intervalos reservados para endereços privados. Os seguintes intervalos estão reservados para endereços IP privados:

```
192.168.0.0 – 192.168.255.255 (65 536 endereços IP)
172.16.0.0 – 172.31.255.255   (1 048 576 endereços IP)
10.0.0.0 – 10.255.255.255     (16 777 216 endereços IP)
```

<div align="right">
  <b><a href="#top">↥ voltar ao topo</a></b>
</div>
</br>

---

### Máscara de sub-rede

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/mask1.png?raw=true" height=250 alt="mask"></kbd>
</p>
</br>

Uma máscara de sub-rede é um endereço de 32 bits (4 bytes) usado para distinguir, no endereço IP, o endereço de rede do endereço de host. Define o intervalo de endereços IP que podem ser usados dentro de uma rede ou de uma sub-rede.
</br>
</br>

#### Encontrar o endereço de rede

A _Interface A1_ acima tem as seguintes propriedades:

```
Endereço IP | 104.198.241.125
Máscara     | 255.255.255.128
```

Para determinar que parte do endereço IP é o endereço de rede, é preciso aplicar a máscara ao endereço IP. Primeiro, convertemos a máscara para a forma binária:

```
Máscara | 11111111.11111111.11111111.10000000
```

Os bits da máscara que são 1 representam o endereço de rede, enquanto os bits restantes, que são 0, representam o endereço de host. Agora convertemos o endereço IP para a forma binária:

```
Endereço IP | 01101000.11000110.11110001.01111101
Máscara     | 11111111.11111111.11111111.10000000
```

Podemos agora aplicar a máscara ao endereço IP através de um [AND bit a bit](https://pt.wikipedia.org/wiki/Operação_bit_a_bit#AND) para encontrar o endereço de rede do IP:

```
Endereço de rede | 01101000.11000110.11110001.00000000
```

O que corresponde ao endereço de rede `104.198.241.0`.
</br>
</br>

#### Encontrar o intervalo de endereços de host

Para determinar que endereços de host podemos usar na nossa rede, temos de usar os bits do endereço IP dedicados ao endereço de host. Usemos o endereço IP e a máscara anteriores:

```
Endereço IP | 01101000.11000110.11110001.01111101
Máscara     | 11111111.11111111.11111111.10000000
```

O intervalo possível dos endereços de host é dado pelos últimos 7 bits da máscara, que são todos 0. Portanto, o intervalo de endereços de host é:

```
BINÁRIO | 0000000 - 1111111
DECIMAL | 0 - 127
```

Para obter o intervalo de endereços IP possíveis da nossa rede, somamos o intervalo de endereços de host ao endereço de rede. O intervalo de endereços IP possíveis passa a ser `104.198.241.0 - 104.198.241.127`.

<ins>NO ENTANTO</ins>, os extremos do intervalo estão reservados para usos específicos e não podem ser atribuídos a uma interface:

```
104.198.241.0   | Reservado para representar o endereço de rede.
104.198.241.127 | Reservado como endereço de broadcast; usado para enviar pacotes a todos os hosts de uma rede.
```

Por isso, o intervalo real de IP passa a ser `104.198.241.1 - 104.198.241.126`, que também se poderia obter com uma [calculadora de IP](https://www.calculator.net/ip-subnet-calculator.html).
</br>
</br>

#### Notação CIDR (/24)

A máscara também pode ser representada com o Classless Inter-Domain Routing (CIDR). Esta forma representa a máscara como uma barra "/", seguida do número de bits que servem de endereço de rede.

Assim, a máscara do exemplo acima, `255.255.255.128`, equivale a uma máscara `/25` na notação CIDR, porque 25 bits dos 32 bits representam o endereço de rede.

<div align="right">
  <b><a href="#top">↥ voltar ao topo</a></b>
</div>
</br>

---

### Switch

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/switch1.png?raw=true" height=150 alt="switch"></kbd>
</p>
</br>

Um switch (comutador) liga vários dispositivos entre si numa única rede. Ao contrário de um router, o switch não tem interfaces, porque apenas distribui pacotes na sua rede local e não consegue falar diretamente com uma rede exterior à sua.

<div align="right">
  <b><a href="#top">↥ voltar ao topo</a></b>
</div>
</br>

---

### Router

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/route1.png?raw=true" height=200 alt="router"></kbd>
</p>
</br>

Tal como o switch liga vários dispositivos numa única rede, o router (encaminhador) liga várias redes entre si. O router tem uma interface por cada rede a que se liga.

Como o router separa redes diferentes, o intervalo de endereços IP possíveis numa das suas interfaces não pode sobrepor-se ao intervalo das outras interfaces. Uma sobreposição no intervalo de endereços IP significaria que as interfaces estão na mesma rede.
</br>
</br>

#### Tabela de encaminhamento

</br>
<p align="center">
  <kbd><img src="https://github.com/lpaube/NetPractice/blob/main/img/routing_table1.png?raw=true" height=150 alt="routing_table"></kbd>
</p>
</br>

Uma tabela de encaminhamento (routing table) é uma tabela de dados guardada num router ou num host de rede que lista as rotas para determinados destinos de rede. No NetPractice, a tabela de encaminhamento tem 2 elementos:

- **Destination** (destino): o destino indica um endereço de rede no qual um host é o alvo final dos pacotes. A rota `default` ou `0.0.0.0/0` é a rota que entra em vigor quando não existe outra rota para um endereço IP de destino. A rota predefinida usa o endereço do próximo salto para enviar os pacotes sem indicar um destino específico. A rota predefinida corresponde a qualquer rede.

- **Next hop** (próximo salto): o próximo salto é o router mais próximo por onde um pacote pode passar. É o endereço IP do router seguinte no caminho do pacote. Cada router mantém a sua tabela de encaminhamento com um endereço de próximo salto.

<div align="right">
  <b><a href="#top">↥ voltar ao topo</a></b>
</div>
</br>

## Níveis

<details>
  <summary>Nível 1</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level1_paint.png?raw=true" alt="level1">  
  <br>
  <br>

**1.** Como o _Client A_ e o _Client B_ estão na mesma rede, o endereço IP de ambos tem de representar a mesma rede, de acordo com a máscara de sub-rede.
<br>
A máscara de sub-rede é _255.255.255.0_, o que significa que os primeiros 3 bytes do endereço IP representam a rede e o 4.º byte representa o host. Como estamos na mesma rede, só o host pode mudar.
<br>
A solução será qualquer endereço no intervalo **104.96.23.0 - 104.96.23.255**, excluindo estes 3:

- **104.96.23.0:** o primeiro número do intervalo de hosts (0, neste caso) representa a rede e não pode ser usado por um host.
- **104.96.23.255:** o último número do intervalo de hosts (255, neste caso) representa o endereço de broadcast.
- **104.96.23.12:** este endereço já está a ser usado pelo host _Client B_.

**2.** O mesmo raciocínio do ponto _1._, mas aqui a máscara de sub-rede é _255.255.0.0_. Os primeiros 2 bytes do endereço IP representam a rede e os últimos 2 bytes, o endereço de host.
<br>
A solução será qualquer endereço no intervalo **211.191.0.0 - 211.191.255.255**, excluindo:

- **211.191.0.0:** representa o endereço de rede.
- **211.191.255.255:** representa o endereço de broadcast.
- **211.191.89.75:** já está ocupado pelo host _Client C_.

<div align="right">
  <b><a href="#top">↥ voltar ao topo</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Nível 2</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level2_paint.png?raw=true" alt="level2">
  <br>
  <br>

**1.** Como o _Client B_ está na mesma rede privada que o _Client A_, devem ter exatamente a mesma máscara de sub-rede.
<br>
A solução só pode ser **255.255.255.224**.

**2.** Para perceber a máscara de sub-rede _255.255.255.224_, vejamos a forma binária, juntamente com o IP _192.168.20.222_ do _Client B_:

<center>

```
MÁSCARA: 11111111.11111111.11111111.11100000
IP:      11000000.10101000.00010100.11011101
```

</center>
Como se vê, os primeiros 27 bits representam a parte de rede do endereço IP, enquanto apenas os últimos 5 bits representam o endereço de host.
<br>
Estes 27 bits que representam a rede têm de permanecer iguais nos endereços IP dos hosts da mesma rede. Para obter a resposta, só podemos alterar os últimos 5 bits.
<br>
<br>
A resposta está no intervalo:

```
BIN:  11000000.10101000.00010100.11000000 - 11000000.10101000.00010100.11011111
ou
DEC:  192.168.20.192 - 192.168.20.223
```

Excluindo:
<br>

- **11000000.10101000.00010100.11000000:** representa o endereço de rede (repara que os últimos 5 bits são todos 0).
- **11000000.10101000.00010100.11011111:** representa o endereço de broadcast (repara que os últimos 5 bits são todos 1).
- **11000000.10101000.00010100.11011110:** o _Client B_ já tem esse endereço.

**3.** Aqui somos apresentados à notação de barra "/" para a máscara de sub-rede na _Interface D1_. Uma máscara de sub-rede _/30_ significa que os primeiros 30 bits do endereço IP representam o endereço de rede e os 2 bits restantes representam o endereço de host:

<center>

```
Máscara /30: 11111111.11111111.11111111.11111100
```

</center>

Este número binário corresponde ao decimal _255.255.255.252_, logo é idêntico à máscara da _Interface C1_.
<br>
<br>
As respostas podem ser qualquer endereço, desde que cumpram as seguintes condições:

- O endereço de rede (primeiros 30 bits) tem de ser idêntico para o _Client D_ e o _Client C_.
- Os bits de host (últimos 2 bits) não podem ser todos 1, nem todos 0.
- O _Client D_ e o _Client C_ não podem ter endereços IP idênticos.

<div align="right">
  <b><a href="#top">↥ voltar ao topo</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Nível 3</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level3_paint.png?raw=true" alt="level3">
  <br>
  <br>

Este exercício introduz o uso do **switch** (_Switch S_ neste exemplo). O switch liga vários hosts da mesma rede.
<br>
<br>

**1.** O _Client A_, o _Client B_ e o _Client C_ estão todos na mesma rede. Por isso, têm de ter todos a mesma máscara de sub-rede. Como o _Client C_ já tem a máscara _255.255.255.128_, a máscara da _Interface B1_ e da _Interface A1_ também será _255.255.255.128_ (ou, em notação de barra: _/25_).
<br>
<br>
O endereço IP da _Interface B1_ e da _Interface C1_ tem de estar no mesmo intervalo de rede que o IP do _Client A_. Esse intervalo é:

  <center>

```
104.198.241.0 - 104.198.241.128
```

  </center>
  Excluindo, claro, o endereço de rede e o endereço de broadcast.

  <div align="right">
  <b><a href="#top">↥ voltar ao topo</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Nível 4</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level4_paint.png?raw=true" alt="level4">
  <br>
  <br>

Este exercício introduz o **router**. O router serve para ligar várias redes entre si. Faz isso através de várias interfaces (_Interface R1_, _Interface R2_ e _Interface R3_ neste exemplo).
<br>
<br>

**1.** Como nenhuma das máscaras da _Interface B1_, da _Interface A1_ e da _Interface R1_ está preenchida, podemos escolher a nossa própria máscara de sub-rede. Uma máscara **/24** é ideal, porque nos deixa o 4.º byte inteiro para o endereço de host e não exige cálculos binários para encontrar o intervalo de endereços de host possíveis.
<br>
<br>
O endereço IP da _Interface B1_ e da _Interface R1_ tem de ter o mesmo endereço de rede que o endereço IP da _Interface A1_. Com uma sub-rede _/24_, o intervalo possível é:

  <center>

```
85.17.5.0 - 85.17.5.255
```

  </center>
  Excluindo o endereço de rede e o endereço de broadcast.
  <br>
  <br>

Repara que não interagimos com as interfaces _Interface R2_ e _Interface R3_ do router, porque nenhuma das nossas comunicações tinha de chegar a esses lados do router.

  <div align="right">
  <b><a href="#top">↥ voltar ao topo</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Nível 5</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level5_paint.png?raw=true" alt="level5">
  <br>
  <br>

Este nível introduz as **rotas**. Uma rota tem 2 campos: o primeiro é o **destination** (destino) dos pacotes de saída e o segundo é o **next hop** (próximo salto) dos pacotes.
<br>

O **destino** _default_ equivale a _0.0.0.0/0_, que envia os pacotes sem distinção para o primeiro endereço de rede que encontrar. Um endereço de destino _122.3.5.3/24_ enviaria os pacotes para a rede _122.3.5.0_.

  <br>
  O **próximo salto** é o endereço IP da interface do router seguinte (ou da Internet) para a qual a interface da máquina atual tem de enviar os seus pacotes.
  <br>
  <br>

**1.** O _Client A_ só tem 1 rota pela qual pode enviar os seus pacotes. Não vale a pena especificar um destino numérico. O destino _default_ envia os pacotes pelo único caminho disponível.
<br>
<br>
O endereço de próximo salto tem de ser o endereço IP da interface do router seguinte no caminho dos pacotes. A interface seguinte é a _Interface R1_, com o endereço IP _54.117.30.126_. Repara que a interface seguinte não é a _Interface A1_, porque essa é a própria interface do emissor.

  <div align="right">
  <b><a href="#top">↥ voltar ao topo</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Nível 6</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level6_paint.png?raw=true" alt="level6">
  <br>
  <br>

Este nível introduz a **Internet**. A Internet comporta-se como um router. No entanto, se uma interface estiver ligada direta ou indiretamente à Internet, **não pode** ter um endereço IP nos seguintes intervalos reservados de IP privados:

```
192.168.0.0 - 192.168.255.255 (65 536 endereços IP)
172.16.0.0 - 172.31.255.255   (1 048 576 endereços IP)
10.0.0.0 - 10.255.255.255     (16 777 216 endereços IP)
```

**1.** O **next hop** da Internet já está preenchido e coincide com o endereço IP da _Interface R2_. Por isso, só precisamos de tratar do destino da Internet.
<br>
<br>
A Internet tem de enviar os seus pacotes para o _Client A_. Para isso, o destino da Internet tem de coincidir com o endereço de rede do _Client A_. Vamos encontrar o endereço de rede do _Client A_:
<br>
A máscara do _Client A_ é _255.255.255.128_, que equivale a _/25_. Isto significa que os primeiros 25 bits do endereço IP são o endereço de rede. Sabemos então que os primeiros 3 bytes (24 bits) do endereço IP fazem parte do endereço de rede:

  <center>

```
40.178.145.?
```

  </center>

Agora só falta saber se o 25.º bit é 1 ou 0.
<br>
Se convertermos o número 227 para binário, obtemos `11100011`. O primeiro dígito, que corresponde ao 25.º bit, é 1. Como só o 25.º bit faz parte do endereço de rede, e não os restantes 7 bits, obtemos `10000000` para o último byte do endereço de rede, que é 128 em decimal.
<br>
<br>
O endereço de rede completo é:

  <center>

```
40.178.145.128
```

  </center>

Com um intervalo de _40.178.145.129 - 40.178.145.254_ para os endereços de host.
<br>
<br>
Podemos agora colocar este endereço, **40.178.145.128**, no destino da Internet. O **/25** a seguir ao endereço de destino representa a máscara aplicada a esse endereço.
<br>
<br>
Um destino _40.178.145.227/25_ equivale ao endereço de destino _40.178.145.128/25_, porque a máscara _/25_ põe a 0 todos os bits depois do 25.º para obter o endereço de rede do destino.

  <div align="right">
  <b><a href="#top">↥ voltar ao topo</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Nível 7</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level7_paint.png?raw=true" alt="level7">
  <br>
  <br>

Este nível introduz o conceito de **sobreposições** (overlaps). O intervalo de endereços IP de uma rede não pode sobrepor-se ao intervalo de endereços IP de outra rede. As redes são separadas por routers.
<br>
<br>

**1.** Temos 3 redes distintas:
<br>

1. Entre o _Client A_ e o _Router R1_.
2. Entre o _Router R1_ e o _Router R2_.
3. Entre o _Router R2_ e o _Client C_.

Na _Interface A1_, não podemos escolher o endereço IP livremente, porque o IP da _Interface R11_ já está preenchido. Além disso, se lhe dermos uma máscara _/24_, o intervalo de endereços IP vai sobrepor-se ao intervalo da _Interface R12_, que já está preenchido. Ambos ficariam no intervalo _93.198.14.0 - 93.198.14.255_.
<br>
<br>

Como precisamos de endereços para 3 redes distintas, convém dividir os últimos bytes do endereço em 4 ou mais intervalos. Fazemo-lo com uma máscara _/26_ ou superior. A máscara _/28_, por exemplo, dá-nos 16 intervalos, dos quais usamos estes 3:

```
93.198.14.1 - 93.198.14.14    (Client A até Router R1)
93.198.14.65 - 93.198.14.78   (Router R1 até Router R2)
93.198.14.241 - 93.198.14.254 (Router R2 até Client C)
```

Para calcular os intervalos possíveis de uma máscara:
<br>
https://www.calculator.net/ip-subnet-calculator.html?cclass=any&csubnet=28&cip=93.198.14.2&ctype=ipv4&printit=0&x=97&y=13

  <div align="right">
  <b><a href="#top">↥ voltar ao topo</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Nível 8</summary>
  <br>
  <img src="img/level8Paint_v2.png" alt="level8">
  <br>
  <br>

**1.** Os hosts _Client C_ e _Client D_ vão enviar pacotes para a Internet e, depois, a Internet responde enviando pacotes de volta até ao emissor inicial. Para enviar esses pacotes, a Internet usa o destino _49.175.13.0/26_, que envia os pacotes para as redes no intervalo `49.175.13.0 - 49.175.13.63`.
<br>
<br>
Todas as redes que recebem pacotes têm de estar neste intervalo, sem se sobreporem umas às outras.
<br>
<br>

**2.** Na _Interface R23_ e na _Interface R22_ usamos a máscara _255.255.255.240_ (ou _/28_), para dividir de forma prática o intervalo _/26_ do endereço de destino em 4 intervalos distintos. Esta divisão em 4 é necessária porque temos as seguintes 3 redes, que não se podem sobrepor:
<br>

1. _Router R1_ até _Router R2_.
2. _Router R2_ até _Client C_.
3. _Router R2_ até _Client D_.

A cada uma destas redes pode ser atribuído um dos seguintes intervalos de IP, com máscara _/28_:

```
49.175.13.0 - 49.175.13.15
49.175.13.16 - 49.175.13.31
49.175.13.32 - 49.175.13.47
49.175.13.48 - 49.175.13.63
```

Repara que o endereço de rede (o primeiro) e o endereço de broadcast (o último) têm de ser excluídos de cada intervalo.
<br>
<br>

**3.** O destino e o próximo salto da Internet já estão preenchidos. Só precisamos de preencher o próximo salto do _Router R2_, que é o IP da _Interface R21_.

<div align="right">
  <b><a href="#top">↥ voltar ao topo</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Nível 9</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level9_paint.png?raw=true" alt="level9">
  <br>
  <br>

Este nível é bastante direto, porque a Internet não envia inicialmente os seus pacotes para uma rede específica. Por isso, as redes distintas não precisam de partilhar um intervalo de endereços comum. A sugestão é seguir simplesmente os 6 objetivos do nível, um a um, até o nível ficar concluído.
<br>
<br>
Lembra-te de não usar endereços de rede dos intervalos reservados de IP privados.
<br>
<br>

**1.** O **objetivo 3** diz que temos de ligar o _meson_ à _Internet_. A _Internet_ terá depois de responder ao _meson_, por isso introduzimos o endereço de rede do _meson_ no destino da _Internet_.
<br>
<br>
O **objetivo 6** diz que temos de ligar o _cation_ à _Internet_, por isso introduzimos o endereço de rede do _cation_ no destino da _Internet_.
<br>
<br>
É normal haver um campo vazio no 3.º destino da _Internet_ e no destino do _Router R1_. Nem todos os campos das tabelas de encaminhamento precisam de ser preenchidos.

  <div align="right">
  <b><a href="#top">↥ voltar ao topo</a></b>
</div>
</br>

</details>

---

<details>
  <summary>Nível 10</summary>
  <br>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level10_paint.png?raw=true" alt="level10">
  <br>
  <br>

Neste nível existem 4 redes diferentes:
<br>

1. _Router R1_ até _Switch S1_
2. _Router R1_ até _Router R2_
3. _Router R2_ até _Client H4_
4. _Router R2_ até _Client H3_
   <br>

**1.** A Internet tem de conseguir enviar os seus pacotes a todos os hosts, por isso o destino tem de cobrir o intervalo de redes de todos os hosts.
<br>
<br>

A _Interface R11_ e a _Interface R13_ já têm um endereço IP preenchido. Este endereço IP só difere no último byte. A _Interface R11_ tem como último byte **1** e a _Interface R13_ tem como último byte **254**. Para cobrir este intervalo tão largo de endereços IP, usamos uma máscara **/24** no destino da _Internet_. Este destino cobre o intervalo `70.101.30.0 - 70.101.30.255`.

  <br>
  <br>

**2.** Ao escolher os endereços IP, temos de garantir 2 coisas:
<br>

1. O endereço IP está coberto pelo destino da _Internet_.
2. O intervalo de endereços IP das várias redes não se sobrepõe.
   <br>

Com os endereços IP já preenchidos (a cinzento), vejamos os intervalos cobertos pelas várias redes:
<br>

1. _Router R1_ até _Switch S1_ — cobre o intervalo **70.101.30.0 - 70.101.30.127** (máscara /25).
2. _Router R2_ até _Client H4_ — cobre o intervalo **70.101.30.128 - 70.101.30.191** (máscara /26).
3. _Router R1_ até _Router R2_ — cobre o intervalo **70.101.30.252 - 70.101.30.255** (máscara /30).
4. _Router R2_ até _Client H3_ — ??? (máscara ???).

Os únicos endereços IP que restam para a rede "Router R2 até Client H3" são **70.101.30.192 - 70.101.30.251**. Podemos escolher qualquer máscara que nos permita tirar 2 endereços IP desse intervalo para colocar na _Interface R22_ e na _Interface R31_.

  <div align="right">
  <b><a href="#top">↥ voltar ao topo</a></b>
</div>
</br>

</details>

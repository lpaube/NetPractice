# NetPractice

<details>
  <summary>Level 1</summary>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level1_paint.png?raw=true" alt="level1">  
  <br>
  <br>

![#ff0000](https://via.placeholder.com/15/ff0000/000000?text=+)
**1.** Since *Client A* and *Client B* are on the same network, their IP address must represent the same network in accordance to the subnet mask.
<br>
The subnet mask is *255.255.255.0*, which means that the first 3 bytes of the IP address represent the network, and the 4th byte represents the host. Since we are on the same network, only the host can change. 
<br>
The solution will be anything in the range of **104.96.23.0 - 104.96.23.255** excluding the following 3:
* **104.96.23.0:** The first number in the range of hosts (0 in this case) represents the network and cannot be used by a host.
* **104.96.23.255:** The last number in the range of hosts (255 in this case) represents the broadcast address.
* **104.96.23.12:** This address is already used by the host *Client B*.

![#ca00ea](https://via.placeholder.com/15/ca00ea/000000?text=+)
**2.** Same reasoning as *1.*, however the subnet mask is *255.255.0.0* in this case. The first 2 bytes of the IP address will represent the network; and the last 2 bytes, the host address.
<br>
The solution will be anything in the range of **211.191.0.0 - 211.191.255.255**, excluding:
* **211.191.0.0:** Represents the network address.
* **211.191.255.255:** Represents the broadcast address.
* **211.191.89.75:** Already taken by host *Client C*.

</details>

---

<details>
  <summary>Level 2</summary>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level2_paint.png?raw=true" alt="level2">
  <br>
  <br>

![#ff0000](https://via.placeholder.com/15/ff0000/000000?text=+)
**1.** Since *Client B* is on the same private network as *Client A*, they should have the exact same subnet mask.
<br>
The solution can only be **255.255.255.224**.

![#ff0000](https://via.placeholder.com/15/ff0000/000000?text=+)
**2.** To understand the subnet mask of *255.255.255.224*, let's look at it in binary form, along with the IP *192.168.20.222* of *Client B*:

<center>

```
MASK: 11111111.11111111.11111111.11100000
IP:   11000000.10101000.00010100.11011101
```
</center>
As we can see, the first 27 bits represent the IP address, while only the last 5 bits represent the host address.
<br>
All these 27 bits representing the network must stay the same in the IP addresses of hosts on the same network. To get the answer, we can only change the last 5 bits.
<br>
<br>
The answer is in the range of:

```
BIN:  11000000.10101000.00010100.11000000 - 11000000.10101000.00010100.11011111
or
DEC:  192.168.20.192 - 192.168.20.223
```
Excluding:
<br>
* **11000000.10101000.00010100.11000000:** Represents the network address (notice all 0 in the last 5 bits).
* **11000000.10101000.00010100.11011111:** Represents the broadcast address (notice all 1 in the last 5 bits).
* **11000000.10101000.00010100.11011110:** *Client B* already has that address.

![#ca00ea](https://via.placeholder.com/15/ca00ea/000000?text=+)
**3.** Here we are introduced to the slash "/" notation for the subnet mask on *Interface D1*. A subnet mask of */30* means that the first 30 bits of the IP address represent the network address, and the remaining 2 bits represent the host address:
<center>

```
Mask /30: 11111111.11111111.11111111.11111100
```
</center>

We can see that this binary number corresponds to the decimal *255.255.255.252*, therefore it is identical to the mask found on *Interface C1*.
<br>
<br>
The answers can then be any addresses, as long as they meet the following conditions:
* The network address (first 30 bits) must be identical for *Client D* and *Client C*.
* The host bits (last 2 bits) cannot be all 1, nor all 0.
* *Client D* and *Client C* do not have identical IP addresses.
</details>

---

<details>
  <summary>Level 3</summary>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level3_paint.png?raw=true" alt="level3">
  <br>
  <br>

  This exercise introduces the use of the **switch** (*Switch S* in this example). The switch links multiple hosts of the same network together.
  <br>
  <br>

  ![#ff0000](https://via.placeholder.com/15/ff0000/000000?text=+)
  **1.** *Client A*, *Client B*, and *Client C* are all on the same network. Therefore, they must all have the same subnet mask. Since *Client C* already has the mask *255.255.255.128*, the mask for *Interface B1* and for *Interface A1* will also be *255.255.255.128* (or in slash notation: */25*).
  <br>
  <br>
  The IP address of *Interface B1* and *Interface C1* must be on the same network range as the IP of *Client A*. This range is:
  <center>

  ```
  104.198.241.0 - 104.198.241.128 
  ```
  </center>
  Excluding of course the network address and the broadcast address.
</details>

---

<details>
  <summary>Level 4</summary>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level4_paint.png?raw=true" alt="level4">
  <br>
  <br>

  This exercise introduces the **router**. The router is used to link multiple networks together. It does so with the use of multiple interfaces (*Interface R1*, *Interface R2*, and *Interface R3* in this example).
  <br>
  <br>

  ![#ff0000](https://via.placeholder.com/15/ff0000/000000?text=+)
  **1.** Since none of the masks on *Interface B1*, *Interface A1*, and *Interface R1* are entered, we are free to chose our own subnet mask. A mask of **/24** is ideal as it leaves us with the entire 4th byte for the host address, and does not require binary calculations to find the range of possible host addresses.
  <br>
  <br>
  The IP address of *Interface B1* and *Interface R1* must have the same network address as the IP address of *Interface A1*. With a subnet of */24*, the possible range is:
  <center>

  ```
  85.17.5.0 - 85.17.5.255
  ```
  </center>
  Excluding the network address and the broadcast address.
  <br>
  <br>

  Note that we did not interact with the router *Interface R2* and *Interface R3*, since none of our communications had to reach these sides of the router.
</details>

---

<details>
  <summary>Level 5</summary>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level5_paint.png?raw=true" alt="level5">
  <br>
  <br>

  This level introduces **routes**. A route contains 2 fields, the first one is the **destination** of outbound packets, the second one is the **next hop** of the packets.
  <br>
  The **destination** *default* is equivalent to *0.0.0.0/0*, which will send the packets undiscriminately to the first network address it encounters. A destination address of *122.3.5.3/24* would send the packets to the network *122.3.5.0*.
  <br>
  The **next hop** is the IP address of the next  router (or internet) interface to which the interface of the current machine must send its packets. 
  <br>
  <br>

  ![#ff0000](https://via.placeholder.com/15/ff0000/000000?text=+)
  **1.** *Client A* only has 1 route through which it can send its packets. There is no use specifying a numbered destination. The destination *default* will send the packets to the only path available.
  <br>
  <br>
  The next hop address must be the IP address of the next router's interface on the packets' way. The next interface is *Interface R1*, with the IP address of *54.117.30.126*. Note that the next interface is not *Interface A1*, since this is the sender's own interface.
</details>

---

<details open>
  <summary>Level 6</summary>
  <img src="" alt="level6">
  <br>
  <br>

  This level introduces the **internet**. The internet behaves like a router. However, if an interface is connected directly or indirectly to the internet, it **cannot** have an IP address in the following reserved private IP ranges:


  ```
  192.168.0.0 - 192.168.255.255 (65,536 IP addresses)
  172.16.0.0 - 172.31.255.255   (1,048,576 IP addresses)
  10.0.0.0 - 10.255.255.255     (16,777,216 IP addresses)
  ```
  ![#ff0000](https://via.placeholder.com/15/ff0000/000000?text=+)
  **1.** The **next hop** of the internet is already entered, and matches the IP address of the *Interface R2*. Therefore we only need to bother with the destination of the internet.
  <br>
  <br>
  The internet must send its packets to *Client A*, and to do so, the internet's destination must match the network address of *Client A*. Let's find the network address of *Client A*:
  <br>
  *Client A*'s mask is *255.255.255.128*, which is equivalent to */25*. This means that the first 25 bits of its IP address is its network address. We know then that the first 3 bytes (24 bits) of its IP address makes part of its network address:
  <center>

  ```
  40.178.145.?
  ```
  </center>

  We now only need to find out if the 25th bit is a 1 or a 0.
  <br>
  If we convert the number 227 to binary, we get **11100011**. The first digit, which corresponds to the 25th bit, is a 1. Since only the 25th bit is part of the network address, and not the remaining 7 bits, we get **10000000** for the last bytes of the network address, which is 128 in decimal.
  <br>
  <br>
  The full network address is:
  <center>

  ```
  40.178.145.128
  ```
  </center>

  With a range of *40.178.145.129 - 40.178.145.254* for its host addresses.
  <br>
  <br>
  We can now put this address of **40.178.145.128** in the Internet destination. The **/25** following the destination address represents the mask applied to its address.
  <br>
  <br>
  A destination of *40.178.145.227/25* is equivalent to the destination address *40.178.145.128/25*, since the mask of */25* will cutout all the bits after the 25th bit to determine the destination's network address.

</details>

---
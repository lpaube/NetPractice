# NetPractice

<details open>
  <summary>Level 1</summary>
  <img src="https://github.com/LPaube/42_NetPractice/blob/main/img/level1_paint.png?raw=true" alt="level1"</img>  
  <br>
  <br>

![#ff0000](https://via.placeholder.com/15/ff0000/000000?text=+)
**1.** Since "Client A" and "Client B" are on the same private network, their IP address must represent the same network in accordance to the subnet mask.
<br>
The subnet mask is "255.255.255.0", which means that the first 3 bytes of the IP address represent the network, and the 4th byte represents the host. Since we are on the same network, only the host can change. 
<br>
The solution will be anything in the range of "104.96.23.0" - "104.96.23.255" excluding the following 3:
* **104.96.23.0:** The first number in the range of hosts (0 in this case) represents the network and cannot be used by a host.
* **104.96.23.255:** The last number in the range of hosts (255 in this case) represents the broadcast address.
* **104.96.23.12:** This address is already used by the host "Client B".

![#ca00ea](https://via.placeholder.com/15/ca00ea/000000?text=+)
**2.** Same reasoning as "1.", however the subnet mask is "255.255.0.0" in this case. The first 2 bytes of the IP address will represent the network; and the last 2 bytes, the host address.
<br>
The solution will be anything in the range of "211.191.0.0" - "211.191.255.255", excluding:
* **211.191.0.0:** Represents the network address.
* **211.191.255.255:** Represents the broadcast address.
* **211.191.89.75:** Already taken by host "Client C".

</details>

---

<details open>
  <summary>Level 2</summary>

</details>

---
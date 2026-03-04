Lo primero ha realizar es preparar el laboratorio, asique utilizando VMware importo la máquina Metasploitable y creo una VM de Kali Linux que utilizaré como mi máquina principal, luego creo una red virtual y la asigno a los adaptadores de red de la máquina Kali linux y Metasploitable <br>
<img width="454" height="144" alt="image" src="https://github.com/user-attachments/assets/6d00ba28-92df-4ef0-b66d-f0239bc37247" />

Utilizo netdiscover para ver los hosts que hay en la red y veo que la IP de la máquina metasploitable es 192.168.92.137

<img width="379" height="37" alt="image" src="https://github.com/user-attachments/assets/76950e22-9c05-4a01-b632-195d8d600f35" /><br>
<img width="623" height="132" alt="image" src="https://github.com/user-attachments/assets/942a1919-4230-409d-bf3a-6c576d027e19" />

Realizo un escaneo con nmap sobre todos los puertos de la máquina, realizo un SYN SCAN para que al recibir confirmación de que el puerto está abierto se cierre la conexión para no completarla y así el escaneo sea mas sigiloso y rápido, activo el triple verbose para que me muestre toda la información posible durante el escaneo y guardo el resultado en un archivo de salida, al ser una máquina muy vulnerable se puede apreciar que hay una gran cantidad de puertos expuestos.<br>
<img width="549" height="657" alt="image" src="https://github.com/user-attachments/assets/7a8738ca-f41f-456a-b4ad-a3e5070d2c70" />

Con el siguiente comando filtro todos los puertos descubiertos por nmap para poder copiarlos en el siguiente comando de nmap
<img width="1433" height="55" alt="image" src="https://github.com/user-attachments/assets/2e913270-6601-4979-a21b-873ec4b67665" />

Realizo un escaneo de vulnerabilidades sobre todos los puertos que he descubierto
<img width="1476" height="667" alt="image" src="https://github.com/user-attachments/assets/0923dae2-b0c7-41d6-a052-cefecbe2790e" />

Lo primero ha realizar es preparar el laboratorio, asique creo una red virtual y la asigno a los adaptadores de red de la máquina Kali linux que utilizaré como herramienta y a la máquina metasploitable <br>
<img width="454" height="144" alt="image" src="https://github.com/user-attachments/assets/6d00ba28-92df-4ef0-b66d-f0239bc37247" />

Utilizo netdiscover para ver los hosts que hay en la red y veo que la IP de la máquina metasploitable es 192.168.92.137

<img width="379" height="37" alt="image" src="https://github.com/user-attachments/assets/76950e22-9c05-4a01-b632-195d8d600f35" /><br>
<img width="623" height="132" alt="image" src="https://github.com/user-attachments/assets/942a1919-4230-409d-bf3a-6c576d027e19" />

Realizo un escaneo con nmap sobre todos los puertos de la máquina, realizo un SYN SCAN para que al recibir confirmación de que el puerto está abierto se cierre la conexión para no completarla y así el escaneo sea mas sigiloso y rápido, activo el triple verbose para que me muestre toda la información posible durante el escaneo y guardo el resultado en un archivo de salida. Al ser una máquina muy vulnerable se puede apreciar que hay una gran cantidad de puertos expuestos.<br>
<img width="549" height="657" alt="image" src="https://github.com/user-attachments/assets/7a8738ca-f41f-456a-b4ad-a3e5070d2c70" />

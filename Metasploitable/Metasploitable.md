Lo primero ha realizar es preparar el laboratorio, asique utilizando VMware importo la máquina Metasploitable y creo una VM de Kali Linux que utilizaré como mi máquina principal, luego creo una red virtual y la asigno a los adaptadores de red de la máquina Kali linux y Metasploitable <br>
<img width="454" height="144" alt="image" src="https://github.com/user-attachments/assets/6d00ba28-92df-4ef0-b66d-f0239bc37247" />

Utilizo netdiscover para ver los hosts que hay en la red y veo que la IP de la máquina metasploitable es 192.168.92.137

<img width="379" height="37" alt="image" src="https://github.com/user-attachments/assets/76950e22-9c05-4a01-b632-195d8d600f35" /><br>
<img width="623" height="132" alt="image" src="https://github.com/user-attachments/assets/942a1919-4230-409d-bf3a-6c576d027e19" />

Realizo un escaneo con nmap sobre todos los puertos de la máquina, realizo un SYN SCAN para que al recibir confirmación de que el puerto está abierto se cierre la conexión para no completarla y así el escaneo sea mas sigiloso y rápido, activo el triple verbose para que me muestre toda la información posible durante el escaneo y guardo el resultado en un archivo de salida, al ser una máquina muy vulnerable se puede apreciar que hay una gran cantidad de puertos expuestos.<br>
<img width="549" height="657" alt="image" src="https://github.com/user-attachments/assets/7a8738ca-f41f-456a-b4ad-a3e5070d2c70" />

Con este comando filtro todos los puertos descubiertos por nmap para poder copiarlos en el siguiente comando de nmap
<img width="1433" height="55" alt="image" src="https://github.com/user-attachments/assets/2e913270-6601-4979-a21b-873ec4b67665" />

Realizo un escaneo de versiones sobre todos los puertos que he descubierto
<img width="1476" height="667" alt="image" src="https://github.com/user-attachments/assets/0923dae2-b0c7-41d6-a052-cefecbe2790e" />

Luego realizo un escaneo de vulnerabilidades utilizando los scripts por defecto de nmap
<img width="1483" height="30" alt="image" src="https://github.com/user-attachments/assets/de9ea56b-709b-4aa9-bd37-942e8983f8f6" />

Hay vulnerabilidades en la mayoria de los puertos, asique realizo una investigación sobre los mas relevantes:

> [Puerto 21](https://github.com/alvaro2347/alvaro347/blob/main/Metasploitable/Puerto%2021.md)
> [Puerto 22](https://github.com/alvaro2347/alvaro347/blob/main/Metasploitable/Puerto%2022.md)
> [Puerto 23](https://github.com/alvaro2347/alvaro347/blob/main/Metasploitable/Puerto%2023.md)
> [Puerto 25]
> [Puerto 111]
> [Puertos 139 y 445]
> [Puerto 1524]
> [Puerto 3306]
> [Puerto 3632]
> [Puerto 5900]

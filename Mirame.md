# Mirame

Se realiza un escaneo con nmap sobre la máquina, ejecutando scripts por defecto y realizando detección de versiones de servicios, se encuentra un servicio SSH y una web apache que indica ser una página de login <br>
<img width="765" height="331" alt="image" src="https://github.com/user-attachments/assets/a79f69a0-386c-412d-a1e9-ba78f439b9aa" /><br>
Accediendo a la página, se puede ver que efectivamente es una página de login, asique se prueba una inyección de código sqli básico, se consigue acceder, comprobando que la página es vulnerable a sqlinjection<br>
<img width="497" height="404" alt="image" src="https://github.com/user-attachments/assets/7c2bffea-ce69-45d1-b5f2-625656ef54f8" /><br>
Una vez realizado el login, en la página no se puede realizar ninguna otra acción que pueda resultar util para la explotación, por lo que se utiliza la herramienta sqlmap para intentar obtener las bases de datos que corren detras de la web, con lo que se localiza la BBDD users<br>
<img width="873" height="836" alt="image" src="https://github.com/user-attachments/assets/9c850313-1c71-4555-afd2-136307ea0c0b" /><br>
Se obtienen las tablas de la BBDD users, en este caso, la tabla usuarios <br>
<img width="865" height="853" alt="image" src="https://github.com/user-attachments/assets/41aa53fd-6e5e-4946-88b1-4e463ada75e3" /><br>
Se extraen los datos de la tabla usuarios, con ello se obtienen las columnas y sus valores<br>
<img width="668" height="1205" alt="image" src="https://github.com/user-attachments/assets/8d00ca7c-e247-42b4-a790-dfe492d422f8" /><br>
Ya que indica que son usuarios, se intenta realizar conexión por SSH con las credenciales obtenidas, pero no se logra, por lo que al ver que una de las credenciales obtenidas se llama directoriotravieso, se intenta acceder mediante la web, se logra acceder y en esta se ubica una imagen, asique se realiza su descarga<br>
<img width="555" height="336" alt="image" src="https://github.com/user-attachments/assets/67513884-02f0-461a-b801-877916b81c72" /><br>
Utilizando steghide se intenta extraer algún archivo oculto que pueda tener la imagen, pero parece estar encriptada, con stegseek se realiza fuerza bruta obteniendo así la contraseña requerida para desencriptarla<br>
<img width="496" height="114" alt="image" src="https://github.com/user-attachments/assets/98f6eb05-97ae-454b-9ce5-a4c548acfba8" /><br>
Utilizando steghide con la contraseña obtenida, se consigue exctraer un arcivo comprimido<br>
<img width="335" height="75" alt="image" src="https://github.com/user-attachments/assets/9549c5a3-a36c-45e4-a92e-8f53b9cf6d74" /><br>
El archivo obtenido también requiere de contraseña para descomprimirse, asique utilizando la herramienta john the ripper, se obtiene un hash que pueda ser tratado por john y tras tratarlo, se obtiene la contraseña <br>
<img width="1099" height="231" alt="image" src="https://github.com/user-attachments/assets/194445fd-490e-4d94-835f-84c0b42b6da9" /><br>
Tras descomprimir el archivo utilizando la contraseña obtenida, se obtiene un archivo txt, este contiene unas credenciales, que al introducirlas mediante SSH, se obtiene una shell<br>
<img width="631" height="488" alt="image" src="https://github.com/user-attachments/assets/ff9bd863-9a04-4628-9752-9b31c2d4b882" /><br>
Se buscan archivos en el sistema que tengan el bit de SUID activado y se encuentra que find lo tiene activo, se busca en GTFOBins un comando que corresponda para aprovecharse de ello y tras ejecutarlo se consigue elevar privilegios a root<br>
<img width="522" height="290" alt="image" src="https://github.com/user-attachments/assets/f4010513-daf9-44dd-b93b-201a26668bc4" />





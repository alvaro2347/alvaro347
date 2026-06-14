# RootMe

Con un escaneo de nmap se descubre que la máquina objetivo tiene un servicio SSH en el puerto 22 y una web en el puerto 80
<img width="767" height="369" alt="Image" src="https://github.com/user-attachments/assets/209c4cba-94ef-4b84-a392-c7ebee010ad5" />

Se utiliza la herramienta gobuster para buscar directorios ocultos en la web, encontrando así los directorios panel y uploads
<img width="811" height="690" alt="Image" src="https://github.com/user-attachments/assets/a1f36ecb-7c24-407d-b7f5-1a6b9c0e85a1" />

Se crea un archivo llamado shell.php, el cual se subirá a traves del directorio panel, este archivo contiene código que permitira ejecutar comandos de shell desde la url de la víctima escribiendo el nombre del archivo seguido de "?cmd=" y seguido del comando a ejecutar
<img width="516" height="32" alt="Image" src="https://github.com/user-attachments/assets/42255b3f-6ec2-47d5-92e0-0e9866c26639" />

Tras intentar subir el archivo se observa que la web no permite la subida de archivos php, asique con BurpSuite se intercepta la petición que realiza la web al intentar subir el archivo y se envia al intruder para intentar subirlo probando diferentes tipos de archivo
<img width="1969" height="714" alt="Image" src="https://github.com/user-attachments/assets/6ee648db-e914-4027-b13b-e771507b2eca" />

Se ve que el resto de formatos si que permite subirlos
<img width="830" height="565" alt="Image" src="https://github.com/user-attachments/assets/0439b5f0-a794-4ca2-b674-5846e42a55e0" />

Se codifica en url el siguiente comando que se encargará de enviar una shell reversa a la máquina Kali
<img width="477" height="287" alt="Image" src="https://github.com/user-attachments/assets/78034141-2a50-4fd5-a81a-a46a264447bc" />

Se ejecuta desde el directorio uploads el archivo shell.phtml y se ejecuta desde la url el comando codificado anteriormente
<img width="1201" height="163" alt="Image" src="https://github.com/user-attachments/assets/18ef39ca-cd8d-46ed-9976-36912d7dc3d8" /><br>

En el netcat que se habia dejado a la escucha, se obtiene la shell como usuario www-data, asique se buscan archivos que tengan activado el bit SUID para aprovecharlos y escalar privilegios<br>
<img width="730" height="627" alt="Image" src="https://github.com/user-attachments/assets/60cc0bd9-038c-464f-afd8-5428647e4dbf" />

Se observa que tiene el bit SUID activo en python, asique se busca información al respecto en GTFOBins encontrando así el siguiente comando, asique se ejecuta y así se consigue escalar al usuario root<br>
<img width="838" height="79" alt="Image" src="https://github.com/user-attachments/assets/30e83fd9-3f8b-49a1-b069-77350191522a" />

Se buscan en el sistema las flags del usuario y de root y se consigue obtener su contenido<br>
<img width="243" height="127" alt="Image" src="https://github.com/user-attachments/assets/563a4051-4b13-4372-87bf-7ca1f6e8772e" />

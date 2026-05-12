# Blog

Realizo un escaneo con nmap sobre la máquina, ejecutando scripts por defecto y realizando detección de versiones de servicios, encuentro un SSH, una web apache y un servicio Samba<br>
<img width="757" height="727" alt="image" src="https://github.com/user-attachments/assets/a4a98dd3-a5a0-4832-85e2-4af4c0bd830c" /><br>

Utilizando whatweb veo que la página está desarrollada usando Wordpress, asique utilizaré wpscan para analizar la web<br>
<img width="1698" height="71" alt="image" src="https://github.com/user-attachments/assets/d9e7e459-1806-460d-80a2-3ef2241e1f7e" /><br>

Con gobuster veo que en la dirección wp-admin tiene una página de login<br>
<img width="707" height="670" alt="image" src="https://github.com/user-attachments/assets/b14f856c-8b6d-4b51-8af7-63d728264eaa" /><br>
Para acceder a wp-admin, es necesario utilizar el dominio blog.thm en lugar de la dirección IP. Por este motivo, en /etc/hosts añado una entrada que asocia la IP de la máquina victima con blog.thm, de modo que el sistema pueda resolver correctamente el nombre de dominio<br>
<img width="427" height="122" alt="image" src="https://github.com/user-attachments/assets/1b1333d8-765c-4442-acba-9e0f5fd7d47d" /><br>

utilizo wpscan para escanear la web y enumerar usuarios y plugin vulnerables<br>
<img width="511" height="722" alt="image" src="https://github.com/user-attachments/assets/b85c36fb-30f2-4fef-ab29-0ac7fabaa52a" /><br>
<img width="556" height="644" alt="image" src="https://github.com/user-attachments/assets/1299bae5-4427-4777-85bd-8a5897de2eea" /><br>

Como vemos en la anterior imagen, no encuentra ningún plugin vulnerable, pero si varios usuarios, asique guardo esos usuarios en un archivo y realizo fuerza bruta<br>
<img width="618" height="294" alt="image" src="https://github.com/user-attachments/assets/6e5374ed-efef-4738-976f-aec51c94b932" /><br>
Gracias a esto encuentro la contraseña de kwheel<br>
<img width="816" height="295" alt="image" src="https://github.com/user-attachments/assets/71d8d409-6ec6-4f94-868c-1e26dffee40f" /><br>

Con las credenciales obtenidas accedo a la web, pero desde aquí no hay ninguna vulnerabilidad explotable<br>
<img width="1711" height="854" alt="image" src="https://github.com/user-attachments/assets/206da0a0-a889-4db8-8559-e73179590f63" /><br>

Como sabemos la versión de wordpress y tenemos credenciales de usuario, realizo una explotación con dicha información desde Metasploit usando el exploit correspondiente a la versión de Wordpress, con esto obtengo una shell de la máquina<br>
<img width="892" height="612" alt="image" src="https://github.com/user-attachments/assets/282f7bde-7018-4fdb-89e8-93a1c0ade97d" /><br>

Busco archivos que tengan el bit SUID activo y veo un programa llamado checker dentro de /sbin <br>
<img width="465" height="404" alt="image" src="https://github.com/user-attachments/assets/5e9ba725-8ac3-4f75-9aef-1448a5993b2c" /><br>

Uso ltrace para ver que funciones realiza el programa checker, este intenta leer la variable de entorno admin y como no existe termina el programa, asique defino la variable admin y al volver a ejecutar checker, como ya existe dicha variable, ahora si me da acceso como root<br>
<img width="451" height="181" alt="image" src="https://github.com/user-attachments/assets/26073ae9-c16f-495a-9422-c0f15ca87909" /><br>

finalmente, siendo root, veo la flag del usuario bjoel en su directorio, pero esta resulta ser falsa, asique la busco en el sistema y veo que la verdadera se encuentra en /media/usb y la flag de root se ubica en el directorio de root<br>
<img width="457" height="385" alt="image" src="https://github.com/user-attachments/assets/b8732506-e8f7-43dd-9f31-1dd3120ff8f9" />

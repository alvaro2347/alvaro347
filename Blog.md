# Blog

Realizo un escaneo con nmap sobre la máquina ejecutando scripts por defecto y realizando detección de versiones de servicios, encuentro un SSH, una web apache y un servicio Samba<br>
<img width="757" height="727" alt="image" src="https://github.com/user-attachments/assets/a4a98dd3-a5a0-4832-85e2-4af4c0bd830c" /><br>

Utilizando whatweb veo que la página está desarrollada usando Wordpress, asique utilizaré wpscan para analizar la web<br>
<img width="1701" height="91" alt="image" src="https://github.com/user-attachments/assets/9f100c4e-1120-4ef6-a542-fc7153e7a0d5" /><br>

Con gobuster veo que en la dirección wp-admin tiene una página de login<br>
<img width="706" height="651" alt="image" src="https://github.com/user-attachments/assets/d7145f68-3969-4d57-b576-ef4bd817abae" /><br>

Para acceder a wp-admin, es necesario utilizar el dominio blog.thm en lugar de la dirección IP. Por este motivo, en /etc/hosts añado una entrada que asocia la IP de la máquina victima con blog.thm, de modo que el sistema pueda resolver correctamente el nombre de dominio<br>
<img width="440" height="124" alt="image" src="https://github.com/user-attachments/assets/7c927f7e-affe-4f51-b903-9746ff79e332" /><br>

utilizo wpscan para escanear la web y enumerar usuarios y plugin vulnerables<br>
<img width="511" height="722" alt="image" src="https://github.com/user-attachments/assets/b85c36fb-30f2-4fef-ab29-0ac7fabaa52a" /><br>
<img width="556" height="644" alt="image" src="https://github.com/user-attachments/assets/1299bae5-4427-4777-85bd-8a5897de2eea" /><br>

Como vemos en la anterior imagen, no encuentra ningún plugin vulnerable, pero si varios usuarios asique guardo esos usuarios en un archivo y realizo fuerza bruta<br>
<img width="618" height="294" alt="image" src="https://github.com/user-attachments/assets/6e5374ed-efef-4738-976f-aec51c94b932" /><br>


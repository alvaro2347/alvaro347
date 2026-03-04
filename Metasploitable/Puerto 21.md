# Puerto 21

Es un servicio FTP con versión vsftpd 2.3.4 y el usuario anónimo de FTP está habilitado
<img width="450" height="278" alt="image" src="https://github.com/user-attachments/assets/b7290a4e-3fb8-48ce-bd31-376fed00f5c6" />

Compruebo que efectivamente se puede acceder con usuario anónimo sin introducir contraseña<br>
<img width="308" height="167" alt="image" src="https://github.com/user-attachments/assets/71083075-ba81-4a7d-9458-64af8a5a3346" />

Busco los exploits para la versión de vsftpd 2.3.4<br>
<img width="447" height="153" alt="image" src="https://github.com/user-attachments/assets/eb7e1e18-bac8-4c65-bf94-653fc187d8ba" />

Descargo el exploit encontrado y lo ejecuto sobre el target, obteniendo así una shell como root
<img width="504" height="311" alt="image" src="https://github.com/user-attachments/assets/4936486a-454f-4cd4-94b4-c3b608136b08" />

Habia otro script el cual es un módulo de metasploit, asique abro la consola de metasploit, ejecuto el script sobre el target y veo que igualmente obtengo una shell como root<br>
<img width="655" height="566" alt="image" src="https://github.com/user-attachments/assets/cfffe310-cafc-44de-ba37-baaaaa525530" />
<img width="977" height="431" alt="image" src="https://github.com/user-attachments/assets/2bdf96f4-337e-45d7-9565-b31ca0f43059" />

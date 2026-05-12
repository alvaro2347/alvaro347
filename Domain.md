# Domain

Se realiza un escaneo con nmap sobre la máquina, ejecutando scripts por defecto y realizando detección de versiones de servicios, se encuentra una web apache y un servicio Samba<br>
<img width="534" height="418" alt="image" src="https://github.com/user-attachments/assets/5459cf6d-9910-44c0-b293-14c5b7ae22ba" />

Utilizando la herramienta smbmap se localizan varios recursos compartidos, pero al intenar acceder con usuario anónimo la conexión es rechazada<br>
<img width="1034" height="764" alt="image" src="https://github.com/user-attachments/assets/fcb2e07c-3da6-4e2e-a2c5-86a4a2f67efc" /><br>
Se realiza otra prueba usando la herramienta smbclient, se localizan los mismos recuros compartidos pero tampoco hay permisos para acceder<br>
<img width="1010" height="267" alt="image" src="https://github.com/user-attachments/assets/31300aff-5b06-45a6-8dcc-2225028c232d" /><br>

Finalmente con la herramienta rpcclient se consigue obtener conexión, utilizando el comando enumdomusers, comando propio de rpcclient, se obtienen dos usuarios, james y bob <br>
<img width="292" height="103" alt="image" src="https://github.com/user-attachments/assets/1421ea1c-22d7-41fc-bc6e-cc7698b82ce1" /><br>

Desde Metasploit, utilizando el módulo smb_login, se realiza fuerza bruta sobre los usuarios de smb
<img width="718" height="687" alt="image" src="https://github.com/user-attachments/assets/ded75bd2-b3ce-42b7-b6a2-316521f8ad3e" /><br>
Tras realizar la fuerza bruta, no se consigue obtener credenciales para el usuario james, pero se obtiene la contraseña del usuario bob<br>
<img width="651" height="99" alt="image" src="https://github.com/user-attachments/assets/47302bf8-6a2c-4dd3-8b07-89401a43dc8f" /><br>
Se consigue acceder mediante smbclient al recurso compartido con las credenciales obtenidas, se sube una shell reversa al directorio para poder ejecutarla<br>
<img width="611" height="363" alt="image" src="https://github.com/user-attachments/assets/d5b05c13-72df-47e9-963c-25ce864a4f46" /><br>



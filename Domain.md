# Domain

Se realiza un escaneo con nmap sobre la máquina, ejecutando scripts por defecto y realizando detección de versiones de servicios, se encuentra una web apache y un servicio Samba<br>
<img width="534" height="418" alt="image" src="https://github.com/user-attachments/assets/5459cf6d-9910-44c0-b293-14c5b7ae22ba" />

Utilizando la herramienta smbmap se localizan varios recursos compartidos, pero al intenar acceder con usuario anónimo la conexión es rechazada<br>
<img width="1034" height="764" alt="image" src="https://github.com/user-attachments/assets/fcb2e07c-3da6-4e2e-a2c5-86a4a2f67efc" /><br>
usando la herramienta smbclient se localizan los mismos recuros compartidos pero tampoco hay permisos para acceder<br>
<img width="1010" height="267" alt="image" src="https://github.com/user-attachments/assets/31300aff-5b06-45a6-8dcc-2225028c232d" /><br>

# Blue

Hago un escaneo con nmap a la máquina intentando detectar versiones de los servicios y ejecutando scripts por defecto asi como scripts para detectar vulnerabilidades, luego guardando el resultado en un archivo <br>
<img width="1079" height="1002" alt="image" src="https://github.com/user-attachments/assets/38c1d619-f960-4c07-8a01-9762ed58195f" />

El escaneo revela que la máquina es vulnerable a ms17-010 el cual corresponde a la conocida vulnerabilidad de smb eternalblue asique desde metasploit busco un módulo para explotar la vulnerabilidad, en este caso voy a utilizar el siguiente: "exploit/windows/smb/ms17_010_eternalblue" <br>
<img width="955" height="598" alt="image" src="https://github.com/user-attachments/assets/b8a51ce4-78e6-4ced-b0f0-042c6c173a97" />

Miro las opciones del exploit y veo que en este caso solo hace falta establecer la máquina objetivo y la atacante, asique la añado y además establezco un payload para que al ejecutar el exploit me devuelva una reverse shell<br>
<img width="727" height="645" alt="image" src="https://github.com/user-attachments/assets/8b8d4aee-999f-4e13-a4d8-19610831be3f" /><br>
Tras ejecutar el exploit ya está establecida la reverse shell<br>
<img width="1008" height="613" alt="image" src="https://github.com/user-attachments/assets/92dcfd2d-834e-4039-9c0a-d412690d2161" />

